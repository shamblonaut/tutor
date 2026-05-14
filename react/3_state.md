# Stage 3: State & Interactivity

Stage 2 taught us how to pass data _into_ a component using props, but props are read-only. If you want a component to "remember" that a user clicked a button or typed into a form, you need **State**.

**State** is a component's private memory. When state changes, React automatically re-renders that component to show the new data on the screen.

---

## 1. The `useState` Hook

To use state in a functional component, we use a special function called a "Hook" named `useState`.

### Syntax Example:

```javascript
const [count, setCount] = useState(0);
```

- `count`: The current value (the variable).
- `setCount`: The function used to update that value.
- `useState(0)`: We initialize the state with a starting value (in this case, `0`).

---

## 2. Handling Events

In vanilla JavaScript, you used `addEventListener`. In React, you attach events directly to elements using "camelCase" names like `onClick` or `onChange`. You pass a function to these events to tell React what to do.

### Syntax Example:

```javascript
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

---

## 3. Conditional Rendering

Sometimes you only want to show a component if a certain condition is true (e.g., showing a "Logout" button only if the user is logged in).

You can use the logical AND (`&&`) operator or the ternary operator (`? :`) directly inside your JSX:

```javascript
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

### 🏋️ Micro-Exercise: The Like Button

**Goal:** Create a component that changes its look based on state.

1. Create a component called `LikeButton`.
2. Initialize a state called `isLiked` to `false`.
3. Render a button. If `isLiked` is true, the button text should be "❤️ Liked". If false, it should be "🤍 Like".
4. Add an `onClick` event that toggles the `isLiked` value using the `!` (NOT) operator.

---

## 🚀 Stage 3 Project: The Interactive Coffee Menu

**Goal:** Manage a numerical total that updates based on user interaction.

**Instructions:**

1. **The State:** In your `App` component, create a state variable called `totalCost` initialized to `0`.
2. **The Menu Items:** Reuse your knowledge of components to create a `MenuItem` component that takes two props: `name` and `price`.
3. **The Interaction:** Pass a function from the parent (`App`) down to the `MenuItem` as a prop. When the user clicks an "Add to Order" button inside the `MenuItem`, it should trigger that function to add the item's price to the `totalCost`.
4. **Display:** Show the `totalCost` at the bottom of the page using a template literal for formatting.
