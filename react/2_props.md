# Stage 2: Props & Dynamic Data

In Stage 1, we built "static" components—they looked the same every time they were used. But a real app needs to be dynamic. Imagine a button that says "Login" in one place and "Logout" in another, or a user card that displays different names.

**Props** (short for properties) allow us to pass data into a component, making it a reusable template rather than a hard-coded block.

---

## 1. Passing the Data

Props are passed to components exactly like HTML attributes. If you have a `User` component, you can pass a name like this:

```javascript
<User name="Shaheem" />
```

Inside the component, React collects all these attributes into a single object called **props**.

```javascript
function User(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

---

## 2. Destructuring (The "Clean Code" Way)

In modern React, we rarely use `props.name`. Instead, we use **destructuring** to grab exactly what we need right inside the function parentheses. It makes the code much easier to read.

**Instead of this:**

```javascript
function Welcome(props) {
  return <h1>Welcome, {props.city}!</h1>;
}
```

**Do this:**

```javascript
function Welcome({ city }) {
  return <h1>Welcome, {city}!</h1>;
}
```

---

## 3. Passing More Than Just Strings

JSX is powerful because props aren't limited to text. You can pass numbers, booleans, arrays, or even other functions. Remember: if it's not a plain string, it **must** be wrapped in curly braces `{}`.

- **Strings:** `label="Submit"`
- **Numbers:** `price={50}`
- **Booleans:** `isAdmin={true}`
- **Arrays:** `tags={["React", "JavaScript"]}`
- **Objects:** `user={{ name: "Shaheem", age: 25 }}` (Notice the double braces: one for JSX, one for the JS object!)

---

## 4. Rendering Lists & The `key` Prop

In React, we don't use loops to generate UI; we use the JavaScript `.map()` method to transform an array of data into an array of JSX elements.

**The Rule of the Key:** Whenever you use `.map()` to render a list, the outermost element of each item **must** have a unique `key` prop. This allows React’s Virtual DOM to track which specific item changed, moved, or was deleted, making updates incredibly efficient.

```javascript
const fruits = ["Apple", "Banana", "Cherry"];

return (
  <ul>
    {fruits.map((fruit, index) => (
      <li key={index}>{fruit}</li>
    ))}
  </ul>
);
```

---

### 🏋️ Micro-Exercise: The PriceTag

**Goal:** Practice passing multiple props and using destructuring.

1. Create a component called `PriceTag`.
2. It should accept two props: `value` (a number) and `currency` (a string).
3. Inside the component, return a stylized `<span>` that displays the currency symbol and the value together (e.g., "$50").
4. In your `App` component, render three `PriceTag` components with different values.

---

> **💡 Pro-Tip: React Developer Tools**
>
> If you haven't already, install the **React Developer Tools** extension in your browser. It adds a "Components" tab to your developer tools where you can inspect your component tree and see exactly what props are being passed to each component!

---

## 🚀 Stage 2 Project: The Recipe Book (Static)

**Goal:** Use an array of data to render multiple components dynamically.

**Instructions:**

1. **The Data:** In your `App.js`, create an array of objects called `recipes`. Each object should have a `title`, `calories`, and an array of `ingredients`.
2. **The Component:** Create a `RecipeCard` component that accepts those three props.
3. **The Loop:** Inside your `App` component, use the `.map()` method (from JavaScript Stage 4!) to loop through your recipes array and return a `<RecipeCard/>` for each one.
4. **The Key:** Remember that when you loop in React, the parent element inside the `.map()` needs a unique `key` prop (usually an ID or the title).
