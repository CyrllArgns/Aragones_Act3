<template>
    <div class="cart">
        <h2>Shopping Cart</h2>
        
        <div class="cart-headers">
            <span class="header">Product Name</span>
            <span class="header">Price</span>
            <span class="header">Quantity</span>
        </div>
        <ul class="cart-items">
            <li v-for="item in cart" :key="item.id" class="cart-item">
                <span class="product-name">{{ item.name }}</span>
                <span class="price">₱{{ calculateItemPrice(item) }}</span>
                <span class="quantity">
                    <button @click="openPromptDialog(item)">Edit Quantity</button>
                    <span>{{ item.quantity }}</span>
                </span>
                <button @click="removeItem(item.id)" class="remove-button">Remove</button>
            </li>
        </ul>
        <p class="total">Total: ₱{{ total }}</p>
    </div>
</template>

<script>
import { cart } from '../main.js';

export default {
    data() {
        return {
            cart: cart,
            editedQuantity: 1,
            selectedItem: null
        };
    },
    computed: {
        total() {
            return this.cart.reduce((total, item) => total + (item.unitPrice * item.quantity), 0);
        }
    },
    methods: {
        calculateItemPrice(item) {
            return item.unitPrice * item.quantity;
        },
        removeItem(itemId) {
            this.cart.splice(itemId, 1);
        },
        openPromptDialog(item) {
            this.selectedItem = item;
            const newQuantity = prompt(`Enter new quantity for ${item.name}:`, item.quantity);
            if (newQuantity !== null) {
                this.editedQuantity = parseInt(newQuantity);
                this.saveEditedQuantity();
            }
        },
        saveEditedQuantity() {
            if (!isNaN(this.editedQuantity) && this.editedQuantity > 0) {
                this.selectedItem.quantity = this.editedQuantity;
            } else {
                alert("Please enter a valid quantity.");
            }
        }
    }
};
</script>

<style>

.shopping-cart {
  max-width: 600px;
  margin: 0 auto;
}

.cart-headers {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  margin-top: 10px;
}

.cart-headers .header {
  font-weight: bold;
}

.cart-items {
  list-style-type: none;
  padding: 0;
}

.cart-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid #ddd;
  padding: 10px 0;
}

.cart-item .product-name,
.cart-item .price,
.cart-item .quantity {
  flex: 1;
  text-align: left;
}

.cart-item .price {
    margin-left: 37.5%;
}
.cart-item .quantity {
  margin-left: 20%;
}

.cart-item .quantity button {
  background-color: #001d8f;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
  margin-right: 22%;
}

.cart-item .quantity span {
  margin: 0 5px;
}

.remove-button {
  background-color: #dc1c12;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}

.edit-dialog {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

.edit-dialog input[type="number"] {
    width: 50px;
    padding: 5px;
    margin-right: 10px;
}

.edit-dialog button {
    padding: 5px 10px;
    margin-right: 10px;
    cursor: pointer;
}

.edit-dialog button:last-child {
    margin-right: 0;
}
.total {
  text-align: right;
  margin-top: 20px;
  font-weight: bold;
  background-color: #0d7f23;
  color: #fff;
  border: none;
  padding: 10px 10px;
  border-radius: 10px;
  cursor: pointer;
}
</style>
