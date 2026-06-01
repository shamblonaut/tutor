# Stage 2: Control Flow & Decision Making

This module focuses on allowing your Java programs to make decisions and run different code based on specific conditions.

---

## 1. `if` and `else` Statements

The `if` statement executes a block of code only if its condition evaluates to `true`. You can use `else` to define a block that runs when the condition is `false`.

```java
int score = 75;

if (score >= 90) {
    System.out.println("You got an A!");
} else if (score >= 80) {
    System.out.println("You got a B!");
} else {
    System.out.println("Keep studying!");
}
```

> **Curly Braces `{ }`**
> In Java, the code block belonging to an `if` statement is enclosed in curly braces. If you only have one line of code, the braces are optional, but it's considered best practice to always include them.

### 🏋️ Micro-Exercise: The Bouncer

**1. Setup:**

```java
int age = 16;
boolean hasID = true;
```

**2. Your Task:**

- Write an `if / else` statement.
- If `age` is 18 or older AND they have an ID (`hasID`), print `"Welcome in!"`.
- Otherwise, print `"Sorry, you cannot enter."`.

*Hint: Use `&&` for AND.*

**3. Expected Console Output:**

```text
Sorry, you cannot enter.
```

---

## 2. Logical Operators

You can combine multiple conditions using logical operators:

- `&&` (AND): Returns `true` if **both** conditions are true.
- `||` (OR): Returns `true` if **at least one** condition is true.
- `!` (NOT): Flips a boolean (makes `true` into `false` and vice versa).

```java
boolean isWeekend = true;
boolean hasHomework = false;

if (isWeekend && !hasHomework) {
    System.out.println("Time to play video games!");
}
```

### 🏋️ Micro-Exercise: The Discount

**1. Setup:**

```java
boolean isMember = false;
double purchaseAmount = 150.0;
```

**2. Your Task:**

- Write an `if / else` statement.
- A user gets a discount if they are a member OR if they spend $100 or more.
- Print `"Discount Applied!"` or `"No Discount."`.

**3. Expected Console Output:**

```text
Discount Applied!
```

---

## 3. The `switch` Statement

When you have many `if / else if` conditions checking the exact value of a single variable, a `switch` statement is cleaner.

```java
int dayOfWeek = 3;

switch (dayOfWeek) {
    case 1:
        System.out.println("Monday");
        break; // Stops checking other cases
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default: // Runs if no cases match (like 'else')
        System.out.println("Another day");
}
```

### 🏋️ Micro-Exercise: The Menu

**1. Setup:**

```java
char menuOption = 'B';
```

**2. Your Task:**

- Write a `switch` statement that checks `menuOption`.
- If it's `'A'`, print `"Order: Apple"`.
- If it's `'B'`, print `"Order: Banana"`.
- If it's `'C'`, print `"Order: Cherry"`.
- Default should print `"Invalid order"`.

**3. Expected Console Output:**

```text
Order: Banana
```

---

## ⚠️ Common Pitfalls

1. **Forgetting `break` in a `switch`:**
   If you forget `break;`, Java will keep running the code in the next `case` block, even if the case doesn't match! This is called "fall-through".

2. **Single `=` vs Double `==`:**
   A single `=` assigns a value. A double `==` compares values.
   ```java
   int lives = 3;
   // if (lives = 0) { ... } // ❌ Syntax Error in Java
   if (lives == 0) { ... }   //  Correct
   ```

3. **Comparing Strings:**
   Remember from Stage 1: never use `==` for Strings. Always use `.equals()`.
   ```java
   String status = "active";
   if (status.equals("active")) {
       System.out.println("User is active");
   }
   ```

---

## 🧠 Brain Teasers & Concept Checks

1. What evaluates first in this expression: `true || false && false`? (Hint: Order of operations matters for logic too!)
2. What happens if you remove the `break;` from `case 2` in the `switch` example?
3. What is the opposite of `!(x > 5)`?

---

## 🚀 Stage 2 Project: The Grading System

**The Goal:** Write a program that takes a numerical test score and outputs a letter grade and a message.

**1. Starter Setup:**
```java
public class Main {
    public static void main(String[] args) {
        int score = 88;
        char grade;
        
        // Write your logic here
    }
}
```

**2. Your Task:**
- Use `if / else if / else` to determine the letter grade based on `score`:
  - 90 or above: 'A'
  - 80 to 89: 'B'
  - 70 to 79: 'C'
  - 60 to 69: 'D'
  - Below 60: 'F'
- Store the result in the `grade` variable.
- Use a `switch` statement on the `grade` variable to print a custom message:
  - 'A': "Excellent work!"
  - 'B': "Good job!"
  - 'C': "You passed."
  - 'D': "Needs improvement."
  - 'F': "Please see the teacher."

**3. Expected Console Output (for score 88):**
```text
Good job!
```
