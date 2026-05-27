# Stage 1: The Building Blocks of JavaScript

This module focuses on the absolute fundamentals: storing data, basic operators, and comparing values.

---

## 0. The Basics: Console & Comments

- **`console.log()`**: Prints output to your screen.
- **`// Comments`**: Ignored by JavaScript; used for notes.

```javascript
console.log("Hello, World!"); // Prints text to the console
```

---

## 1. Variables (`let` vs `const`)

- **`let`**: A variable whose value **can** be reassigned.
- **`const`**: A variable whose value **cannot** be reassigned after it is set.

```javascript
let currentScore = 0;
currentScore = 10; // Fine!

const myName = "Alex";
// myName = "Sam"; // ERROR! Cannot reassign const.
```

> **Naming Rule (camelCase)**
> Variable names cannot have spaces. By convention, use camelCase (e.g., `currentScore`, `hasDriverLicense`).

### 🏋️ Micro-Exercise: The Swap

**1. Setup:**

```javascript
let a = 5;
let b = 10;
```

**2. Your Task:**

- Create a temporary variable named `temp` and store the value of `a` in it.
- Assign the value of `b` to `a`.
- Assign the value of `temp` to `b`.
- Log the values of `a` and `b` using `console.log(a, b)`.

**3. Expected Console Output:**

```text
10 5
```

---

## 2. Data Types

JavaScript has 4 core primitive data types:

1.  **Strings:** Text. Wrapped in quotes (`'...'` or `"..."`).
2.  **Numbers:** Mathematical numbers (decimals or integers). No quotes!
3.  **Booleans:** `true` or `false`.
4.  **Undefined / Null:** `undefined` means a variable is declared but empty. `null` is an intentional empty value.

Use `typeof` to check the data type:

```javascript
let greeting = "Hello there!"; // String
let temperature = 72.5; // Number
let isRaining = false; // Boolean

console.log(typeof temperature); // Logs: "number"
```

### 🏋️ Micro-Exercise: The Inspector

**1. Setup:**

```javascript
const val1 = "Hello";
const val2 = 99;
const val3 = false;
```

**2. Your Task:**

- Use the `typeof` operator inside `console.log()` to print the data type of `val1`, `val2`, and `val3`.

**3. Expected Console Output:**

```text
string
number
boolean
```

---

## 3. Template Literals

Use **backticks** (`` ` ``) instead of standard quotes to inject variables directly into a string using `${variableName}` syntax.

```javascript
const userName = "Jordan";
const notifications = 5;

// Modern Template Literal:
const message = `Welcome back, ${userName}! You have ${notifications} unread messages.`;
console.log(message);
```

### 🏋️ Micro-Exercise: The Bio

**1. Setup:**

```javascript
const name = "Alex";
const age = 25;
const hobby = "coding";
```

**2. Your Task:**

- Create a template literal using backticks (`` ` ``) and the setup variables to log a single sentence.

**3. Expected Console Output:**

```text
Hi, I'm Alex, I'm 25 years old, and I love coding.
```

---

## 4. Basic Operators

Use standard mathematical operators to calculate values:

- `+` (Addition), `-` (Subtraction), `*` (Multiplication), `/` (Division)
- `%` (Modulo / Remainder): returns remainder of division (e.g., `10 % 3` is `1`).
- `+=`, `-=`, `++`, `--` (Shorthand operators).

```javascript
let score = 10;
score += 5; // score = 15
score--; // score = 14
```

### 🏋️ Micro-Exercise: The Splitter

**1. Setup:**

```javascript
const totalBill = 124;
const people = 3;
```

**2. Your Task:**

- Create a variable `amountPerPerson` and calculate the split cost.
- Log the result in a readable sentence using a template literal.

**3. Expected Console Output:**

```text
Each person pays $41.333333333333336.
```

---

## 5. Comparison Operators

Compare two values and return a **Boolean** (`true` or `false`):

- `>` / `<` (Greater / Less than)
- `>=` / `<=` (Greater / Less than or equal to)
- `===` (Strictly equal to)
- `!==` (Not equal to)

```javascript
console.log(10 > 5); // true
console.log("apple" === "orange"); // false
```

### 🏋️ Micro-Exercise: The Age Check

**1. Setup:**

```javascript
const myAge = 20;
```

**2. Your Task:**

- Use a comparison operator to check if `myAge` is greater than or equal to `18`.
- Log the result using `console.log()`.

**3. Expected Console Output:**

```text
true
```

---

## ⚠️ Common Pitfalls

1.  **Reassigning `const`:**
    ```javascript
    const userRole = "admin";
    userRole = "editor"; // ❌ TypeError: Assignment to constant variable.
    ```
2.  **Missing String Quotes:**
    ```javascript
    let name = Alex; // ❌ ReferenceError: Alex is not defined
    let name = "Alex"; //  Correct
    ```
3.  **Mixing Numbers and Strings:**
    ```javascript
    console.log(5 + "5"); // Logs "55" (string concatenation) instead of 10.
    ```

---

## 🧠 Brain Teasers & Concept Checks

Test your knowledge before moving to the project. Try to predict the outputs:

1.  What does `console.log(17 % 5)` print?
2.  What is the type of `result` in: `let result = typeof 42;`?
3.  What does this output?
    ```javascript
    const score = 100;
    score++;
    console.log(score);
    ```

---

## 🚀 Stage 1 Project: Next Century Countdown

Now it's time to put all of these building blocks together into a single script.

**The Goal:** Write a program that calculates how many days, weeks, and months are left until we reach the next century (the year 2100).

**1. Starter Setup:**
```javascript
const currentYear = 2026;
const targetYear = 2100;
```

**2. Your Task:**
- Calculate the number of remaining years by subtracting `currentYear` from `targetYear`. Store this in a variable named `yearsRemaining`.
- Calculate the remaining days (`yearsRemaining` multiplied by `365`). Store this in a variable named `daysRemaining`.
- Calculate the remaining weeks (`yearsRemaining` multiplied by `52`). Store this in a variable named `weeksRemaining`.
- Calculate the remaining months (`yearsRemaining` multiplied by `12`). Store this in a variable named `monthsRemaining`.
- Log the final message to the console using a template literal.

**3. Expected Console Output:**
```text
There are 27010 days, 3848 weeks, and 888 months left until the next century!
```
