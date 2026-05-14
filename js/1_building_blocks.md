# Stage 1: The Building Blocks of JavaScript

Welcome to the first stage of your JavaScript journey! In this module, we are focusing on the absolute fundamentals: how a computer "remembers" things and how it manipulates basic information.

By the end of this stage, you will understand how to store data, check its type, combine text, do basic math, and compare values.

---

## 0. The Basics: Console & Comments

Before we write code, you need to know how to see the results and take notes:

- **`console.log()`**: Your megaphone. It prints whatever is inside the parentheses to your screen so you can see what your code is doing.
- **`// Comments`**: JavaScript ignores anything after `//` on a line. Use them to leave notes for yourself!

---

## 1. Variables (`let` vs `const`)

Think of variables as labeled boxes where you can store information. In modern JavaScript, we use two main keywords to create these boxes: `let` and `const`.

- **`let`**: A box whose contents _can_ change later. Use this for values that will update (like a score in a game).
- **`const`**: A box that is sealed shut once you put something in it. Its contents _cannot_ change. Use this for values that should remain constant (like your birth year).

### Syntax Example:

```javascript
let currentScore = 0;
currentScore = 10; // This is fine! We used 'let'.

const myName = "Alex";
myName = "Sam"; // ERROR! You cannot reassign a 'const'.
```

> **Pro-Tip: Naming Rules**
> Variable names cannot contain spaces. By convention, JavaScript uses **camelCase** (e.g., `currentScore`, `hasDriverLicense`).

### 🏋️ Micro-Exercise: The Swap

Create two variables, `a = 5` and `b = 10`. Write the code to swap their values so `a` becomes 10 and `b` becomes 5, without just typing `a = 10` and `b = 5`.
_(Hint: You might need a temporary third "box" to hold one of the values while you swap them!)_

---

## 2. Data Types

Now that we have boxes (variables), what can we put inside them? In JavaScript, there are three primary "primitive" data types you will use every day:

1.  **Strings:** Text. Always wrapped in quotes (single `'...'` or double `"..."`).
2.  **Numbers:** Mathematical numbers (both whole numbers and decimals). No quotes!
3.  **Booleans:** True or False. That's it. Used for making decisions later.
4.  **Undefined / Null:** The "empty" types. `undefined` means a variable was created but has no value yet. `null` is when you _intentionally_ set a box to be completely empty.

You can use the built-in `typeof` operator to ask JavaScript what type of data is inside a variable.

### Syntax Example:

```javascript
let greeting = "Hello there!"; // String
let temperature = 72.5; // Number
let isRaining = false; // Boolean

console.log(typeof temperature); // Logs: "number"
```

### 🏋️ Micro-Exercise: The Inspector

Create three variables: a string, a number, and a boolean. Use `typeof` wrapped in a `console.log()` to check the data type of each and print it to your console.

---

## 3. Template Literals

Often, you will need to combine strings together, or insert a variable _inside_ a string. In the old days, we used the `+` symbol (e.g., `"Hello " + name + "!"`). Now, we use **Template Literals**.

Template literals use **backticks** (`` ` ``) instead of normal quotes. To inject a variable directly into the string, you use the `${variableName}` syntax.

### Syntax Example:

```javascript
const userName = "Jordan";
const notifications = 5;

// Using backticks to inject variables smoothly:
const message = `Welcome back, ${userName}! You have ${notifications} unread messages.`;
console.log(message);
```

### 🏋️ Micro-Exercise: The Bio

Create three variables for your `name`, `age`, and a `hobby`. Use template literals to log a single sentence: _"Hi, I'm [Name], I'm [Age] years old, and I love [Hobby]."_

---

## 4. Basic Operators

JavaScript can act as a very powerful calculator. You have access to standard mathematical operators:

- `+` (Addition)
- `-` (Subtraction)
- `*` (Multiplication)
- `/` (Division)
- `%` (Modulo / Remainder) - _This one returns the remainder of a division. (e.g., `10 % 3` is `1` because 3 goes into 10 three times with 1 left over)._

### Syntax Example:

```javascript
const totalApples = 10 + 5; // 15
const half = totalApples / 2; // 7.5

// Shorthand Assignments and Increments:
let score = 10;
score += 5; // Same as score = score + 5 (Result: 15)
score -= 2; // Same as score = score - 2 (Result: 13)
score++; // Same as score += 1 OR score = score + 1 (Result: 14)
```

### 🏋️ Micro-Exercise: The Splitter

Imagine you and your friends go out to dinner. The total bill is **$124**, and it needs to be split evenly between **3** people. Write the math to calculate how much each person pays, and log it to the console in a readable sentence using template literals.

---

## 5. Comparison Operators

Instead of doing math, these operators _compare_ values and always result in a **Boolean** (`true` or `false`). These are essential for the next lesson!

- `>` / `<` (Greater / Less than)
- `>=` / `<=` (Greater / Less than or equal to)
- `===` (Strictly equal to)
- `!==` (Not equal to)

### Syntax Example:

```javascript
console.log(10 > 5); // Logs: true
console.log("apple" === "orange"); // Logs: false
```

### 🏋️ Micro-Exercise: The Age Check

Create a variable `myAge` and set it to your age. Then, use a comparison operator to check if `myAge` is greater than or equal to `18`. Log the result to the console.

---

## 🚀 Stage 1 Project: The "Life in Weeks" Calculator

Now it's time to put all of these building blocks together into a single script.

**The Goal:** Write a program that calculates how many days, weeks, and months a person has left to live, assuming they will live to be exactly 90 years old.

**Instructions:**

1. Create a `const` variable for your `currentAge`.
2. Calculate the _years remaining_ by subtracting your age from 90.
3. Calculate the _days remaining_ (years remaining \* 365).
4. Calculate the _weeks remaining_ (years remaining \* 52).
5. Calculate the _months remaining_ (years remaining \* 12).
6. Use a template literal to log the final message to the console:
   _"You have \[x\] days, \[y\] weeks, and \[z\] months left."_
