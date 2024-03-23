<template>
  <div>
    <h2 class="center">Products</h2>
    <div class="product-columns">
      <div v-for="(column, index) in productColumns" :key="index" class="product-column">
        <ul class="product-list">
          <li v-for="product in column" :key="product.id" class="product-item">
            <div>{{ product.name }}</div>
            <div>₱{{ product.price }}</div>
            <button class="add-to-cart-btn" @click="addToCart(product)">Add to Cart</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      productColumns: [], 
    };
  },
  mounted() {
    this.splitProductsIntoColumns();
  },
  methods: {
    addToCart(product) {
      this.$emit("add-to-cart", product);
    },
    splitProductsIntoColumns() {
      const productsCopy = [...this.products];
      const numColumns = 2;
      const productsPerColumn = Math.ceil(this.products.length / numColumns);
      for (let i = 0; i < numColumns; i++) {
        this.productColumns.push(productsCopy.splice(0, productsPerColumn));
      }
    },
  },
};
</script>

<style scoped>
.center {
  text-align: center;
}

.product-columns {
  display: flex;
  justify-content: space-around;
}

.product-column {
  flex: 1;
  margin: 0 10px; 
}

.product-list {
  list-style: none;
  padding: 0;
}

.product-item {
  display: flex;
  flex-direction: column; 
  align-items: center; 
  text-align: center; 
  margin-bottom: 5px;
}

.product-item div {
  margin-bottom: 5px; 
}

.add-to-cart-btn {
  background-color: #ffa500;
  border: none;
  color: white;
  padding: 5px 10px;
  border-radius: 10px;
  cursor: pointer;
}
</style>
