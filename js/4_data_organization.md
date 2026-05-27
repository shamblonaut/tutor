# Stage 4: Data Organization

This module covers grouping data: lists (Arrays) and key-value records (Objects), as well as modern methods to transform and unpack them.

---

## 1. Arrays Basics

An ordered list of items. Arrays are **zero-indexed** (first item is at index `0`).

```javascript
const colors = ["red", "blue", "green"];

console.log(colors[0]); // "red"
console.log(colors.length); // 3

colors.push("yellow"); // Adds to the end -> ["red", "blue", "green", "yellow"]
colors.pop(); // Removes last item -> ["red", "blue", "green"]
```

### 🏋️ Micro-Exercise: The Grocery Add

**1. Setup:**
```javascript
const groceries = ["milk", "bread", "eggs"];
```

**2. Your Task:**
- Use `.push()` to add `"butter"` to the end of the `groceries` array.
- Use `.pop()` to remove the last item from the array (which will be `"butter"`).
- Log the updated `groceries` array and its `.length` to the console.

**3. Expected Console Output:**
```text
[ 'milk', 'bread', 'eggs' ]
3
```

---

## 2. Object Literals

Store data in structured **key-value pairs**. Access/modify values using dot notation (`object.key`).

```javascript
const player = {
  username: "SpaceNinja",
  level: 42,
  isOnline: true,
};

console.log(player.username); // "SpaceNinja"
player.level = 43; // Modify value
player.score = 1000; // Add new property
```

> **Mutability & `const`**
> Declaring arrays and objects with `const` prevents you from *reassigning* the variable to a new array/object, but you can still freely add, remove, or modify items *inside* them.

### 🏋️ Micro-Exercise: The Smartphone

**1. Setup:**
```javascript
const phone = { brand: "Apple", model: "iPhone 13", is5G: true };
```

**2. Your Task:**
- Use dot notation to update the `model` property to `"iPhone 14"`.
- Use dot notation to add a new property named `color` and set it to `"black"`.
- Log the updated `phone` object to the console.

**3. Expected Console Output:**
```text
{ brand: 'Apple', model: 'iPhone 14', is5G: true, color: 'black' }
```

---

## 3. Array Iteration (`.forEach()` & `.map()`)

Built-in methods to loop through lists:

- **`.forEach()`**: Executes code for each item (does not return a new array).
- **`.map()`**: Runs code on each item and **returns a new array** containing the results.

```javascript
const prices = [10, 20, 30];

// Logging elements
prices.forEach((price) => console.log(`Price: $${price}`));

// Transforming elements (returns new array)
const doubled = prices.map((price) => price * 2); // [20, 40, 60]
```

### 🏋️ Micro-Exercise: The Uppercaser

**1. Setup:**
```javascript
const names = ["alice", "bob", "charlie"];
```

**2. Your Task:**
- Use `.map()` to create a new array named `uppercaseNames`.
- Inside the `.map()` callback, transform each name to ALL CAPS using the `.toUpperCase()` string method.
- Log the `uppercaseNames` array to the console.

**3. Expected Console Output:**
```text
[ 'ALICE', 'BOB', 'CHARLIE' ]
```

---

## 4. Filtering Data (`.filter()`)

Loops through an array and **returns a new array** containing only items that pass a specific test (where the callback returns `true`).

```javascript
const ages = [12, 18, 25, 8, 30];
const adults = ages.filter((age) => age >= 18); // [18, 25, 30]
```

### 🏋️ Micro-Exercise: The Score Filter

**1. Setup:**
```javascript
const testScores = [55, 80, 92, 65, 78, 45, 99];
```

**2. Your Task:**
- Use the `.filter()` method to create a new array named `passingScores`.
- Filter the `testScores` array so that only scores strictly greater than `70` are included in the new array.
- Log the `passingScores` array to the console.

**3. Expected Console Output:**
```text
[ 80, 92, 78, 99 ]
```

---

## 5. Power Tools: Destructuring & Spread

Unpack and copy data quickly.

> ⚛️ **The React Foundation**
>
> If you plan to learn **React** next, pay extra attention to this section and the array methods (`.map()` and `.filter()`) above! React uses these features constantly:
> - **`.map()`** renders lists of components.
> - **`.filter()`** deletes items from state.
> - **Destructuring** extracts props.
> - **Spread Operator (`...`)** updates state immutably.

