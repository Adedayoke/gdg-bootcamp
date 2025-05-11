---
sidebar-position: 2
---

# Add to Cart

This section explains how the **"Add to Cart"** functionality works in our MiniStore project. It enables users to add products to a shopping cart, which is stored in memory (via an array) and reflected on the UI.

---

## 🧾 Overview

When a user clicks the **"Add to cart"** button on any product card, the corresponding product is added to the cart array. The total number of items in the cart is then updated and displayed in the header.

This functionality is managed using:

- Event delegation
- Data attributes (`data-index`)
- State management via an in-memory `cart[]` array

---

## 🗂 Files Involved

- `index.html` – contains the cart indicator and buttons
- `script.js` – handles the logic for adding items to the cart
- `style.css` – styles the cart display in the header

---

## 🔄 How it Works

1. A `cart[]` array is initialized to keep track of added products.
2. Each product button is rendered with a `data-index` attribute representing the product's `id`.
3. A click event listener on the parent container (`#productContainer`) uses **event delegation** to capture clicks on "Add to cart" buttons.
4. When a button is clicked, the corresponding product is looked up using its ID and added to the cart.
5. The cart amount is updated and shown beside the "Cart" label in the header.

---

## 🧠 Why Event Delegation?

Instead of attaching a listener to each button individually (which may not exist when the page loads), we attach one listener to the parent container. This improves performance and avoids potential bugs with dynamically loaded content.

---

## 📜 Sample Code Snippet (JS)

```js
const cart = [];
let allProducts = [];

const cartAmount = document.querySelector(".cartAmount");
const productContainer = document.getElementById("productContainer");

function resetCart() {
  cartAmount.innerText = `${cart.length}`;
}

// Handle "Add to cart" clicks
productContainer.addEventListener("click", function (e) {
  const id = e.target.getAttribute("data-index");
  const product = allProducts.find((p) => p.id == id);

  if (product) {
    cart.push(product);
    resetCart();
  }
});
```

<details> 
    <summary>HTML Snippet with <code>data-index</code></summary>
    ```html
    <button class="add-to-cart" data-index="3">Add to cart</button>
    ```
</details>

<details> 
<summary>Cart Indicator in <code>index.html</code></summary>
```html
<header>
  <h1>MiniStore</h1>
  <div class="header-cart-container">
    <p>Cart(<span class="cartAmount">0</span>)</p>
    <button class="logoutBtn">Logout</button>
  </div>
</header>


<details> 
<summary>Css button style<code>styles.css</code></summary>
```css
    .header-cart-container{
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-weight: 900;
        gap: 10px;
    }
    .header-cart-container p{
        cursor: pointer;
    }
```
</details>

<details> 
<summary>Final code in<code>script.js</code></summary>
```js
// =======================
// MiniStore Script
// =======================

// Cart and Product Variables
const cart = [];
let allProducts = [];

// Token Check for Authentication
const token = localStorage.getItem("token");

if (!token) {
  // Redirect to login if not logged in
  window.location.href = "login.html";
}

// -----------------------
// Logout Functionality
// -----------------------

function logout() {
  localStorage.removeItem("token");
  window.location.href = "login.html"; // Adjust path if needed
}

const logoutBtn = document.querySelector(".logoutBtn");
logoutBtn.addEventListener("click", logout);

// -----------------------
// Cart Display Update
// -----------------------

const cartAmount = document.querySelector(".cartAmount");

function updateCartDisplay() {
  cartAmount.innerText = `${cart.length}`;
}

// -----------------------
// Display Products
// -----------------------

const productContainer = document.getElementById("productContainer");

function displayProducts(products) {
  products.forEach((product) => {
    productContainer.insertAdjacentHTML(
      "afterbegin",
      `
      <div class="product-card">
        <img src="${product.image}" alt="${product.title}">
        <div class="product-card-content">
          <h3>${product.title}</h3>
          <p>${product.description.slice(0, 100)}...</p>
          <div class="price">$${product.price}</div>
          <button class="add-to-cart" data-index="${product.id}">
            Add to cart
          </button>
        </div>
      </div>
    `
    );
  });
}

// -----------------------
// Add to Cart (Event Delegation)
// -----------------------

productContainer.addEventListener("click", function (e) {
  if (e.target.classList.contains("add-to-cart")) {
    const id = e.target.getAttribute("data-index");
    const product = allProducts.find((p) => p.id == id);

    if (product) {
      cart.push(product);
      updateCartDisplay();
    }
  }
});

// -----------------------
// Fetch Products from API
// -----------------------

async function fetchProducts() {
  try {
    const res = await fetch("https://fakestoreapi.com/products");
    const products = await res.json();
    allProducts = products;
    displayProducts(products);
  } catch (err) {
    console.error("Failed to load products:", err);
  }
}

// -----------------------
// Initialize
// -----------------------

fetchProducts();

```
</details>

## 💡 Features
- Real-time update of cart count
- No page reload needed
- Easily extendable for full cart page or checkout functionality

:::info[Checkpoint]
- "Add to Cart" buttons work for each product
- Cart count updates in the header dynamically
- Data binding uses data-index and event delegation
:::
