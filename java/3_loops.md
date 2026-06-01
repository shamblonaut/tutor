# Stage 3: Loops & Iteration

This module covers how to repeat blocks of code efficiently using loops.

---

## 1. The `while` Loop

A `while` loop repeats a block of code as long as a condition remains `true`. It checks the condition **before** each run.

```java
int count = 0;

while (count < 3) {
    System.out.println("Count is: " + count);
    count++; // Don't forget this, or the loop will run forever!
}
```

### 🏋️ Micro-Exercise: The Countdown

**1. Setup:**

```java
int timer = 5;
```

**2. Your Task:**

- Write a `while` loop that runs as long as `timer` is greater than `0`.
- Inside the loop, print the `timer` and then decrease it by `1`.
- After the loop finishes, print `"Blast off!"`.

**3. Expected Console Output:**

```text
5
4
3
2
1
Blast off!
```

---

## 2. The `do-while` Loop

A `do-while` loop is similar to a `while` loop, but it checks the condition **after** the code runs. This guarantees the code will execute at least once, even if the condition is false initially.

```java
int attempts = 0;

do {
    System.out.println("Trying to connect...");
    attempts++;
} while (attempts < 0); // Condition is false, but code ran once!
```

---

## 3. The `for` Loop

A `for` loop is ideal when you know exactly how many times you want to iterate. It combines the initialization, condition, and update into one line.

```java
// for (initialization; condition; update)
for (int i = 0; i < 5; i++) {
    System.out.println("Iteration: " + i);
}
```

### 🏋️ Micro-Exercise: The Evens

**1. Setup:**
No variables to start!

**2. Your Task:**

- Write a `for` loop that starts at `2` and goes up to `10` (inclusive).
- Make the loop increment by `2` each time.
- Print the number inside the loop.

**3. Expected Console Output:**

```text
2
4
6
8
10
```

---

## 4. Breaking and Continuing

You can alter the normal flow of a loop using two keywords:

- **`break`**: Instantly exits the entire loop.
- **`continue`**: Skips the rest of the current iteration and jumps to the next one.

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue; // Skips printing 3
    }
    System.out.println(i);
}
```

### 🏋️ Micro-Exercise: The Search

**1. Setup:**

```java
int target = 7;
```

**2. Your Task:**

- Write a `for` loop from `1` to `10`.
- Inside the loop, check if the loop variable equals `target`.
- If it does, print `"Found it!"` and `break` out of the loop.
- If it doesn't, print `"Checking " + i`.

**3. Expected Console Output:**

```text
Checking 1
Checking 2
Checking 3
Checking 4
Checking 5
Checking 6
Found it!
```

---

## ⚠️ Common Pitfalls

1. **Infinite Loops:**
   If you forget to update your variable inside a `while` loop, the condition will never become false, freezing your program.
   ```java
   int x = 0;
   while (x < 5) {
       System.out.println("Help!");
       // Missing x++; here causes an infinite loop
   }
   ```

2. **Off-by-One Errors:**
   Be careful with `<` versus `<=`. If you want to run a loop 5 times, `for(int i = 0; i < 5; i++)` is standard. If you use `<= 5`, it will run 6 times.

3. **Scoping:**
   If you declare a variable inside a `for` loop (like `int i`), it cannot be used outside of that loop!

---

## 🧠 Brain Teasers & Concept Checks

1. Which loop (`while` or `for`) would you use if you need to ask a user for a password until they get it right?
2. What will this code print?
   ```java
   for (int i = 0; i < 3; i++) {
       for (int j = 0; j < 2; j++) {
           System.out.println(i + " " + j);
       }
   }
   ```

---

## 🚀 Stage 3 Project: The FizzBuzz Challenge

**The Goal:** Write the classic "FizzBuzz" algorithm. It's a common interview question that tests loops and logic.

**1. Starter Setup:**
```java
public class Main {
    public static void main(String[] args) {
        // Write your loop here
    }
}
```

**2. Your Task:**
- Write a `for` loop that goes from `1` to `15` (inclusive).
- Inside the loop:
  - If the number is divisible by both `3` AND `5`, print `"FizzBuzz"`.
  - If the number is divisible only by `3`, print `"Fizz"`.
  - If the number is divisible only by `5`, print `"Buzz"`.
  - Otherwise, print the number itself.
*(Hint: Use the modulo operator `%` to check for divisibility. `x % 3 == 0` means `x` is divisible by 3).*

**3. Expected Console Output:**
```text
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
```
