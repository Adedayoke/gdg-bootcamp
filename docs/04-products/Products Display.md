---
  sidebar-positon: 1
---
# Products Display

This page displays all the products retrieved from the **FakeStore API** in a responsive card layout.

---

## 🧾 Overview

The `index.html` file serves as the homepage for our eCommerce site — also known as the "Products Page". It fetches product data from the API and dynamically injects product cards into the DOM.

Each product card displays the following:

- 🖼 **Image**
- 🛍 **Title**
- 📃 **Description**
- 💲 **Price**

It also includes a **Logout** button for user session handling.

---

## 🗂 Files Involved

- `index.html` – structure of the page
- `script.js` – JavaScript logic for fetching and displaying products
- `style.css` – styles for the product cards and layout

---

## 🔄 How it Works

1. When the page loads, a `fetch()` call is made to:
   ```
   https://fakestoreapi.com/products
   ```

2. The response is parsed, and each product is rendered as a card in the `#productContainer` element.

3. Each card includes:

```html
<div class="product-card">
  <img src="..." alt="Product image" />
  <h2>Title</h2>
  <p class="desc">Description text...</p>
  <p class="price">$99.99</p>
</div>
```

4. All product cards are displayed using a CSS grid for responsive layout.

---

## 💡 Features

- Responsive design using CSS Grid
- Minimal layout for focus on content
- Easy to extend with buttons (e.g. “Add to Cart”)

---

## 📜 Sample Code Snippet (JS)

```js
async function fetchProducts() {
  const res = await fetch('https://fakestoreapi.com/products');
  const products = await res.json();

  const productContainer = document.getElementById("productContainer");

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
          <button class="add-to-cart">Add to cart</button>
        </div>
      </div>
    `
    );
  });
}
```

<details>
  <summary>Changes in <code>index.html</code></summary>

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>MiniStore</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <header>
      <h1>MiniStore</h1>
      <button class="logoutBtn">Logout</button>
    </header>

    <main id="productContainer" class="product-grid">
      <!-- Products will be injected here by script.js -->
    </main>

    <script src="script.js"></script>
  </body>
  </html>
  ```

</details>


<details>
  <summary>Changes in <code>script.js</code></summary>

  ```js
  const token = localStorage.getItem("token");

if (!token) {
  // Not logged in, redirect to login
  window.location.href = "login.html";
}

function logout() {
  localStorage.removeItem("token");
  window.location.href = "login.html"; // adjust the path if needed
}


const logoutBtn = document.querySelector("logoutBtn")
if(logoutBtn){
    logoutBtn.addEventListener("click", logout);
}
const productContainer = document.getElementById("productContainer");

async function fetchProducts() {
  try {
    const res = await fetch("https://fakestoreapi.com/products");
    const products = await res.json();
    console.log(products)
    productContainer.innerHTML = products.map(product => `
      <div class="product-card">
        <img src="${product.image}" alt="${product.title}">
        <div class="product-card-content">
          <h3>${product.title}</h3>
          <p>${product.description.slice(0, 100)}...</p>
          <div class="price">$${product.price}</div>
        </div>
      </div>
    `).join("");
  } catch (err) {
    console.error("Failed to load products:", err);
  }
}

fetchProducts();

  ```

</details>


<details>
  <summary>Changes in <code>styles.css</code></summary>

  ```css
  body {
  font-family: sans-serif;
  background: #f4f4f4;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 400px;
  margin: 100px auto;
  padding: 20px;
  background: white;
  border-radius: 8px;
}

input {
  width: 98%;
  margin: 10px 0;
  padding: 10px 3px;
  display: inline-block;
}

button {
  width: 100%;
  padding: 10px;
  background: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 20px;
  padding: 20px;
}

.product-grid div {
  background: white;
  padding: 10px;
  border-radius: 6px;
  text-align: center;
}


 body {
      font-family: sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f8f8f8;
    }
    header {
      background-color: #333;
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .logoutBtn {
      background-color: crimson;
      color: white;
      border: none;
      padding: 0.5rem 1rem;
      cursor: pointer;
      border-radius: 4px;
      width: fit-content;
    }
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 1.5rem;
      padding: 2rem;
    }
    .product-card {
      background: white;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }
    .product-card img {
      width: 100%;
      height: 200px;
      object-fit: contain;
    }
    .product-card-content {
      padding: 1rem;
    }
    .product-card h3 {
      font-size: 1.1rem;
      margin-bottom: 0.5rem;
    }
    .product-card p {
      font-size: 0.9rem;
      margin-bottom: 0.5rem;
      color: #555;
    }
    .product-card .price {
      font-weight: bold;
      color: #2d6a4f;
      font-size: 1rem;
    }

  ```

</details>


:::info[Checkpoint]

- Products load from the FakeStore API  
- Product cards display image, title, description, and price  
- Layout looks clean and responsive

:::