# Stage 2: Decision Making & Repetition

This module covers control flow: making choices using conditionals and automating repetitive tasks using loops.

---

## 1. Conditionals (`if`, `else if`, `else`)

Control which code runs based on a condition evaluating to `true` or `false`.

```javascript
let weather = "rainy";

if (weather === "sunny") {
  console.log("Wear sunglasses!");
} else if (weather === "rainy") {
  console.log("Grab an umbrella!");
} else {
  console.log("Just wear a jacket.");
}
```

> **Block Scope `{ }`**
> Variables created inside `{}` braces are locked inside that block and cannot be accessed outside.

### 🏋️ Micro-Exercise: The Bouncer

**1. Setup:**
```javascript
const age = 16;
```

**2. Your Task:**
- Write an `if/else` statement.
- If `age` is 18 or older, log `"Welcome to the club!"`.
- Otherwise (if under 18), log `"Access Denied"`.

**3. Expected Console Output:**
```text
Access Denied
```

---

## 2. Logical Operators (`&&`, `||`, `!`)

Combine multiple conditions:

- `&&` (AND): Both conditions must be `true`.
- `||` (OR): At least one condition must be `true`.
- `!` (NOT): Flips the boolean value (e.g., `!true` is `false`).

```javascript
let hasDriverLicense = true;
let hasCar = false;

if (hasDriverLicense && hasCar) {
  console.log("You can drive to work!");
} else {
  console.log("You need to take the bus.");
}
```

> **Truthy & Falsy**
> In conditional checks, JavaScript automatically treats `0`, `""` (empty string), `null`, `undefined`, and `NaN` as `false` (Falsy). All other values are treated as `true` (Truthy).

### 🏋️ Micro-Exercise: The Security Gate

**1. Setup:**
```javascript
const hasTicket = true;
const isSober = false;
```

**2. Your Task:**
- Write an `if/else` statement using the `&&` operator.
- Only log `"Enter the venue"` if both `hasTicket` and `isSober` are true.
- Otherwise, log `"Access Denied"`.

**3. Expected Console Output:**
```text
Access Denied
```

---

## 3. The `for` Loop

Repeats code a specific number of times.

- **Structure:** `for (initialization; condition; increment)`

```javascript
// Logs: 1, 2, 3, 4, 5
for (let i = 1; i <= 5; i++) {
  console.log(`Current number is: ${i}`);
}
```

### 🏋️ Micro-Exercise: The Multiplier

**1. Setup:**
None (start the loop directly).

**2. Your Task:**
- Write a `for` loop that starts at 5, ends at 50, and increments by 5 each iteration (`i += 5`).
- Log the current value of `i` inside the loop.

**3. Expected Console Output:**
```text
5
10
15
20
25
30
35
40
45
50
```

---

## 4. The `while` Loop

Repeats code as long as a condition remains `true`. Use this when you do not know the exact number of iterations beforehand.

```javascript
let energy = 3;

while (energy > 0) {
  console.log(`Running! Energy left: ${energy}`);
  energy--; // Modify the condition to avoid an infinite loop!
}
```

### 🏋️ Micro-Exercise: The Countdown

**1. Setup:**
```javascript
let count = 10;
```

**2. Your Task:**
- Write a `while` loop that logs the value of `count` as long as `count` is greater than 0.
- Make sure to decrement `count` by 1 inside the loop to avoid an infinite loop!
- After the loop finishes (outside the loop), log `"Blast off!"`.

**3. Expected Console Output:**
```text
10
9
8
7
6
5
4
3
2
1
Blast off!
```

---

## ⚠️ Common Pitfalls

1.  **Using `=` Instead of `===`:**
    ```javascript
    let score = 0;
    if (score = 10) { // ❌ Assignment instead of comparison! Always returns truthy (10).
      console.log("You won!");
    }
    ```
2.  **Infinite Loops:**
    ```javascript
    let count = 1;
    while (count <= 5) {
      console.log(count);
      // ❌ Forgot count++! This runs forever and crashes the browser.
    }
    ```

---

## 🧠 Brain Teasers & Concept Checks

Try to predict the outputs of these snippets:

1.  What does this output?
    ```javascript
    let score = 0;
    if (score) {
      console.log("Game started!");
    } else {
      console.log("No score.");
    }
    ```
2.  What does this print?
    ```javascript
    let x = true;
    let y = false;
    console.log(!x || y);
    ```
3.  How many times does this loop run?
    ```javascript
    for (let i = 0; i < 3; i++) {
      console.log("Hello");
    }
    ```

---

## 🚀 Stage 2 Project: Text-Based Battle Simulator

Create a script where a "Hero" and a "Monster" fight using a loop until one of their health points reaches zero.

**1. Starter Setup:**
```javascript
let heroHealth = 100;
let monsterHealth = 100;
```

**2. Your Task:**
- Set up a `while` loop that continues running as long as both `heroHealth` is greater than 0 AND `monsterHealth` is greater than 0.
- Inside the loop:
  1. Calculate random damage for the Hero's attack (a random number between 1 and 20):
     `const heroDamage = Math.floor(Math.random() * 20) + 1;`
  2. Subtract `heroDamage` from `monsterHealth`.
  3. Log the action using a template literal: `"Hero hits Monster for [heroDamage] damage. Monster HP: [monsterHealth]"`.
  4. Check if the monster is still alive (`monsterHealth > 0`). If so, calculate the Monster's random attack damage (between 1 and 20):
     `const monsterDamage = Math.floor(Math.random() * 20) + 1;`
  5. Subtract `monsterDamage` from `heroHealth`.
  6. Log the action using a template literal: `"Monster hits Hero for [monsterDamage] damage. Hero HP: [heroHealth]"`.
- Outside the loop (after it ends):
  - Write an `if/else` statement checking who won. Log either `"The Hero wins!"` or `"The Monster wins!"` depending on whose health is greater than 0.

**3. Expected Console Output (Example Run):**
```text
Hero hits Monster for 12 damage. Monster HP: 88
Monster hits Hero for 5 damage. Hero HP: 95
Hero hits Monster for 18 damage. Monster HP: 70
...
Hero hits Monster for 15 damage. Monster HP: -5
The Hero wins!
```
