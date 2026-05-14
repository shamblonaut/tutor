# Stage 2: Decision Making & Repetition

Welcome to Stage 2! In the previous stage, our code ran straight from top to bottom. But real programs need to be smart. They need to make choices based on different situations, and they need to automate repetitive tasks so we don't have to write the same code a hundred times.

This is where **Logic** (Conditionals) and **Repetition** (Loops) come in. These form the "brain" of your code.

---

## 1. Conditionals (`if`, `else if`, `else`)

Conditionals allow your program to ask a question and run different blocks of code depending on the answer (True or False).

- `if`: The first question you ask.
- `else if`: A follow-up question if the first one was false.
- `else`: The "catch-all" block that runs if _everything_ above was false.

### Syntax Example:

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

> **The Power of the Curly Brace `{ }`**: These define a "block" of code. Anything inside them belongs to that specific `if` or `else`. Plus, any variable created _inside_ a block stays there—it can't be used outside! (We call this "Block Scope").

### 🏋️ Micro-Exercise: The Bouncer

Write a script that checks an `age` variable. If the age is under 18, log `"Access Denied"`. If the age is 18 or older, log `"Welcome to the club!"`.

---

## 2. Logical Operators (`&&`, `||`, `!`)

Sometimes, an `if` statement needs to check multiple things at once. We use logical operators to combine conditions.

- `&&` (AND): **Both** sides must be true.
- `||` (OR): **At least one** side must be true.
- `!` (NOT): Flips a boolean (True becomes False, False becomes True).

### Syntax Example:

```javascript
let hasDriverLicense = true;
let hasCar = false;
let isRaining = false;

if (hasDriverLicense && hasCar) {
  console.log("You can drive to work!");
} else {
  console.log("You need to take the bus.");
}

if (!isRaining) {
  console.log("It's a dry day, you can walk!");
}
```

> **Pro-Tip: Truthy & Falsy**
>
> In JavaScript, you don't always have to compare things. Values like `0`, `""` (empty string), `null`, and `undefined` are automatically treated as **false**. Almost everything else is **true**!

### 🏋️ Micro-Exercise: The Security Gate

Create two variables: `hasTicket = true` and `isSober = true`. Write an `if` statement that checks both conditions. Only log `"Enter the venue"` if **both** are true. Test your code by changing one of them to `false`.

---

## 3. The `for` Loop

Loops are how we tell the computer to do something over and over again. A `for` loop is perfect when you know exactly _how many times_ you want the code to repeat.

It has three parts inside the parentheses, separated by semicolons:

1.  **Initialization:** Where does the loop start? (e.g., `let i = 0`)
2.  **Condition:** How long should it keep going? (e.g., `i < 5`)
3.  **Increment:** What happens after each loop? (e.g., `i++` to add 1)

### Syntax Example:

```javascript
// This will log the numbers 1, 2, 3, 4, 5
for (let i = 1; i <= 5; i++) {
  console.log(`Current number is: ${i}`);
}
```

### 🏋️ Micro-Exercise: The Multiplier

Write a `for` loop that logs the "5 Times Table". It should start at 5 and go up to 50, logging 5, 10, 15, 20... etc.
_(Hint: You can increase your counter by 5 each time using `i = i + 5` or `i += 5` instead of `i++`)_.

---

## 4. The `while` Loop

A `while` loop is used when you _don't_ know exactly how many times you need to loop, but you want to keep looping **as long as a condition is true**.

_Warning: If the condition never becomes false, you will create an "infinite loop" that crashes your browser! Always make sure something inside the loop changes the condition._

### Syntax Example:

```javascript
let energy = 3;

while (energy > 0) {
  console.log(`Running! Energy left: ${energy}`);
  energy--; // Decrease energy by 1 each time
}
console.log("Out of energy. Time to rest.");
```

### 🏋️ Micro-Exercise: The Countdown

Use a `while` loop to create a countdown timer. Start a variable at 10. Keep looping and logging the number as long as it's greater than 0. After the loop finishes, log `"Blast off!"`.

---

## 🚀 Stage 2 Project: Text-Based Battle Simulator

It's time to build a mini-game using loops and conditionals!

**The Goal:** Create a script where a "Hero" and a "Monster" fight. They will take turns attacking each other using a `while` loop until one of their health points reaches zero.

**Instructions:**

1. Create two variables: `heroHealth = 100` and `monsterHealth = 100`.
2. Set up a `while` loop that runs **as long as** both `heroHealth > 0` AND `monsterHealth > 0`.
3. Inside the loop, calculate random damage for the hero's attack (e.g., between 1 and 20). You can generate a random number using `Math.floor(Math.random() * 20) + 1`.
4. Subtract that damage from `monsterHealth` and log: _"Hero attacks! Monster health is now [X]"_.
5. Do the same for the monster's attack (calculate random damage, subtract from `heroHealth`, and log the result).
6. Outside and after the loop, write an `if/else` statement to declare the winner. If `heroHealth` is greater than 0, log _"Hero wins!"_. Otherwise, log _"Monster wins!"_.
7. **Bonus Challenge:** Did you notice the monster still attacks even if its health is 0? Try wrapping the monster's attack in an `if` statement so it only fights back if it's still alive!

_Tip: Watch the battle unfold in your console!_

> **Pro-Tip: Generating Random Numbers**
>
> `Math.random()` gives you a random decimal between 0 and 1 (like 0.45). We multiply it by 20 and use `Math.floor()` to "chop off" the decimals to get a whole number between 1 and 20!
