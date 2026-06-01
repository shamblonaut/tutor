# Stage 4: Methods (The Java "Functions")

This module focuses on creating reusable blocks of code called methods. In Java, all functions must live inside a Class, which is why they are called "methods".

---

## 1. What is a Method?

A method takes input, performs an action, and optionally returns an output. It prevents you from copying and pasting the same code multiple times.

```java
public class Main {
    // Defining a method
    static void sayHello() {
        System.out.println("Hello there!");
    }

    public static void main(String[] args) {
        // Calling the method
        sayHello(); 
        sayHello();
    }
}
```

> **Why `static`?**
> For now, because we are calling our methods from the `public static void main` method, our custom methods also need the `static` keyword. We will learn why in the next stage!

---

## 2. Parameters (Input)

Methods can accept data to work with. These are called **parameters**. You must define the data type for every parameter.

```java
static void greetUser(String name) {
    System.out.println("Welcome, " + name + "!");
}

public static void main(String[] args) {
    greetUser("Alex"); // Passes "Alex" to the method
}
```

### 🏋️ Micro-Exercise: The Greeter

**1. Setup:**

```java
public class Main {
    // Write your method here

    public static void main(String[] args) {
        greet("Morning", "Sam");
    }
}
```

**2. Your Task:**

- Define a `static void` method named `greet`.
- It should take two `String` parameters: `timeOfDay` and `name`.
- Inside the method, print `"Good [timeOfDay], [name]!"`.

**3. Expected Console Output:**

```text
Good Morning, Sam!
```

---

## 3. Return Values (Output)

Instead of just printing, methods can hand data back to the code that called them. To do this, change the `void` keyword to the data type you want to return, and use the `return` keyword.

```java
// This method promises to return an int
static int multiply(int a, int b) {
    return a * b; // Hands the result back
}

public static void main(String[] args) {
    int result = multiply(4, 5);
    System.out.println("The answer is: " + result);
}
```

### 🏋️ Micro-Exercise: The Doubler

**1. Setup:**

```java
public class Main {
    // Write your method here

    public static void main(String[] args) {
        int myNumber = 10;
        int doubled = doubleValue(myNumber);
        System.out.println(doubled);
    }
}
```

**2. Your Task:**

- Define a `static` method named `doubleValue` that returns an `int`.
- It should take one `int` parameter.
- It should return that parameter multiplied by `2`.

**3. Expected Console Output:**

```text
20
```

---

## 4. Variable Scope

Variables only exist inside the block of code `{ }` where they were created. This is called their **scope**. 

```java
static void doMath() {
    int secret = 42; // Only exists inside doMath
}

public static void main(String[] args) {
    // System.out.println(secret); // ❌ Error! main cannot see 'secret'
}
```

---

## ⚠️ Common Pitfalls

1. **Missing `return` Statement:**
   If your method signature says it returns an `int` (or any type other than `void`), Java will not compile if you forget the `return` keyword.

2. **Unreachable Code:**
   Any code written *after* a `return` statement inside a method will never execute and will cause a compiler error.
   ```java
   static int getNumber() {
       return 5;
       System.out.println("This will cause an error!"); // ❌
   }
   ```

3. **Type Mismatch on Return:**
   If you promise to return a `String`, you cannot return an `int`.
   ```java
   static String getName() {
       return 100; // ❌ Error: int cannot be converted to String
   }
   ```

---

## 🧠 Brain Teasers & Concept Checks

1. What keyword do you use if a method performs an action but does *not* return any data?
2. If a method is defined as `static double calculateTotal(double price, double tax)`, what data type must the caller expect to receive back?
3. True or False: Two different methods can both have a variable named `result` without causing an error.

---

## 🚀 Stage 4 Project: The Math Utility

**The Goal:** Build a program that calculates the area of different shapes using distinct methods.

**1. Starter Setup:**
```java
public class Main {
    
    // 1. Write calculateSquareArea here
    
    // 2. Write calculateRectangleArea here

    public static void main(String[] args) {
        double squareArea = calculateSquareArea(5.0);
        double rectArea = calculateRectangleArea(4.0, 6.0);
        
        System.out.println("Square Area: " + squareArea);
        System.out.println("Rectangle Area: " + rectArea);
    }
}
```

**2. Your Task:**
- Write a method `calculateSquareArea` that takes one `double` (side) and returns the area (side * side).
- Write a method `calculateRectangleArea` that takes two `double`s (length and width) and returns the area (length * width).
- Ensure both methods are `static` and return a `double`.

**3. Expected Console Output:**
```text
Square Area: 25.0
Rectangle Area: 24.0
```