### Destructuring (Unpacking)
```javascript
const user = { name: "Alex", age: 25 };
const { name, age } = user; // Extracts variables directly

console.log(name); // "Alex"
```

### Spread Operator (`...`)
```javascript
// Copying & extending arrays
const fruits = ["apple", "banana"];
const allFruits = [...fruits, "cherry"]; // ["apple", "banana", "cherry"]

// Copying & extending objects
const base = { theme: "dark", notify: true };
const userSettings = { ...base, theme: "light" }; // theme: "light", notify: true
```

---

## ⚠️ Common Pitfalls

1.  **Forgetting to `return` in `.map()` or `.filter()`:**
    If you use curly braces `{}` in these callbacks, you must write `return` explicitly. Otherwise, the new array will contain `undefined` (for map) or be empty (for filter).
    ```javascript
    const prices = [10, 20];
    const double = prices.map((p) => { p * 2 }); // ❌ Returns: [undefined, undefined]
    const double = prices.map((p) => p * 2); //  Returns: [20, 40]
    ```
2.  **Off-by-One Array Indexing:**
    ```javascript
    const items = ["a", "b"];
    console.log(items[items.length]); // ❌ undefined! (Last index is items.length - 1)
    ```
3.  **Reassigning a `const` Object/Array:**
    ```javascript
    const user = { name: "Alex" };
    user.name = "Sam"; //  Allowed (mutating keys inside const)
    user = { name: "Sam" }; // ❌ TypeError (cannot reassign const variable)
    ```

---

## 🧠 Brain Teasers & Concept Checks

Predict the outputs of the following snippets:

1.  What does this output?
    ```javascript
    const nums = [1, 2, 3];
    const filtered = nums.filter((n) => n > 5);
    console.log(filtered);
    ```
2.  What is logged to the console here?
    ```javascript
    const user = { username: "codeguy", active: true };
    const { username } = user;
    console.log(username);
    ```
3.  What does this print?
    ```javascript
    const arr = [1, 2];
    const newArr = [arr, 3];
    console.log(newArr); // Is it [1, 2, 3] or [ [1, 2], 3 ]?
    ```

---

## 🚀 Stage 4 Project: A "Library" Management System

Create a mini-database to manage a personal book collection.

**1. Starter Setup:**
```javascript
const library = [
  { title: "The Great Gatsby", author: "F. Scott Fitzgerald", isRead: true },
  { title: "To Kill a Mockingbird", author: "Harper Lee", isRead: false },
  { title: "1984", author: "George Orwell", isRead: false }
];
```

**2. Your Task:**
1.  **The Adder:** Write a function `addBook(title, author)` that:
    - Creates a new book object with `title`, `author`, and `isRead: false`.
    - Push this new book object into the `library` array.
2.  **The Searcher:** Write a function `searchByAuthor(authorName)` that:
    - Uses `.filter()` to find and return all books written by the given `authorName`.
3.  **The To-Do List:** Write a function `getUnreadBooks()` that:
    - Uses `.filter()` to return all books where `isRead` is `false`.
4.  **Test Your Code:**
    - Call `addBook("The Hobbit", "J.R.R. Tolkien")`.
    - Log the entire `library` array to confirm it was added.
    - Call `searchByAuthor("Harper Lee")` and log the result.
    - Call `getUnreadBooks()` and log the result.

**3. Expected Console Output:**
```text
(Logs library array including "The Hobbit" object)
[
  { title: 'The Great Gatsby', author: 'F. Scott Fitzgerald', isRead: true },
  { title: 'To Kill a Mockingbird', author: 'Harper Lee', isRead: false },
  { title: '1984', author: 'George Orwell', isRead: false },
  { title: 'The Hobbit', author: 'J.R.R. Tolkien', isRead: false }
]

(Logs search result)
[ { title: 'To Kill a Mockingbird', author: 'Harper Lee', isRead: false } ]

(Logs unread books)
[
  { title: 'To Kill a Mockingbird', author: 'Harper Lee', isRead: false },
  { title: '1984', author: 'George Orwell', isRead: false },
  { title: 'The Hobbit', author: 'J.R.R. Tolkien', isRead: false }
]
```
