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

You can also assign **default values** inside the destructured arguments in case the prop isn't passed down.

**Instead of this:**

```javascript
function Welcome(props) {
  return <h1>Welcome, {props.city}!</h1>;
}
```

**Do this:**

```javascript
function Welcome({ city = "our website" }) {
  return <h1>Welcome to {city}!</h1>;
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

> **⚠️ The Index Key Anti-Pattern**
> Avoid using the array `index` as a key (e.g., `key={index}`). If the list order changes, items are deleted, or new items are inserted, React will mismatch the keys with the DOM elements. This can lead to visual bugs and state conflicts. Always use a stable, unique ID (like a database ID or an item's unique slug) if possible.

```javascript
const fruits = [
  { id: 1, name: "Apple" },
  { id: 2, name: "Banana" },
  { id: 3, name: "Cherry" }
];

return (
  <ul>
    {fruits.map((fruit) => (
      <li key={fruit.id}>{fruit.name}</li>
    ))}
  </ul>
);
```

---

## 5. Exercises & Projects

### 🏋️ Micro-Exercise: The PriceTag

**1. Setup:**
Create a new file called `PriceTag.jsx` and import it into your `App.jsx` component.

**2. Your Task:**
- Create a component called `PriceTag`.
- It should accept two props: `value` (a number) and `currency` (a string, with a default value of `"$"`).
- Inside the component, return a stylized `<span>` that displays the currency symbol and the value together (e.g., "$50").
- In your `App` component, render three `PriceTag` components with different values (e.g., `50`, `100`, `15`) and verify default currency values.

**3. Expected Outcome:**
Three formatted price tags rendered side-by-side or stacked on the page, using the appropriate currency symbol.

---

> **💡 Pro-Tip: React Developer Tools**
>
> If you haven't already, install the **React Developer Tools** extension in your browser. It adds a "Components" tab to your developer tools where you can inspect your component tree and see exactly what props are being passed to each component!

---

## ⚠️ Common Pitfalls

1. **Mutating Props Directly:**
   Props are strictly **read-only**. A component must never modify its own props.
   ```javascript
   // ❌ ERROR! Props are read-only.
   function Profile({ name }) {
     name = name.toUpperCase(); // Mutating a prop
     return <h2>{name}</h2>;
   }
   ```
2. **Missing brackets `{}` for non-string values:**
   Passing numerical or boolean values without curly braces treats them as plain strings.
   ```javascript
   // ❌ Treated as string "50" and string "true"
   <Product price="50" inStock="true" />

   //  Passed as number 50 and boolean true
   <Product price={50} inStock={true} />
   ```
3. **Omitting the `key` prop inside list mapping:**
   If you forget to include a unique key inside a loop or `.map()`, React will output a console warning: `Warning: Each child in a list should have a unique "key" prop.`

---

## 🧠 Brain Teasers & Concept Checks

Predict the output or behavior of the following code snippets:

1. What will this render?
   ```javascript
   function Button({ text = "Click me" }) {
     return <button>{text}</button>;
   }
   
   // Inside App:
   <Button />
   ```
2. Why is the key prop necessary when rendering list arrays? What happens if you reorder list elements using `key={index}`?
3. What is wrong with this component?
   ```javascript
   function TotalPrice({ price, tax }) {
     props.price = price + tax;
     return <h2>Total: {props.price}</h2>;
   }
   ```

---

## 🚀 Stage 2 Project: The Recipe Book (Static)

**The Goal:** Use an array of data to render multiple components dynamically.

**1. Starter Setup:**
In your `App.jsx`, define an array of objects called `recipes`.
```javascript
const recipes = [
  { id: "r1", title: "Spaghetti Carbonara", calories: 650, ingredients: ["Pasta", "Egg", "Pecorino", "Guanciale"] },
  { id: "r2", title: "Chicken Caesar Salad", calories: 400, ingredients: ["Chicken", "Lettuce", "Croutons", "Caesar Dressing"] }
];
```
Create a new file `RecipeCard.jsx`.

**2. Your Task:**
- Create a `RecipeCard` component that accepts three props: `title`, `calories`, and `ingredients` (an array).
- Inside `RecipeCard`, display the title, calories, and map the ingredients array into a nested `<ul>` list with a key for each ingredient.
- Inside your `App` component, use the `.map()` method to loop through the `recipes` array and render a `<RecipeCard />` for each.
- Ensure the `<RecipeCard />` inside the loop gets a unique `key` prop using the recipe's unique `id`.

**3. Expected Outcome:**
A layout on the page displaying card sections for each recipe, showing their title, calories, and ingredients mapped as a sub-list, with no unique key console warnings.
