# Stage 5: Introduction to Classes & Objects

Welcome to Object-Oriented Programming (OOP)! This is the paradigm shift that makes Java so powerful. 

---

## 1. Classes vs. Objects

- A **Class** is a blueprint or template. (e.g., the concept of a `Car`).
- An **Object** is a specific, concrete instance built from that blueprint. (e.g., *your* red Honda Civic).

You write a Class once, but you can create hundreds of Objects from it!

```java
// 1. The Blueprint (Class)
class Car {
    String color;
    int year;
}

public class Main {
    public static void main(String[] args) {
        // 2. The Concrete Object (Instance)
        Car myCar = new Car(); // 'new' builds the object!
        myCar.color = "Red";
        myCar.year = 2022;
        
        System.out.println("My car is " + myCar.color);
    }
}
```

---

## 2. Instance Variables (Fields)

The variables defined directly inside a class (but outside any methods) are called **fields** or **instance variables**. Every object you create gets its own separate copy of these variables.

### 🏋️ Micro-Exercise: The Dog Blueprint

**1. Setup:**

```java
class Dog {
    // Write fields here
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        // Set the fields here
        
        System.out.println(myDog.name + " is a " + myDog.breed);
    }
}
```

**2. Your Task:**

- Inside the `Dog` class, define two fields: a `String name` and a `String breed`.
- Inside `main`, assign `"Buddy"` to `myDog.name` and `"Golden Retriever"` to `myDog.breed`.

**3. Expected Console Output:**

```text
Buddy is a Golden Retriever
```

---

## 3. Constructors

When you use the `new` keyword, Java calls a special method called a **Constructor** to set up the object. Constructors have the **exact same name as the class** and **no return type**.

```java
class User {
    String username;

    // The Constructor
    User(String startName) {
        username = startName;
    }
}

public class Main {
    public static void main(String[] args) {
        // Passes "Alex123" into the constructor
        User player1 = new User("Alex123"); 
        System.out.println(player1.username);
    }
}
```

### 🏋️ Micro-Exercise: The Book Setup

**1. Setup:**

```java
class Book {
    String title;
    int pages;

    // Write constructor here
}
```

**2. Your Task:**

- Write a constructor for `Book` that takes a `String` for the title and an `int` for the pages.
- Assign the parameters to the class fields.
- In `main`, create a new `Book` called `"The Hobbit"` with `300` pages and print its title.

**3. Expected Console Output:**

```text
The Hobbit
```

---

## 4. Instance Methods

Classes can also have methods. These are actions that the specific object can perform. Notice that we **drop the `static` keyword** here, because these methods belong to a specific instance, not the class globally!

```java
class Cat {
    String name;

    Cat(String startName) {
        name = startName;
    }

    // Instance Method (No 'static'!)
    void meow() {
        System.out.println(name + " says Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        Cat cat1 = new Cat("Whiskers");
        cat1.meow(); // Object performs the action
    }
}
```

---

## ⚠️ Common Pitfalls

1. **Forgetting `new`:**
   You cannot create an object without the `new` keyword.
   ```java
   Car myCar;
   myCar.color = "Blue"; // ❌ NullPointerException! No object exists yet.
   ```

2. **Constructor Return Types:**
   If you accidentally put `void` on a constructor, Java treats it as a normal method, and your setup code won't run when you say `new`.
   ```java
   class Dog {
       void Dog() { ... } // ❌ This is a method named Dog, not a constructor!
   }
   ```

3. **Static Context:**
   You cannot call an instance method from a `static` method (like `main`) without an object!
   ```java
   // Cat.meow(); // ❌ Cannot call directly on the class.
   ```

---

## 🧠 Brain Teasers & Concept Checks

1. What keyword is used to create a brand new object in memory?
2. Why don't instance methods use the `static` keyword?
3. If you create two `Dog` objects, do they share the same `name` variable in memory, or do they each have their own?

---

## 🚀 Stage 5 Project: The Virtual Pet

**The Goal:** Build a basic Tamagotchi-style virtual pet class.

**1. Starter Setup:**
```java
class VirtualPet {
    // 1. Add fields: name (String) and hunger (int)

    // 2. Add constructor
    
    // 3. Add feed() method
}

public class Main {
    public static void main(String[] args) {
        // 4. Test your pet here
    }
}
```

**2. Your Task:**
- In `VirtualPet`, add fields for `name` and `hunger`.
- Write a constructor that takes a `String` for the name and sets `hunger` to `10` initially.
- Write an instance method `feed()` that decreases `hunger` by `2` and prints `"[Name] was fed! Hunger is now [hunger]."`.
- In `main`, instantiate a `VirtualPet` named `"Fido"`. Call `feed()` on it twice.

**3. Expected Console Output:**
```text
Fido was fed! Hunger is now 8.
Fido was fed! Hunger is now 6.
```
