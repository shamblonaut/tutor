# Stage 3: Functional Foundations

This module covers functions: creating blocks of reusable code, managing inputs and outputs, and understanding scopes.

---

## 1. Function Declaration & Parameters

Create a reusable recipe of code. Define it once, then execute (call) it whenever needed.

- **Parameters:** Placeholders inside the function definition.
- **Arguments:** Actual values passed to the function when calling it.

```javascript
// Definition (filling is a parameter)
function makeSandwich(filling) {
  console.log(`Putting ${filling} between two slices of bread.`);
}

// Execution ("turkey" is an argument)
makeSandwich("turkey");
```

### 🏋️ Micro-Exercise: The Greeter

**1. Setup:**
None (declare the function directly).

**2. Your Task:**
- Write a function called `sayHello` that takes a `name` parameter.
- Inside the function, log a template literal greeting: `"Hello, [Name]!"`.
- Call your function twice: first with the argument `"Alex"`, and then with `"Sam"`.

**3. Expected Console Output:**
```text
Hello, Alex!
Hello, Sam!
```

---

## 2. Return Statements

Use the `return` keyword to hand data back to the code that called the function. A function **stops executing** immediately when it reaches a `return` statement.

```javascript
function addNumbers(num1, num2) {
  return num1 + num2; // Hands the result back
}

let myTotal = addNumbers(5, 10);
console.log(myTotal); // Logs: 15
```

### 🏋️ Micro-Exercise: The Calculator

**1. Setup:**
None (declare the function directly).

**2. Your Task:**
- Create a function called `multiply` that takes two parameters: `num1` and `num2`.
- Inside the function, **return** their product (`num1 * num2`).
- Call the function passing `3` and `5` as arguments, catch the returned value in a variable named `result`, and log `result`.

**3. Expected Console Output:**
```text
15
```

---

## 3. Arrow Functions

A shorter syntax for writing functions using the `=>` operator.

- **Standard Arrow:** `const double = (n) => { return n * 2; };`
- **Implicit Return:** If the function is a single-line expression, skip `{}` and `return` to return the value implicitly.

```javascript
// Standard Arrow
const add = (a, b) => {
  return a + b;
};

// Implicit Return Arrow
const double = (num) => num * 2;
```

### 🏋️ Micro-Exercise: The Refactor

**1. Setup:**
None.

**2. Your Task:**
- Rewrite the `multiply` function from the previous exercise as a single-line arrow function named `multiplyArrow` using an **implicit return**.
- Call it with `3` and `5`, and log the result.

**3. Expected Console Output:**
```text
15
```

---

## 4. Anonymous Functions & Callbacks

An **Anonymous Function** has no name. It is often passed directly into another function as a **Callback** to run later.

```javascript
// Passing an anonymous function into setTimeout
setTimeout(() => {
  console.log("This logs after 2 seconds!");
}, 2000);
```

---

## 5. Scope

Defines where variables can be accessed.

- **Global Scope:** Variables declared outside any function. Accessible everywhere.
- **Local (Block) Scope:** Variables declared inside a function or block `{}`. Only accessible inside that block.

```javascript
let globalName = "Alex"; // Global

function test() {
  let localName = "Sam"; // Local
  console.log(globalName); // Works!
}

// console.log(localName); // ❌ ReferenceError: localName is not defined
```

### 🏋️ Micro-Exercise: The Scope Check

**1. Setup:**
```javascript
let speedLimit = 60;
```

**2. Your Task:**
- Write a function called `checkSpeed`.
- Inside the function, create a local variable `let currentSpeed = 80;`.
- Still inside the function, log both `speedLimit` and `currentSpeed`.
- Call `checkSpeed()`.
- Outside the function, log `speedLimit`.
- Try to log `currentSpeed` outside the function and observe the error.

**3. Expected Console Output:**
```text
60 80
60
ReferenceError: currentSpeed is not defined
```

---

## ⚠️ Common Pitfalls

1.  **The Implicit Return Curly Braces Trap:**
    Adding curly braces `{}` to an arrow function turns off the implicit return. You must use the `return` keyword explicitly if braces are present!
    ```javascript
    const add = (a, b) => { a + b }; // ❌ Returns undefined!
    const add = (a, b) => a + b; //  Correct
    const add = (a, b) => { return a + b; }; //  Correct
    ```
2.  **Referencing Local Variables Globally:**
    ```javascript
    function test() {
      let x = 10;
    }
    console.log(x); // ❌ ReferenceError: x is not defined (x is trapped in test's scope)
    ```
3.  **Forgetting Parentheses to Execute:**
    ```javascript
    function greet() {
      return "Hi!";
    }
    console.log(greet); // ❌ Logs the function definition itself, not the return value.
    console.log(greet()); //  Logs "Hi!"
    ```

---

## 🧠 Brain Teasers & Concept Checks

Predict the outputs of the following code snippets:

1.  What does this output?
    ```javascript
    const value = () => 5;
    console.log(value() + 5);
    ```
2.  What does this output?
    ```javascript
    let x = 5;
    function printX() {
      let x = 10;
      console.log(x); // (Note: Variable Shadowing warning: avoid this in clean code)
    }
    printX();
    ```
3.  What happens here?
    ```javascript
    const sayHi = () => {
      console.log("Hi");
      return "Hello";
      console.log("Bye"); // Will this run?
    };
    sayHi();
    ```

---

## 🚀 Stage 3 Project: The Personal Finance Assistant

Build three functions that help with monthly budgeting.

**1. Starter Setup:**
```javascript
const annualSalary = 60000;
const savingsPercentage = 0.20; // 20%
const laptopBasePrice = 1200;
const salesTaxRate = 0.08; // 8%
```

**2. Your Task:**
1.  **Income Calculator:** Write an arrow function `calculateMonthlyIncome` that takes `annualSalary` as a parameter and returns the monthly income (salary divided by 12).
2.  **Savings Goal:** Write an arrow function `calculateSavings` that takes `monthlyIncome` and `savingsPercentage` as parameters and returns the amount to save.
3.  **Tax Applier:** Write an arrow function `applyTax` that takes `expenseAmount` and `taxRate` as parameters and returns the total cost including tax: `expenseAmount * (1 + taxRate)`.
4.  **Integration:**
    - Call `calculateMonthlyIncome(annualSalary)` and save it in a variable named `monthlyIncome`.
    - Call `calculateSavings(monthlyIncome, savingsPercentage)` and save it in a variable named `savingsGoal`.
    - Call `applyTax(laptopBasePrice, salesTaxRate)` and save it in a variable named `laptopTotalPrice`.
    - Log a summary displaying these calculated values using a template literal.

**3. Expected Console Output:**
```text
Monthly Income: $5000
Monthly Savings Goal (20%): $1000
Laptop Price with Tax: $1296
```
