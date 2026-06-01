# Stage 8: Abstraction & Interfaces

Sometimes, you want to create a parent class, but you *never* want anyone to instantiate it directly. You only want it to act as a template for other classes. This is where **Abstraction** comes in.

---

## 1. Abstract Classes

If you mark a class as `abstract`, you cannot create an object of it using `new`. 

Abstract classes can also have **abstract methods**—methods with no body (no `{}`) that *must* be overridden by any child class.

```java
abstract class Shape {
    String color;
    
    // Abstract method: No body! Just a semicolon.
    public abstract void draw(); 
}

class Square extends Shape {
    // We MUST override draw(), or Java will throw an error.
    @Override
    public void draw() {
        System.out.println("Drawing a Square");
    }
}

public class Main {
    public static void main(String[] args) {
        // Shape s = new Shape(); // ❌ ERROR! Shape is abstract.
        Shape s = new Square();   //  Fine! Polymorphism still works.
        s.draw();
    }
}
```

### 🏋️ Micro-Exercise: Abstract Animals

**1. Setup:**

```java
abstract class Pet {
    public abstract void makeSound();
}
```

**2. Your Task:**

- Create a `Bird` class that `extends Pet`.
- You must override `makeSound()` to print `"Chirp chirp!"`.
- In `main`, create a `Bird` and call `makeSound()`.

**3. Expected Console Output:**

```text
Chirp chirp!
```

---

## 2. Interfaces (Contracts)

Java does not allow a class to inherit from more than one parent class. But what if you want a `Smartphone` to be a `Phone` AND a `Camera` AND a `GPS`? 

You use **Interfaces**. An Interface is like a 100% abstract class. It only contains method signatures (promises of what a class *can do*). A class **implements** an interface.

```java
// The Contract
interface Flyable {
    void fly(); // Inherently public and abstract
}

// The Implementation
class Airplane implements Flyable {
    @Override
    public void fly() {
        System.out.println("Engines roaring, taking off!");
    }
}
```

---

## 3. Implementing Multiple Interfaces

A single class can implement as many interfaces as it wants, separated by commas.

```java
interface Swimmable {
    void swim();
}

interface Quackable {
    void quack();
}

class Duck implements Swimmable, Quackable {
    @Override
    public void swim() {
        System.out.println("Paddling...");
    }

    @Override
    public void quack() {
        System.out.println("Quack!");
    }
}
```

### 🏋️ Micro-Exercise: The Gadget

**1. Setup:**

```java
interface Chargeable {
    void charge();
}
```

**2. Your Task:**

- Create a `Laptop` class that `implements Chargeable`.
- Override `charge()` to print `"Plugging in USB-C..."`.
- Test it in `main`.

**3. Expected Console Output:**

```text
Plugging in USB-C...
```

---

## ⚠️ Common Pitfalls

1. **Instantiating Interfaces:**
   Just like abstract classes, you cannot use `new` on an Interface.
   ```java
   Flyable f = new Flyable(); // ❌ ERROR!
   ```
2. **Missing Implementations:**
   If your class says `implements Flyable`, you MUST provide the code for the `fly()` method, otherwise your class won't compile.

---

## 🧠 Brain Teasers & Concept Checks

1. Can an `abstract class` have normal methods with code inside them? 
2. Can an `interface` have instance variables (fields) like `String name`?
3. If `Car` extends `Vehicle` and implements `Drivable`, what is the correct syntax?
   `(A) class Car implements Drivable extends Vehicle`
   `(B) class Car extends Vehicle implements Drivable`

---

## 🚀 Stage 8 Project: The Notification System

**The Goal:** Use an interface to treat different notification types exactly the same way.

**1. Starter Setup:**
```java
// 1. Create Sendable interface

// 2. Create Email class

// 3. Create SMS class

public class Main {
    public static void main(String[] args) {
        // 4. Test here
    }
}
```

**2. Your Task:**
- Create an interface `Sendable` with one method: `void send(String message);`.
- Create an `Email` class that implements `Sendable`. Its `send` method should print `"Sending Email: " + message`.
- Create an `SMS` class that implements `Sendable`. Its `send` method should print `"Sending Text: " + message`.
- In `main`, create a variable of type `Sendable`. First, assign it a `new Email()` and call `send("Hello!")`. Then, reassign the SAME variable to a `new SMS()` and call `send("Hello!")` again.

**3. Expected Console Output:**
```text
Sending Email: Hello!
Sending Text: Hello!
```
