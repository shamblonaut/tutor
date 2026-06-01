# Stage 1: The Building Blocks of Java

This module focuses on the absolute fundamentals: storing data, basic operators, and comparing values in Java.

---

## 0. The Basics: Console & Comments

- **`System.out.println()`**: Prints output to your screen and moves to the next line.
- **`// Comments`**: Ignored by Java; used for notes.

```java
System.out.println("Hello, World!"); // Prints text to the console
```

---

## 1. Variables and Static Typing

In Java, you must declare the **type** of data a variable will hold before you can use it. Once set, the variable can only ever hold that type of data.

```java
int currentScore = 0;
currentScore = 10; // Fine!

// currentScore = "Ten"; // ERROR! Cannot assign a String to an int.
```

> **Naming Rule (camelCase)**
> Variable names cannot have spaces. By convention, use camelCase (e.g., `currentScore`, `hasDriverLicense`).

### 🏋️ Micro-Exercise: The Swap

**1. Setup:**

```java
int a = 5;
int b = 10;
```

**2. Your Task:**

- Create a temporary variable named `temp` and store the value of `a` in it.
- Assign the value of `b` to `a`.
- Assign the value of `temp` to `b`.
- Log the values of `a` and `b` using `System.out.println()`.

**3. Expected Console Output:**

```text
a is now 10, b is now 5
```

---

## 2. Core Primitive Data Types

Java has several primitive data types. Here are the four most common ones:

1. **`int`**: Whole numbers (integers).
2. **`double`**: Numbers with decimals.
3. **`boolean`**: `true` or `false`.
4. **`char`**: A single character, wrapped in single quotes (`'A'`).

*Note: Text is represented by `String`, which is an Object, not a primitive! Strings must use double quotes (`"..."`).*

```java
String greeting = "Hello there!"; // String (Object)
double temperature = 72.5;        // double
boolean isRaining = false;        // boolean
char grade = 'A';                 // char
```

### 🏋️ Micro-Exercise: The Profile

**1. Setup:**
Imagine you are building a user profile.

**2. Your Task:**
- Declare a `String` for the user's name.
- Declare an `int` for their age.
- Declare a `boolean` for whether they are an active user.
- Print them out on separate lines.

**3. Expected Console Output:**

```text
Name: Alex
Age: 25
Active: true
```

---

## 3. String Concatenation

You can combine strings and variables using the `+` operator. 

```java
String userName = "Jordan";
int notifications = 5;

String message = "Welcome back, " + userName + "! You have " + notifications + " unread messages.";
System.out.println(message);
```

### 🏋️ Micro-Exercise: The Bio

**1. Setup:**

```java
String name = "Alex";
int age = 25;
String hobby = "coding";
```

**2. Your Task:**

- Combine these variables into a single sentence and print it.

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

```java
int score = 10;
score += 5; // score = 15
score--;    // score = 14
```

### 🏋️ Micro-Exercise: The Splitter

**1. Setup:**

```java
double totalBill = 124.0;
int people = 3;
```

**2. Your Task:**

- Create a `double` variable `amountPerPerson` and calculate the split cost.
- Log the result in a readable sentence.

**3. Expected Console Output:**

```text
Each person pays 41.333333333333336.
```

---

## 5. Comparison Operators

Compare two values and return a **boolean** (`true` or `false`):

- `>` / `<` (Greater / Less than)
- `>=` / `<=` (Greater / Less than or equal to)
- `==` (Equal to)
- `!=` (Not equal to)

```java
System.out.println(10 > 5); // true
```

### 🏋️ Micro-Exercise: The Age Check

**1. Setup:**

```java
int myAge = 20;
```

**2. Your Task:**

- Use a comparison operator to check if `myAge` is greater than or equal to `18`.
- Print the result directly.

**3. Expected Console Output:**

```text
true
```

---

## ⚠️ Common Pitfalls

1. **Missing Semicolons:**
   Every statement in Java must end with a semicolon (`;`).
   ```java
   int age = 30 // ❌ Syntax Error
   int age = 30; // Correct
   ```

2. **Comparing Strings with `==`:**
   In Java, `==` on objects compares their memory addresses, not their contents! Use `.equals()` to compare the text of Strings.
   ```java
   String word = new String("apple");
   System.out.println(word == "apple");      // ❌ Might be false!
   System.out.println(word.equals("apple")); //  Correct (true)
   ```

3. **Integer Division:**
   If you divide two integers, Java truncates the decimal.
   ```java
   System.out.println(5 / 2); // Logs "2", not 2.5!
   System.out.println(5.0 / 2); // Logs "2.5"
   ```

---

## 🧠 Brain Teasers & Concept Checks

Test your knowledge before moving to the project. Try to predict the outputs:

1. What does `System.out.println(17 % 5);` print?
2. Why does `System.out.println(10 / 4);` print `2`?
3. What is the output of this code?
   ```java
   int score = 100;
   score++;
   System.out.println(score);
   ```

---

## 🚀 Stage 1 Project: Next Century Countdown

Now it's time to put all of these building blocks together.

**The Goal:** Write a program that calculates how many days, weeks, and months are left until we reach the next century (the year 2100).

**1. Starter Setup:**
```java
public class Main {
    public static void main(String[] args) {
        int currentYear = 2026;
        int targetYear = 2100;
        
        // Write your code here!
    }
}
```

**2. Your Task:**
- Calculate the number of remaining years by subtracting `currentYear` from `targetYear`. Store this in a variable.
- Calculate the remaining days (remaining years multiplied by `365`). Store this in a variable.
- Calculate the remaining weeks (remaining years multiplied by `52`). Store this in a variable.
- Calculate the remaining months (remaining years multiplied by `12`). Store this in a variable.
- Print the final message to the console.

**3. Expected Console Output:**
```text
There are 27010 days, 3848 weeks, and 888 months left until the next century!
```
