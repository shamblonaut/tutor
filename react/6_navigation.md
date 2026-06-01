# Stage 6: Navigation & Routing

Until now, our apps have felt like single "rooms." You click a button, and the content inside that room changes. But most websites feel like "houses" with different rooms (pages) like `/home`, `/about`, or `/contact`.

In a traditional website, clicking a link fetches a completely new HTML file from a server, causing a blank screen flash. In React, we use **React Router** to change the URL in the browser and show different components without the page ever having to refresh. This is called a **Single Page Application (SPA)**.

---

## 1. The Core Routing Setup

To turn your app into a multi-page site, you use components from the `react-router-dom` library. We divide routing responsibilities into two files:

1. **The Wrapper (`main.jsx`)**: Tells React to track browser history.
2. **The Layout & Switchboard (`App.jsx`)**: Displays persistent navigation and determines which sub-component to show based on the active URL.

### Step A: Wrapping the App (in `main.jsx` or `index.jsx`)

Wrap the `<App />` component in `<BrowserRouter>` so that routing logic is available anywhere in your application.

```javascript
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { BrowserRouter } from "react-router-dom";

import App from "./App";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
);
```

### Step B: The Layout & Routing Switchboard (in `App.jsx`)

- **`<Routes>` & `<Route>`**: These act like a switchboard. When the URL matches a defined `path`, the corresponding `element` is rendered.
- **`<NavLink>`**: Renders a clickable link. It automatically gets an `active` class applied to it when its path matches the current browser URL (perfect for styling active navigation tabs!).

```javascript
import { Routes, Route, NavLink } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import Contact from "./pages/Contact";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <div className="app-container">
      {/* 1. Persistent Navigation Header */}
      <nav className="navbar">
        <NavLink to="/" end>
          Home
        </NavLink>
        <NavLink to="/about">About Us</NavLink>
        <NavLink to="/contact">Contact</NavLink>
      </nav>

      {/* 2. Dynamic Content Area (Changes based on URL) */}
      <main className="content">
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
          {/* Catch-all 404 Route */}
          <Route path="*" element={<NotFound />} />
        </Routes>
      </main>
    </div>
  );
}

export default App;
```

---

## 2. Dynamic Routing & Hooks

### 📂 URL Parameters (Dynamic Slugs)

What if you have 100 products? You don't want to create 100 manual routes. Instead, you use a **colon** in the path to create a variable parameter (a slug):

```javascript
// Inside App.jsx Routes:
<Route path="/product/:id" element={<ProductDetail />} />
```

Inside the `<ProductDetail />` component, use the `useParams` hook to read the dynamic parameter value from the URL and fetch the correct data:

```javascript
import { useParams } from "react-router-dom";

function ProductDetail() {
  const { id } = useParams(); // Grabs "id" from the URL slug /product/123

  return (
    <div>
      <h2>Product Details</h2>
      <p>Viewing product with ID: {id}</p>
    </div>
  );
}
```

### ➡️ Programmatic Navigation (`useNavigate`)

Sometimes you need to redirect the user automatically after an event happens, like submitting a form or clicking a login button. For this, use the `useNavigate` hook:

```javascript
import { useNavigate } from "react-router-dom";

function ContactForm() {
  const navigate = useNavigate();

  const handleFormSubmit = (e) => {
    e.preventDefault();
    // 1. Submit form details to an API here...
    // 2. Redirect programmatically to the confirmation page
    navigate("/thanks");
  };

  return (
    <form onSubmit={handleFormSubmit}>
      <button type="submit">Submit Feedback</button>
    </form>
  );
}
```

---

## 3. Exercises & Projects

### 🏋️ Micro-Exercise: The Mini-Site

**1. Setup:**

- Install `react-router-dom` in your project.
- In `main.jsx`, wrap `<App />` in `<BrowserRouter>`.

**2. Your Task:**

- Create three basic page components: `Home.jsx` (renders "Welcome Home"), `About.jsx` (renders "This is who we are"), and `NotFound.jsx` (renders "404 Page Not Found").
- In `App.jsx`, render a `<nav>` with `<NavLink>` tags pointing to `/` and `/about`.
- In `App.jsx` under the nav, configure your `<Routes>` layout. Include `/` mapping to `Home`, `/about` mapping to `About`, and a catch-all route `*` mapping to `NotFound`.
- Add active link styling in `index.css` to verify `<NavLink>` active classing:
  ```css
  nav a.active {
    color: #ff5722;
    font-weight: bold;
  }
  ```

**3. Expected Outcome:**
Clicking navbar links switches page contents instantly with no full page refresh. Active links change color dynamically. Typing an invalid URL in the address bar displays the "NotFound" component.

---

## ⚠️ Common Pitfalls

1. **Using Standard `<a>` Anchor Tags:**
   Using `<a href="/about">` causes the browser to refresh the whole page, losing all active React memory state. Always use `<Link>` or `<NavLink>` instead!
2. **Placing Routing Components Outside `<BrowserRouter>`:**
   Hooks like `useParams`, `useNavigate` and components like `<Link>`, `<Routes>`, or `<Route>` will crash if they are rendered outside a `<BrowserRouter>` context wrapper.
3. **Forgetting the Leading Slash in `to` and `path` Attributes:**
   Ensure paths are absolute relative to the domain (e.g., `<Link to="/about">`, not `<Link to="about">`), unless you are intentionally configuring nested, relative sub-routes.

---

## 🧠 Brain Teasers & Concept Checks

Predict the outputs or behaviors of these routing scenarios:

1. What hook would you use inside a `<UserProfile />` component if the path is set as `/user/:username` and you need to get the active username?
2. Why does client-side routing feel faster than standard multi-page website routing?
3. Where does the catch-all `<Route path="*" element={<NotFound />} />` need to be positioned relative to other routes?

---

## 🚀 Stage 6 Project: The Mini-E-Commerce Storefront

**The Goal:** Combine every concept from Stage 1 to 6 into a cohesive, multi-page application.

**1. Starter Setup:**
Ensure `react-router-dom` is installed and `<BrowserRouter>` is wrapping your app. Create `Home.jsx`, `Detail.jsx`, `Cart.jsx`, and `Navbar.jsx` components.

**2. Your Task:**

- **Home Page (`/`):** Fetch a list of products from `https://fakestoreapi.com/products` using `useEffect`. Render them as a list of product cards, each containing a `<Link to={\`/product/\${product.id}\`}>` wrapper.
- **Detail Page (`/product/:id`):** When a user loads this page, use `useParams` to grab the ID and fetch details for that specific product. Show an "Add to Cart" button.
- **Global Cart State:** Maintain a `cart` state array in the `App.jsx` component. Pass down a callback to add items to the cart.
- **Detail Add-to-Cart Redirect:** When the "Add to Cart" button is clicked in the Detail component, update the global cart state and use `useNavigate` to redirect the user programmatically to the `/cart` page.
- **Cart Page (`/cart`):** Show the contents of the cart and calculate the total price using mathematical operators.

**3. Expected Outcome:**
A fully functional mini-store. Users can browse products, click to view details, add products to their cart, see their updated cart, and navigate between pages fluidly with persistent navigation state.
