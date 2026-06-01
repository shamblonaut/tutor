# Stage 4: Side Effects & APIs

In Stage 3, we learned how to update the UI based on user interactions like clicks. But what if you want something to happen automatically when a component first appears? Or what if you need to fetch data from a weather service or a database?

These are called **Side Effects** because they happen _outside_ of the normal React rendering process. To handle them, we use the **`useEffect`** hook.

---

## 1. The `useEffect` Hook

Think of `useEffect` as React’s way of saying, "Hey, now that you’ve finished drawing the UI on the screen, go do this other task."

### Syntax Example:

```javascript
import { useEffect } from "react";

useEffect(() => {
  // Your side-effect code goes here
}, [dependencies]);
```

---

## 2. The Dependency Array & Render Loops

The second argument of `useEffect` is an array that tells React _when_ to run the effect:

- **`[]` (Empty Array):** The effect runs **only once**, right after the component "mounts" (appears for the first time). This is perfect for API calls.
- **`[variable]`:** The effect runs on the first mount AND every time that specific variable changes.
- **No Array:** The effect runs after **every single render**.

> **⚠️ The Infinite Render Loop Trap**
> If you update a state variable inside `useEffect` and do not provide a dependency array, or if you add that state variable to the dependency array, you will trigger an infinite loop:
> 1. Component renders.
> 2. Effect runs and updates state.
> 3. State update triggers a re-render.
> 4. Effect runs again (and cycles forever, crashing your app).

---

## 3. Fetching Data with Async/Await & Load States

While we learned about `fetch` and `async/await` in our JavaScript curriculum, using them in React requires combining them with `useState` to store the data and `useEffect` to trigger the call.

It's also important to manage **loading** and **error** states so that the user knows the status of the network request.

> **Pro-Tip:** You cannot make the `useEffect` callback function itself `async`. Instead, define an async function _inside_ the effect and call it immediately.

```javascript
import { useState, useEffect } from "react";

function DataFetcher() {
  const [data, setData] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setIsLoading(true);
        const response = await fetch("https://api.example.com/data");
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError("Failed to fetch data.");
      } finally {
        setIsLoading(false);
      }
    };

    fetchData();
  }, []); // Empty array means fetch only once on mount

  if (isLoading) return <p>Loading data...</p>;
  if (error) return <p style={{ color: "red" }}>{error}</p>;

  return (
    <ul>
      {data.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

---

## 4. Cleanup Functions (Preventing Memory Leaks)

Sometimes your side effects create things that need to be "cleaned up" when the component disappears (unmounts) or before the effect runs again, like a `setInterval` or an event listener.

You do this by **returning a function** from your `useEffect`.

```javascript
import { useEffect } from "react";

function Timer() {
  useEffect(() => {
    const timer = setInterval(() => {
      console.log("Tick");
    }, 1000);

    // This cleanup function runs when the component unmounts
    // OR before running the effect code again (if dependencies change)
    return () => {
      clearInterval(timer);
    };
  }, []);

  return <p>Timer is running. Check your console logs!</p>;
}
```

---

## 5. Exercises & Projects

### 🏋️ Micro-Exercise: The Mount Logger

**1. Setup:**
Create a component called `Logger.jsx` and import it into your `App.jsx` file.

**2. Your Task:**
- Create a piece of state called `count` and a button that increments it.
- Implement `useEffect` with an **empty dependency array**.
- Inside the effect, `console.log("Component has landed!")`.
- Add a second `useEffect` that has `[count]` as its dependency array and logs `count` each time it changes.
- Click the increment button and observe which logs fire and how often.

**3. Expected Outcome:**
The "Component has landed!" log should only fire once on load. The second log should fire on load and every time the button is clicked.

---

## ⚠️ Common Pitfalls

1. **Infinite Loop by Modifying Dependents:**
   ```javascript
   // ❌ CRASH: Effect updates count, which triggers effect, which updates count...
   useEffect(() => {
     setCount(count + 1);
   }, [count]);
   ```
2. **Forgetting the Dependency Array Entirely:**
   ```javascript
   // ❌ Runs on EVERY single render
   useEffect(() => {
     doSomething();
   }); 
   ```
3. **Stale Closures in Effects:**
   If you reference variables inside `useEffect` but don't add them to the dependency array, the effect will continue using their values from the render session when the effect was created, resulting in stale data.

---

## 🧠 Brain Teasers & Concept Checks

Predict the outputs/actions of the following snippets:

1. How many times will "Fetch active" be logged?
   ```javascript
   function Users() {
     const [users, setUsers] = useState([]);
     useEffect(() => {
       console.log("Fetch active");
       fetch("/api/users").then(r => r.json()).then(setUsers);
     }); // <-- Note the missing array!
     return <div>Count: {users.length}</div>;
   }
   ```
2. In what order will the console logs appear when this component mounts and then unmounts?
   ```javascript
   useEffect(() => {
     console.log("Effect run");
     return () => {
       console.log("Cleanup run");
     };
   }, []);
   ```

---

## 🚀 Stage 4 Project: The Random Quote Generator

**The Goal:** Synchronize React state with external data using an API.

**1. Starter Setup:**
Create a component called `QuoteGenerator.jsx`. You can use the public Quotes API: `https://api.allorigins.win/raw?url=https://zenquotes.io/api/random` (or any free public quote API).

**2. Your Task:**
- Create three pieces of state: `quote` (an object with author and text), `isLoading` (boolean, default `true`), and `error` (string, default `null`).
- Create an async function `fetchQuote` that fetches a random quote, handles errors using `try/catch`, and sets the state.
- Call `fetchQuote` inside a `useEffect` with an empty dependency array.
- In your JSX, write conditional returns:
  - If `isLoading` is true, render a Loading spinner/header.
  - If `error` is not null, render the error message.
  - Otherwise, render the quote text and author.
- Add a "New Quote" button that manually triggers the `fetchQuote` function to update state.

**3. Expected Outcome:**
On load, a loading indicator appears, followed by a random quote. Clicking the "New Quote" button displays the loading state again and fetches a fresh quote.
