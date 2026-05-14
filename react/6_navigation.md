# Stage 6: Navigation & Routing

Until now, our apps have felt like single "rooms." You click a button, and the content inside that room changes. But most websites feel like "houses" with different rooms (pages) like `/home`, `/about`, or `/contact`.

In React, we use **React Router** to change the URL in the browser and show different components without the page ever having to refresh. This creates a **Single Page Application (SPA)** experience.

---

## 1. The React Router Components

To turn your app into a multi-page site, you use a few core "wrapper" components provided by the `react-router-dom` library:

- **`<BrowserRouter>`**: The "parent" wrapper that manages your history and keeps the UI in sync with the URL.
- **`<Routes>` & `<Route>**`: These act like a switchboard. When the URL matches a defined `path`, the corresponding `element` (component) is rendered.
- **`<Link>`**: Instead of using standard `<a href="...">` tags (which refresh the entire browser), we use `Link` to tell React Router to switch the view instantly.

## 2. Dynamic Routing (URL Parameters)

What if you have 100 products? You don't want to create 100 manual routes. Instead, you use a **colon** in the path to create a "slug" or variable.

### Syntax Example: 

```javascript
<Route path="/product/:id" element={<ProductDetail />} />
```

Inside the `ProductDetail` component, you can use the `useParams` hook to grab that specific `id` and use it to fetch the correct data from an API.

---

### 🏋️ Micro-Exercise: The Mini-Site

**Goal:** Create a 2-page site with a persistent navigation bar.

1. Install `react-router-dom` in your project.
2. Create two components: `Home` (renders "Welcome Home") and `About` (renders "This is who we are").
3. Wrap your entire `App` in `<BrowserRouter>`.
4. Create a `<nav>` component with `<Link>` tags pointing to `/` and `/about`.
5. Set up your `<Routes>` so that each path renders the correct component.

---

## 🚀 Stage 6 Project: The Mini-E-Commerce Storefront

**Goal:** Combine every concept from Stage 1 to 6 into a cohesive, multi-page application.

**Instructions:**

1. **The Home Page:** Fetch a list of products from an API (like `[https://fakestoreapi.com/products](https://fakestoreapi.com/products)`) using `useEffect`. Render them as a list of `ProductCard` components using the `.map()` method.
2. **The Detail Page:** When a user clicks a product, navigate them to `/product/:id`. Use the `useParams` hook to get the specific ID and fetch only that product's data.
3. **The Cart (State Management):** Keep a `cart` state in your top-level `App` component (Lifting State Up!). Allow users to add items to the cart from the Detail Page.
4. **The Cart Page:** Create a `/cart` route that displays every item added to the state and calculates the total price using basic math operators.
