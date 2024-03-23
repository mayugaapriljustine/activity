<template>
  <div id="app">
    <div>
      <product-list :products="products" @add-to-cart="addToCart"></product-list>
    </div>
    <div>
      <shopping-cart :cart="cart" @remove-from-cart="removeFromCart" @update-quantity="updateQuantity"></shopping-cart>
    </div>
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";
import ShoppingCart from "./components/ShoppingCart.vue";

export default {
  name: "App",
  components: {
    ProductList,
    ShoppingCart,
  },
  data() {
    return {
      products: [
        { id: 1, name: "Tote Bag", price: 150.00 },
        { id: 2, name: "Sling Bag", price: 200.00 },
        { id: 3, name: "Belt Bag", price: 250.00 },
        { id: 4, name: "Bagpack", price: 300.00 },
        { id: 5, name: "Handbags", price: 350.00 },
        { id: 6, name: "Bucket Bag", price: 400.00 },
        { id: 7, name: "Clutch Bag", price: 450.00 },
        { id: 8, name: "Beach Bag", price: 500.00 },
        { id: 9, name: "Barrel Bag", price: 550.00 },
        { id: 10, name: "Satchel Bag", price: 600.00 },
        
      ],
      cart: [],
    };
  },
  methods: {
    addToCart(product) {
      const existingItemIndex = this.cart.findIndex(item => item.id === product.id);
      if (existingItemIndex !== -1) {
        this.cart[existingItemIndex].quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeFromCart(productId) {
      this.cart = this.cart.filter(item => item.id !== productId);
    },
    updateQuantity(payload) {
      const { productId, quantity } = payload;
      const cartItem = this.cart.find(item => item.id === productId);
      if (cartItem) {
        cartItem.quantity = quantity;
      }
    },
  },
};
</script>

<style>
#app {
  display: inline-block;
  flex-direction: column; 
  align-items: center; 
  padding: 40px;
}
</style>
