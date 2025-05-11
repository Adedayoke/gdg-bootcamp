---
  sidebar-position: 3
---

#  Authentication Helper Functions

In this section, we’ll break down the authentication logic for the login and signup system in our JavaScript eCommerce app. We'll interact with the [FakeStore API](https://fakestoreapi.com/) to simulate real-world login and user creation.

---

## 📦 Helper Functions Overview

Here are the key helper functions we use:

### ✅ `setToken(token)`
This function stores the JWT token (received from a successful login) into `localStorage`.

```js
function setToken(token) {
  if (!token) return;
  console.log("Token set");
  localStorage.setItem("token", JSON.stringify(token));
}
```

- `localStorage` persists the token even after page refresh.
- This token can be used to authorize future requests (not needed for FakeStore, but great for real APIs).


### 📥 `getToken()`
Fetches the token back from localStorage. `localStorage`.

```js
function getToken() {
  const token = localStorage.getItem("token");
  return token ? JSON.parse(token) : null;
}
```

### 🔐 `login(credentials)`
Handles user login by sending their username and password to the FakeStore API.

```js
async function login(credentials) {
  // ...validation

  const response = await fetch("https://fakestoreapi.com/auth/login", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(credentials),
  });

  const { token } = await response.json();
  setToken(token); // Store token
  window.location.href = "index.html"; // Redirect on success
}

```

- If login fails (wrong username or password), an alert notifies the user.
- On success, we:
    - Store the returned `token`
    - Redirect to the homepage


### 🆕 `signup(user)`
Creates a new user by posting their data to the FakeStore API.

```js
async function signup(user) {
  const response = await fetch("https://fakestoreapi.com/users", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(user),
  });

  const data = await response.json();
  alert("Signup successful!");
  window.location.href = "login.html";
}
```

- We collect `username`, `email`, and `password` from the signup form.
- On successful signup, the user is redirected to the login page.

:::warning
    The FakeStore API doesn't actually save users permanently, but this simulates the process in real apps.
:::


