# Stage 4: Side Effects & APIs

In Stage 3, we learned how to update the UI based on user interactions like clicks. But what if you want something to happen automatically when a component first appears? Or what if you need to fetch data from a weather service or a database?

These are called **Side Effects** because they happen _outside_ of the normal React rendering process. To handle them, we use the **`useEffect`** hook.

---

## 1. The `useEffect` Hook

Think of `useEffect` as React’s way of saying, "Hey, now that you’ve finished drawing the UI on the screen, go do this other task."

### Syntax Example:

```javascript
useEffect(() => {
  // Your side-effect code goes here
}, [dependencies]);
```

## 2. The Dependency Array (The Most Important Part)

The second argument of `useEffect` is an array that tells React _when_ to run the effect:

- **`[]` (Empty Array):** The effect runs **only once**, right after the component "mounts" (appears for the first time). This is perfect for API calls.
- **`[variable]`:** The effect runs on the first mount AND every time that specific variable changes.
- **No Array:** The effect runs after **every single render**. (Warning: This is rarely what you want and can cause performance issues!)

---

## 3. Fetching Data with Async/Await

While we learned about `fetch` and `async/await` in our JavaScript curriculum, using them in React requires combining them with `useState` to store the data and `useEffect` to trigger the call.

> **Pro-Tip:** You cannot make the `useEffect` function itself `async`. Instead, define an async function _inside_ the effect and call it immediately.

```javascript
useEffect(() => {
  const fetchData = async () => {
    const response = await fetch("https://api.example.com/data");
    const result = await response.json();
    setData(result);
  };

  fetchData();
}, []); // Empty array means fetch only once
```

---

## 4. Cleanup Functions (Preventing Memory Leaks)

Sometimes your side effects create things that need to be "cleaned up" when the component disappears (unmounts), like a `setInterval` or an event listener.

You do this by **returning a function** from your `useEffect`.

```javascript
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Tick");
  }, 1000);

  // This cleanup function runs when the component unmounts
  return () => {
    clearInterval(timer);
  };
}, []);
```

---

### 🏋️ Micro-Exercise: The Mount Logger

**Goal:** Understand the "Mounting" phase.

1. Create a component called `Logger`.
2. Use `useEffect` with an **empty dependency array**.
3. Inside the effect, `console.log("Component has landed!")`.
4. Add a piece of state called `count` and a button that increments it.
5. Notice that even when you click the button and the component re-renders, the message only logs **once**.

---

## 🚀 Stage 4 Project: The Random Quote Generator

**Goal:** Synchronize React state with external data using an API.

**Instructions:**

1. **The State:** Create two pieces of state: `quote` (an object or string) and `isLoading` (a boolean initialized to `true`).
2. **The Fetch:** Use `useEffect` to fetch a random quote from a public API (like `[https://api.quotable.io/random](https://api.quotable.io/random)`) when the component first loads.
3. **Loading State:** Before your `return` statement, write an `if` statement: if `isLoading` is true, return `<h1>Loading...</h1>`.
4. **Display:** Once the data arrives, set `isLoading` to false and display the quote and the author in a stylized card.
5. **Refresh:** Add a "New Quote" button that triggers the fetch function again to update the state.
