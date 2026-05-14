# Stage 3: Functional Foundations

Welcome to Stage 3! Up until now, we've written code that runs once and is done. But what if you want to run the same logic multiple times without copy-pasting it?

Enter **Functions**. Functions are like recipes. You write the instructions once, and then you can "cook" that recipe whenever you want, even swapping out the ingredients (data) each time. This is how we keep our code clean, organized, and reusable.

---

## 1. Function Declaration & Parameters

To create a function, you declare it, name it, and define what it does inside curly braces `{}`. To use it, you "call" it by its name followed by parentheses `()`.

Functions can also accept inputs, called **parameters**. Think of parameters as empty variables waiting to be filled when the function is called.

> **Note:** You'll also hear the term **arguments**. Parameters are the "labels" in the recipe, while Arguments are the actual ingredients you pass in.

### Syntax Example:

```javascript
// Defining the function (the recipe)
function makeSandwich(filling) {
  console.log(`Putting ${filling} between two slices of bread.`);
}

// Calling the function (cooking the recipe)
makeSandwich("peanut butter");
makeSandwich("turkey");
```

### 🏋️ Micro-Exercise: The Greeter

Write a function called `sayHello` that takes a `name` as a parameter. Inside the function, `console.log` a greeting like `"Hello, [Name]!"`. Call your function three times with three different names to see it in action.

---

## 2. Return Statements

`console.log()` is great for us humans to see what's happening, but it doesn't give the data back to the computer to use later. To get data _out_ of a function, we use the `return` keyword.

When a function hits a `return` statement, it immediately stops running and spits that value out.

### Syntax Example:

```javascript
function addNumbers(num1, num2) {
  let sum = num1 + num2;
  return sum; // Hands the result back to the program
}

// We can catch the returned value in a new variable:
let myTotal = addNumbers(5, 10);
console.log(`The total is ${myTotal}`); // Logs: The total is 15
```

### 🏋️ Micro-Exercise: The Calculator

Create a function called `multiply` that takes two numbers as parameters and **returns** their product. Outside the function, create a new variable to "catch" the returned result, and then log that variable to the console.

---

## 3. Arrow Functions

In modern JavaScript, there is a shorter, sleeker way to write functions called **Arrow Functions**. They do exactly the same thing but use an arrow `=>` instead of the `function` keyword.

If your function only has one line of code that returns something, you can even skip the curly braces and the `return` keyword entirely!

### Syntax Example:

```javascript
// Old way:
function double(num) {
  return num * 2;
}

// Modern Arrow Function:
const double = (num) => {
  return num * 2;
};

// Ultra-short Arrow Function (Implicit Return):
const doubleShort = (num) => num * 2;
```

> **Watch Out: The Order Rule**
>
> You can call a regular `function` even if you write it later in your code. However, **arrow functions must be defined before you call them**, or your code will crash!

### 🏋️ Micro-Exercise: The Refactor

Take the `multiply` function you wrote in the previous exercise and rewrite it as a single-line arrow function. Test it to make sure it still works!

---

## 4. Anonymous Functions & Callbacks

An **Anonymous Function** is simply a function without a name. We often use these as "one-off" tools, especially when we pass one function into another function. This is called a **Callback**.

You will see this a lot in later stages when we talk about Arrays and the DOM.

### Syntax Example:

```javascript
// We are passing an anonymous arrow function INTO setTimeout
setTimeout(() => {
  console.log("This happened after 2 seconds!");
}, 2000);
```

---

## 5. Scope

**Scope** is the concept of where a variable "lives" and who has access to it.

- **Global Scope:** A variable created _outside_ of any function. Everyone can see it and use it.
- **Local Scope:** A variable created _inside_ a function. It is trapped inside that function. The outside world doesn't know it exists.

### Syntax Example:

```javascript
let secretBase = "The Moon"; // Global scope

function spyMission() {
  let secretCode = "007"; // Local scope
  console.log(`Mission at ${secretBase} using code ${secretCode}`);
}

spyMission();
// console.log(secretCode); // ERROR! secretCode is not defined here.
```

### 🏋️ Micro-Exercise: The Shadow

Create a global variable `let x = 100;`. Then, write a function. Inside the function, write `let x = 50;` and `console.log(x)`. Finally, `console.log(x)` _outside_ the function. Run your code to see which `x` "wins" in different places. This is called "Variable Shadowing" (local variables inside a function take priority over global ones with the same name).

---

## 🚀 Stage 3 Project: The Personal Finance Assistant

Let's build a set of functions that could be the backend for a budgeting app!

**The Goal:** Create a series of functions to calculate a monthly budget, determine a savings goal, and apply a tax to specific expenses.

**Instructions:**

1.  **The Income Calculator:** Write an arrow function called `calculateMonthlyIncome` that takes an `annualSalary` as a parameter and **returns** the monthly income (annual divided by 12).
2.  **The Savings Goal:** Write a function called `calculateSavings` that takes `monthlyIncome` and a `savingsPercentage` (e.g., 0.20 for 20%). It should **return** how much money should be saved that month.
3.  **The Tax Applier:** Write a function called `applyTax` that takes an `expenseAmount` and a `taxRate` (e.g., 0.08 for 8%). It should **return** the total cost of the expense including tax.
4.  **Putting it together:**
    - Set up a variable for your annual salary (e.g., $60,000).
    - Call `calculateMonthlyIncome` and save the result in a variable.
    - Call `calculateSavings` using your monthly income to find out how much to save.
    - You buy a new laptop for $1,200 with an 8% tax. Call `applyTax` to find the final price.
    - Log a summary sentence using template literals showing your monthly income, your savings goal, and the final price of the laptop.
