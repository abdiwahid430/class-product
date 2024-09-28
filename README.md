class Product {
    constructor(id, name, price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }
}
class ShoppingCartItem {
    constructor(product, quantity) {
        this.product = product;
        this.quantity = quantity;
    }

    // Method to calculate total price for this item
    getTotalPrice() {
        return this.product.price * this.quantity;
    }
}
class ShoppingCart {
    constructor() {
        this.items = []; // Array to hold ShoppingCartItem instances
    }

    // Method to add items
    addItem(product, quantity) {
        const existingItem = this.items.find(item => item.product.id === product.id);
        if (existingItem) {
            existingItem.quantity += quantity; // Increase quantity if item already exists
        } else {
            const cartItem = new ShoppingCartItem(product, quantity);
            this.items.push(cartItem); // Add new item
        }
    }

    // Method to remove items
    removeItem(productId) {
        this.items = this.items.filter(item => item.product.id !== productId);
    }

    // Method to get the total of items inside the cart
    getTotal() {
        return this.items.reduce((total, item) => total + item.getTotalPrice(), 0);
    }

    // Method to display cart items
    displayItems() {
        this.items.forEach(item => {
            console.log(`${item.product.name} (x${item.quantity}): $${item.getTotalPrice().toFixed(2)}`);
        });
    }
}
// Creating products
const product1 = new Product(1, "Apple", 0.99);
const product2 = new Product(2, "Banana", 0.79);
const product3 = new Product(3, "Orange", 1.29);

// Creating a shopping cart
const cart = new ShoppingCart();

// Adding items to the cart
cart.addItem(product1, 3); // 3 Apples
cart.addItem(product2, 2); // 2 Bananas
cart.addItem(product3, 1); // 1 Orange

// Display the cart items
console.log("Cart Items:");
cart.displayItems();
console.log(`Total: $${cart.getTotal().toFixed(2)}`);

// Removing an item from the cart
cart.removeItem(2); // Remove Bananas

// Display the updated cart items
console.log("\nUpdated Cart Items:");
cart.displayItems();
console.log(`Total: $${cart.getTotal().toFixed(2)}`);

