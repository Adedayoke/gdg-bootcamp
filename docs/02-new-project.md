---
    sidebar-position: 2
---


# Project Setup

Welcome! Before we dive into building our eCommerce app using JavaScript and the FakeStore API, let’s get your environment ready and the project initialized.

---

## 📦 Package Manager & Tools

To keep things simple and compatible across systems, we’ll use:

- **Node.js** (version 18 or above recommended)
- **Live Server** (for real-time HTML/JS updates)
- **VS Code** (or your preferred text editor)

You can use any package manager you're comfortable with:
- `npm`
- `yarn`
- `pnpm`
- `bun`

But for this course, we’ll mostly use **npm**.

---

## 🏁 Project Options

You can start the course in **three different ways**:

### 🔹 1. Clone Starter Repository

If you want to skip initial setup and get straight into coding, clone the starter template:

```bash
git clone https://github.com/Adedayoke/js-ecommerce-starter.git
cd js-ecommerce-starter
npm install
```

:::tip[Tip]
Replace the GitHub URL with the actual repo once created.
:::

### 🔹 2. Create a New Folder Manually

Prefer building it from scratch? Here's what to do:

```bash
mkdir js-ecommerce-app
cd js-ecommerce-app
code .
```
Then inside your editor, create these files and folders:

```pgsql
mkdir js-ecommerce-app
cd js-ecommerce-app
code .
```
You’ll link the JS and CSS files in your index.html.

### 🔹 3. Code Along

Just open your favorite editor and code along with me. I’ll guide you step-by-step — no pressure to use any template or starter repo.

## 🚀 Run Your App Locally
We’ll use a simple Live Server to preview our app in real-time.

If using VS Code:

- Install the Live Server extension.
- Right-click on index.html → Open with Live Server.

Or install it globally with npm:

```bash
npm install -g live-server
```
Then run:
```bash
live-server
```
> This will open your app at http://127.0.0.1:8080 in the browser.

## 💡 Do I Need a Backend?
Nope! We’ll use the FakeStore API, which simulates a real eCommerce backend with endpoints like:

- GET /products
- GET /products/:id
- GET /carts
- POST /auth/login

We’ll interact with this API using JavaScript’s fetch() method.

:::info[Checkpoint]
 - Folder created
 - index.html, style.css, script.js set up
 - Live server is running
 - Ready to start coding!
 :::

 :::tip[Debug tip]
 If live-server doesn’t auto-refresh, try restarting it or clearing your browser cache.
:::

 :::tip[Pro tip]
Create a GitHub repo early to save your progress regularly.
:::


