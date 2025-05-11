---
  sidebar-position: 2
---


# Connecting Forms to Logic

We use **event listeners** to handle form submission:

```js
const loginForm = document.getElementById("loginForm");
const signupForm = document.getElementById("signupForm");
```

- When users submit a form, we prevent the default reload and grab form values using `querySelector`.
- The values are passed to `login()` or `signup()`.

```js

// Login form submit
if (loginForm) {
  loginForm.addEventListener("submit", function (e) {
    e.preventDefault();
    const username = loginForm.querySelector("#loginUsername").value.trim();
    const password = loginForm.querySelector("#loginPassword").value.trim();
    login({ username, password });
  });
}

// Signup form submit
if (signupForm) {
  signupForm.addEventListener("submit", function (e) {
    e.preventDefault();
    const username = signupForm.querySelector("#signupUsername").value.trim();
    const email = signupForm.querySelector("#signupEmail").value.trim();
    const password = signupForm.querySelector("#signupPassword").value.trim();
    signup({ username, email, password });
  });
}
```
- Checks if the `loginForm` or `signupForm` exists because the same javascript file `auth.js` is used for `login.html` and `signup.html`

:::info[Checkpoint]
 - Login and Signup forms working
 - Users are redirected after actions
 - Token saved in localStorage
 :::

 :::tip[Debug tip]
If login isn't working:
    - Confirm credentials from FakeStore
    - Check console logs and network tab
    - Make sure forms have correct `id` selectors
:::

> Next up: we’ll protect the homepage and start rendering products from the FakeStore API!