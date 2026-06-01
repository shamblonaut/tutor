# Stage 5: Lifting State & Context API

In Stage 4, we learned how to bring data into our components from the outside world. Now, we need to learn what to do when multiple components need to share the same "memory" or state.

---

## 1. Lifting State Up

Sometimes, two components that are "siblings" need to share the same information. For example, a search bar needs to tell a list which items to show. In React, data only flows **down** (unidirectional data flow).

To share data between siblings, you must **"Lift State Up"** to their closest common parent. The parent then passes that state down to both children as props.

---

## 2. The Problem: Prop Drilling

Lifting state up works great for small apps. But what if you have a piece of state—like a "Dark Mode" theme or the logged-in user's data—that needs to be accessed by almost every component in your app?

If you lift that state to the very top (`App`), you end up having to pass it down through dozens of intermediary components that don't even use the state, just so they can pass it to the child that does. This is called **Prop Drilling**, and it makes code messy and hard to maintain.

---

## 3. The Solution: Context API

The **Context API** solves Prop Drilling by allowing you to "teleport" data directly to the components that need it, without having to pass it manually via props at every level.

**How it works (Best Practice Template):**
Instead of declaring context and consuming it separately in every file, wrap context, provider, state, and custom consumer hook in a single file:

```javascript
// ThemeContext.jsx
import { createContext, useContext, useState } from "react";

// 1. Create the Context
const ThemeContext = createContext();

// 2. Create the Provider wrapper component
export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  const toggleTheme = () => {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// 3. Create a Custom Hook to consume context cleanly
export function useTheme() {
  const context = useContext(ThemeContext);
  if (!context) {
    throw new Error("useTheme must be used within a ThemeProvider");
  }
  return context;
}
```

**Using the Provider (typically in `main.jsx` or `App.jsx`):**
```javascript
import { ThemeProvider } from "./ThemeContext";
import App from "./App";

function Root() {
  return (
    <ThemeProvider>
      <App />
    </ThemeProvider>
  );
}
```

**Using the Custom Hook in children:**
```javascript
import { useTheme } from "./ThemeContext";

function ThemedButton() {
  const { theme, toggleTheme } = useTheme();
  return (
    <button onClick={toggleTheme} className={theme}>
      Current Theme: {theme}
    </button>
  );
}
```

### ⚡ Context Re-rendering Caveat
When the `value` passed to `<ThemeContext.Provider>` changes, **all** components that consume that context (using `useTheme` or `useContext`) will re-render automatically. Keep this in mind when storing complex or highly volatile states in Context, as it can cause performance lags if large component trees are forced to re-render.

---

## 4. Exercises & Projects

### 🏋️ Micro-Exercise: The Theme Toggle

**1. Setup:**
Create a new file `ThemeContext.jsx` in your project.

**2. Your Task:**
- In `ThemeContext.jsx`, create `ThemeContext` using `createContext()`.
- Export a custom hook named `useTheme` that consumes this context.
- Create a `ThemeProvider` component that wraps its `{children}` in `ThemeContext.Provider`.
- Maintain a state variable `theme` (either "light" or "dark") inside `ThemeProvider`, along with a function `toggleTheme` to switch it.
- Wrap your top-level `App` component in your `<ThemeProvider>`.
- Create a nested child component `<ThemedButton />` that uses your custom `useTheme()` hook to read the current theme, style itself accordingly, and call `toggleTheme` when clicked.

**3. Expected Outcome:**
Clicking the themed button updates the global theme, switching the background colors of the button (or entire page) dynamically without manually passing any props.

---

## ⚠️ Common Pitfalls

1. **Forgetting to Wrap the App in the Provider:**
   If you try to call `useContext(MyContext)` in a component that isn't wrapped in `<MyContext.Provider>` higher up in the tree, it will return `undefined` (or the default value passed to `createContext`), which usually leads to errors like `Cannot read properties of undefined`.
2. **Passing a Single Value Instead of an Object:**
   If you need to pass multiple items (like a state variable and its setter), make sure to wrap them in an object:
   ```javascript
   // ❌ Bad: only one value gets passed
   <ThemeContext.Provider value={theme}>
   
   //  Good: passes both as an object
   <ThemeContext.Provider value={{ theme, setTheme }}>
   ```
3. **Putting Too Much Volatile State in Context:**
   Putting highly active states (like character inputs or mouse positions) directly in context can cause lag because every consumer component will re-render on every keystroke/pixel change.

---

## 🧠 Brain Teasers & Concept Checks

Predict the outputs or behaviors of these scenarios:

1. A component `<SettingsPanel />` consumes a `UserContext`. If `<SettingsPanel />` has a child `<LogoutButton />` that does **not** call `useContext(UserContext)`, will `<LogoutButton />` re-render when the user state changes?
2. What happens if you define a default value inside `createContext("blue")` but wrap your app in `<ThemeContext.Provider value="red">`? Which value will `useContext` return?
3. Why is prop drilling considered a problem in large-scale applications?

---

## 🚀 Stage 5 Project: The Collaborative To-Do App

**The Goal:** Master state management by sharing data between unrelated components.

**1. Starter Setup:**
Create your components directory: `TaskStats.jsx` and `TaskList.jsx` in your project.

**2. Your Task:**
- In your parent `App` component, maintain a state variable called `tasks` (an array of task objects, e.g. `{ id: 1, text: "Learn React" }`).
- Create `TaskStats` which accepts the `tasks` array as a prop and displays the count of tasks.
- Create `TaskList` which accepts the `tasks` array and a callback function `onDeleteTask`.
- Inside `TaskList`, map through the tasks, display their text, and render a "Delete" button.
- Make sure clicking the delete button triggers `onDeleteTask` with the task's unique ID.
- In `App.jsx`, implement `onDeleteTask` to filter out the deleted task from the state.
- Render both sibling components inside `App` and verify they both stay in sync.

**3. Expected Outcome:**
A to-do page layout. When you delete an item from the list in `TaskList`, the stats component (`TaskStats`) automatically updates its counter, demonstrating proper unidirectional data flow via lifted state.
