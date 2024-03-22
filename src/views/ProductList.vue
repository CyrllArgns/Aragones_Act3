<template>
    <div class="product">
        <h2 class="products-heading">Products List</h2>
        <ul class="products-list">
            <li v-for="item in products" :key="item.id" class="product-item">
                <b><span class="product-details">{{ item.name }} - ₱{{ item.price }}</span></b>
                <p></p>
                <button @click="addToCart(item)" class="add-to-cart-btn">Add to Cart</button>
            </li>
        </ul>
    </div>
</template>

<script>
import { cart } from '../main.js';

export default {
    data() {
        return {
            products: [
                { name: 'Tapsilog', price: 105 },
                { name: 'Longsilog', price: 75 },
                { name: 'Tocilog', price: 95 },
                { name: 'Hotsilog', price: 75 },
                { name: 'Bangsilog', price: 85 },
                { name: 'Chicksilog', price: 85 },
                { name: 'Bacsilog', price: 75 },
                { name: 'Spamsilog', price: 65 },
                { name: 'Cornsilog', price: 65 },
                { name: 'Tunasilog', price: 75 },
            ],
        };
    },
    methods: {
        addToCart(item) {
            const existingProductIndex = cart.findIndex(product => product.name === item.name);
            if (existingProductIndex !== -1) {
                
                window.alert(`${item.name} is already exists in your cart!`);
                return;
            }

            // If the product is not in the cart, add it

            cart.push({
                name: item.name,
                price: item.price,
                unitPrice: item.price,
                quantity: 1,
            });

            window.alert(`Added ${item.name} to your cart!`);
        },
    }
};
</script>


<style>

.products-heading {
  font-size: 50px;
  margin-bottom: 20px;
}

.products-list {
  display: flex;
  flex-wrap: wrap; /* Wrap items to the next row */
  gap: 80px; /* Spacing between items */
  padding: 70px;
}

.product-item {
  flex: 20; /* Allow items to grow to fill available space */
  min-width: 200px; /* Minimum width of each item */
  max-width: calc(50% - 20px); /* Maximum width (50% minus spacing) for two items per row */
  border: 5px solid #ccc;
  padding: 10px;
}

.product-details {
  font-size: 20px;
}

.add-to-cart-btn {
  background-color: #0d7f23;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 25px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.add-to-cart-btn:hover {
  background-color: #0d7f23;
}

</style>


