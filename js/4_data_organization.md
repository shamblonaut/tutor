# Stage 4: Data Organization

Welcome to Stage 4! So far, our variables have only held one thing at a time: one number, one string, or one boolean. But in the real world, data comes in groups. A shopping cart has _many_ items. A user profile has a name, an email, _and_ an age.

To handle complex data, JavaScript gives us two incredibly powerful tools: **Arrays** (for lists) and **Objects** (for structured data).

---

## 1. Arrays Basics

An array is simply an ordered list of items. You create an array using square brackets `[]` and separate the items with commas.

The most important thing to know about arrays is that they are **zero-indexed**. This means the first item is at position (index) `0`, not `1`!

You can add items to the end of an array using `.push()` and remove the last item using `.pop()`.

### Syntax Example:

```javascript
const colors = ["red", "blue", "green"];

console.log(colors[0]); // Logs: "red"
console.log(colors[2]); // Logs: "green"
console.log(colors.length); // Logs: 3 (The number of items)

colors.push("yellow"); // Adds "yellow" to the end
colors.pop(); // Removes the last item ("yellow")
```

### 🏋️ Micro-Exercise: The Grocery Add

Create an array called `groceries` containing 3 items (e.g., `"apples"`, `"milk"`, `"bread"`). Use `.push()` to add a 4th item to the list. Then, use `.pop()` to remove the last item. Finally, `console.log` the array and its length to see what it looks like now.

---

## 2. Object Literals

While arrays are great for simple lists, sometimes you need to group related information together. An **Object** holds data in **key-value pairs**.

You create objects using curly braces `{}`. You can access or change the data inside an object using "dot notation" (e.g., `object.key`).

### Syntax Example:

```javascript
const player = {
  username: "SpaceNinja",
  level: 42,
  isOnline: true,
};

console.log(player.username); // Logs: "SpaceNinja"

// Changing a value:
player.level = 43;

// Adding a brand new property:
player.score = 1000;

console.log(`Player leveled up to ${player.level}!`);
```

> **Pro-Tip: Const & Mutability**
>
> You'll notice we used `const` for these arrays and objects. Even though `const` means you can't _reassign_ the variable name to something else, you **can** still change the contents inside the array or object. In JavaScript, most developers use `const` for all their arrays and objects!

### 🏋️ Micro-Exercise: The Smartphone

Create an object called `phone` with three properties: `brand` (string), `model` (string), and `is5G` (boolean). After creating the object, use dot notation to change the `model` property to something else. Log the updated `phone` object to the console.

---

## 3. Array Iteration (`.forEach()` & `.map()`)

In Stage 2, we used a `for` loop to repeat code. But looping through an array is so common that JavaScript gives us special, built-in array methods to make it easier.

- `.forEach()`: Runs a function on _every single item_ in the array.
- `.map()`: Runs a function on every item and **returns a brand new array** with the transformed items.

### Syntax Example:

```javascript
const prices = [10, 20, 30];

// Using forEach just to log items:
prices.forEach((price) => {
  console.log(`The item costs $${price}`);
});

// Using map to create a new array with tax added:
const pricesWithTax = prices.map((price) => {
  return price * 1.1;
});
console.log(pricesWithTax); // [11, 22, 33]
```

### 🏋️ Micro-Exercise: The Uppercaser

Create an array of three lowercase names (e.g., `["alice", "bob", "charlie"]`). Use `.forEach()` or `.map()` to loop through the array and `console.log` each name in ALL CAPS. _(Hint: You can use `.toUpperCase()` on a string)._

---

## 4. Filtering Data (`.filter()`)

What if you have a massive list of data and you only want to keep some of it? The `.filter()` method loops through an array and creates a **new array** containing only the items that pass a specific test (where your function returns `true`).

### Syntax Example:

```javascript
const ages = [12, 18, 25, 8, 30];

const adults = ages.filter((age) => age >= 18);

console.log(adults); // Logs: [18, 25, 30]
```

### 🏋️ Micro-Exercise: The Score Filter

Given an array `testScores` (`[55, 80, 92, 65, 78, 45, 99]`), use `.filter()` to create a new array called `passingScores` that contains only the scores strictly greater than `70`. Log `passingScores` to the console.

---

## 5. Power Tools: Destructuring & Spread

As you work with more data, you'll want faster ways to "unpack" it.

### Destructuring (Unpacking)

Destructuring allows you to pull properties out of an object (or items out of an array) and save them into variables in one line.

```javascript
const user = { name: "Alex", age: 25, city: "London" };

// Instead of user.name, user.age...
const { name, age } = user;

console.log(name); // "Alex"
console.log(age); // 25
```

### The Spread Operator (`...`)

The spread operator allows you to "spread" the contents of an array or object into a new one. This is perfect for making copies or combining data.

```javascript
const fruits = ["apple", "banana"];
const moreFruits = [...fruits, "cherry"]; // ["apple", "banana", "cherry"]

const baseSettings = { theme: "dark", notifications: true };
const userSettings = { ...baseSettings, theme: "light" }; // theme is now "light"
```

---

## 🚀 Stage 4 Project: A "Library" Management System

Now we are going to combine Arrays, Objects, and Array Methods to build a mini-database!

**The Goal:** Create a system to manage a personal book collection. You will store the books as an array of objects and write functions to interact with that array.

**Instructions:**

1.  **The Database:** Create an array called `library`. Inside this array, put 3 objects. Each object should represent a book and have three properties: `title` (string), `author` (string), and `isRead` (boolean).
2.  **The Adder:** Write a function called `addBook(title, author)`. This function should create a new book object (defaulting `isRead` to `false`) and `.push()` it into your `library` array.
3.  **The Searcher:** Write a function called `searchByAuthor(authorName)`. This function should use `.filter()` to return a new array of books written by that specific author.
4.  **The To-Do List:** Write a function called `getUnreadBooks()`. This function should use `.filter()` to return all books where `isRead` is `false`.

**Test your system:**

- Call `addBook("The Hobbit", "J.R.R. Tolkien")`.
- Log your `library` array to make sure it was added.
- Call `getUnreadBooks()` and log the result to see what you still need to read!
