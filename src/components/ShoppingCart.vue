<template>
  <div class="shopping-cart">
    <h2 class="center">Shopping Cart</h2>
    <div class="cart-items">
      <div v-for="item in cart" :key="item.id" class="cart-item">
        <div class="item-details">
          <div>{{ item.name }}</div>
          <div>₱{{ item.price }}</div>
        </div>
        <div class="item-controls">
          <input type="number" v-model="item.quantity" @change="updateQuantity(item.id, item.quantity)">
          <button class="remove-from-cart-btn" @click="removeFromCart(item.id)">Remove</button>
        </div>
      </div>
    </div>
    <div class="total">Total: ₱{{ totalPrice }}</div>
  </div>
</template>

<script>
export default {
  props: {
    cart: {
      type: Array,
      required: true,
    },
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
    },
  },
  methods: {
    removeFromCart(productId) {
      this.$emit("remove-from-cart", productId);
    },
    updateQuantity(productId, quantity) {
      this.$emit("update-quantity", { productId, quantity: parseInt(quantity) });
    },
  },
};
</script>

<style scoped>
.center {
  text-align: center;
}

.shopping-cart {
  background-color: #f5f5f5; 
  padding: 20px;
  border-radius: 10px;
  margin-bottom: 20px;
}

.cart-items {
  display: grid;
  grid-template-columns: 1fr;
  gap: 10px;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ccc;
  padding: 10px;
}

.item-details {
  display: flex;
  flex-direction: column;
  flex: 1; 
}

.item-details div {
  margin-bottom: 5px; 
}

.item-controls {
  display: flex;
  align-items: center;
}

.remove-from-cart-btn {
  background-color: #ffa500; 
  border: none;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}

.total {
  text-align: center;
  margin-top: 10px;
}
</style>
