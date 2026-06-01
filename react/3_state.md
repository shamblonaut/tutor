# Stage 3: State & Interactivity

Stage 2 taught us how to pass data _into_ a component using props, but props are read-only. If you want a component to "remember" that a user clicked a button or typed into a form, you need **State**.

**State** is a component's private memory. When state changes, React automatically re-renders that component to show the new data on the screen.

---

## 1. The `useState` Hook

To use state in a functional component, we use a special function called a "Hook" named `useState`.

### Syntax Example:

```javascript
import { useState } from "react";

const [count, setCount] = useState(0);
```

- `count`: The current value (the variable).
- `setCount`: The function used to update that value.
- `useState(0)`: We initialize the state with a starting value (in this case, `0`).

---

## 2. Handling Events & State Updates

In vanilla JavaScript, you used `addEventListener`. In React, you attach events directly to elements using "camelCase" names like `onClick` or `onChange`. You pass a function to these events to tell React what to do.

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### ⏳ Asynchronous Updates & Batching
When you call `setCount(count + 1)`, React does **not** update the `count` variable immediately on the next line of code. Instead, it schedules an update and triggers a re-render. If you log `count` immediately after setting it, you will see the **old** value:

```javascript
import { useState } from "react";

function ClickTracker() {
  const [count, setCount] = useState(0);
  
  const handleClick = () => {
    setCount(count + 1);
    console.log(count); // ❌ Still prints 0!
  };

  return <button onClick={handleClick}>Count: {count}</button>;
}
```

### 🔄 The Functional Updater Pattern
If you need to update state based on its **previous value**, you should pass a callback function to the state setter instead of a raw value. This guarantees you are using the most up-to-date state.
```javascript
// Do this:
setCount(prevCount => prevCount + 1);
```

---

## 3. Conditional Rendering

Sometimes you only want to show a component if a certain condition is true (e.g., showing a "Logout" button only if the user is logged in).

You can use the logical AND (`&&`) operator or the ternary operator (`? :`) directly inside your JSX:

```javascript
import { useState } from "react";

function WelcomeMessage() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  return (
    <div>
      {isLoggedIn ? (
        <div>
          <h1>Welcome back!</h1>
          <button onClick={() => setIsLoggedIn(false)}>Logout</button>
        </div>
      ) : (
        <div>
          <h1>Please sign in.</h1>
          <button onClick={() => setIsLoggedIn(true)}>Login</button>
        </div>
      )}
    </div>
  );
}
```

---

## 4. Controlled Components (Forms)

In traditional HTML, input fields (like `<input>` or `<textarea>`) keep track of their own state. In React, we want our component's state to be the "single source of truth." We do this by tying the input's `value` to a state variable, and updating that state using the `onChange` event.

```javascript
import { useState } from "react";

function SearchBar() {
  const [query, setQuery] = useState("");

  return (
    <input
      type="text"
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      placeholder="Search..."
    />
  );
}
```

---

## 5. State vs. Props: The Key Difference

It is helpful to visualize the difference between these two concepts:

- **Props** are like arguments passed to a function; they are external and immutable (read-only) for the component receiving them.
- **State** is like variables declared inside a function; it is internal and fully controlled by the component itself.

---

## 6. Exercises & Projects

### 🏋️ Micro-Exercise: The Like Button

**1. Setup:**
Create a component called `LikeButton.jsx` and render it in `App.jsx`.

**2. Your Task:**
- Initialize a state called `isLiked` to `false` using `useState`.
- Render a button. If `isLiked` is true, the button text should be "❤️ Liked". If false, it should be "🤍 Like".
- Add an `onClick` event that toggles the `isLiked` value using the functional updater form and the logical NOT (`!`) operator.

**3. Expected Outcome:**
Clicking the button toggles between "🤍 Like" and "❤️ Liked" instantly.

---

## ⚠️ Common Pitfalls

1. **Direct State Mutation:**
   Never modify state variables directly. If you modify an array or object directly, React won't know the state changed and won't trigger a re-render.
   ```javascript
   // ❌ Bad: mutates state directly
   const [items, setItems] = useState([1, 2]);
   items.push(3); 
   setItems(items); // React will NOT re-render because the array reference is the same!

   //  Good: creates a new array reference
   setItems(prevItems => [...prevItems, 3]);
   ```
2. **Accessing State Immediately After Setting It:**
   Remember that state updates are asynchronous. If you set state and immediately log it, the log will show the stale value.
3. **Infinite Re-renders (Setting State in Render):**
   Calling a state setter directly in the body of a component function triggers a re-render, which calls the body again, leading to an infinite loop and app crash.
   ```javascript
   // ❌ CRASH: Infinite loop
   function BadComponent() {
     const [value, setValue] = useState(0);
     setValue(10); // Runs every render!
     return <div>{value}</div>;
   }
   ```

---

## 🧠 Brain Teasers & Concept Checks

Predict the behavior of the following snippets:

1. What will be logged to the console when the button is clicked?
   ```javascript
   const [score, setScore] = useState(0);
   const handleClick = () => {
     setScore(score + 10);
     setScore(score + 10);
   };
   ```
2. How would you rewrite the above `handleClick` to make the score increment by 20 correctly?
3. Why does this list not update on screen even though the console shows the item was added?
   ```javascript
   const [todos, setTodos] = useState(["Buy milk"]);
   const addTodo = () => {
     todos.push("Clean room");
     setTodos(todos);
   };
   ```

---

## 🚀 Stage 3 Project: The Interactive Coffee Menu

**The Goal:** Manage a numerical total that updates based on user interaction.

**1. Starter Setup:**
Create a menu items array in `App.jsx`:
```javascript
const coffeeMenu = [
  { id: "c1", name: "Espresso", price: 3 },
  { id: "c2", name: "Cappuccino", price: 4.5 },
  { id: "c3", name: "Latte", price: 5 }
];
```
Create a `MenuItem.jsx` component.

**2. Your Task:**
- In `App.jsx`, create a state variable `totalCost` initialized to `0`.
- Create a `MenuItem` component that takes `name`, `price`, and a callback function prop `onAddToOrder`.
- Inside `MenuItem`, render the item details and an "Add to Order" button. The button's `onClick` should call `onAddToOrder`.
- In `App.jsx`, map the `coffeeMenu` array to render a `<MenuItem />` for each item.
- Pass a function to `onAddToOrder` that adds the item's price to `totalCost` using the functional updater form: `setTotalCost(prev => prev + price)`.
- Display the `totalCost` at the bottom of the page (e.g., `Total Cost: $X.XX`).

**3. Expected Outcome:**
An interactive menu showing three coffees. Clicking "Add to Order" on any coffee immediately updates the running total displayed at the bottom of the page.
