# Stage 7: Inheritance & Polymorphism

In this stage, we learn how to make classes share code. Instead of writing the same fields and methods over and over, we can create a parent class and have child classes inherit from it.

---

## 1. `extends` (Inheritance)

To inherit from another class, use the `extends` keyword. The child class (subclass) gets all the `public` (and `protected`) fields and methods of the parent class (superclass).

```java
// Parent Class
class Animal {
    public void sleep() {
        System.out.println("Zzz...");
    }
}

// Child Class inherits sleep()!
class Cat extends Animal {
    public void meow() {
        System.out.println("Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        Cat myCat = new Cat();
        myCat.meow();  // Its own method
        myCat.sleep(); // Inherited method!
    }
}
```

### 🏋️ Micro-Exercise: The Vehicles

**1. Setup:**

```java
class Vehicle {
    public void honk() {
        System.out.println("Beep!");
    }
}

// Write Car class here
```

**2. Your Task:**

- Create a `Car` class that `extends Vehicle`.
- Give `Car` its own method `drive()` that prints `"Vroom"`.
- In `main`, create a `Car` and call both `honk()` and `drive()`.

**3. Expected Console Output:**

```text
Beep!
Vroom
```

---

## 2. The `super` Keyword

If the parent class has a constructor that requires arguments, the child class *must* call that parent constructor using the `super()` keyword as the very first line in its own constructor.

```java
class Person {
    String name;
    
    public Person(String name) {
        this.name = name;
    }
}

class Student extends Person {
    int gradeLevel;

    public Student(String name, int gradeLevel) {
        super(name); // Calls Person(String name)
        this.gradeLevel = gradeLevel;
    }
}
```

---

## 3. Overriding Methods

If a child class doesn't like how the parent class implemented a method, it can write its own version with the exact same name. This is called **overriding**.

Use the `@Override` annotation just above the method. It tells Java to check that you are actually overriding a parent method.

```java
class Animal {
    public void speak() {
        System.out.println("Generic animal sound");
    }
}

class Dog extends Animal {
    @Override
    public void speak() {
        System.out.println("Woof!");
    }
}
```

### 🏋️ Micro-Exercise: Overriding

**1. Setup:**

```java
class Shape {
    public void draw() {
        System.out.println("Drawing a basic shape");
    }
}

class Circle extends Shape {
    // Override draw here
}
```

**2. Your Task:**

- Inside `Circle`, override the `draw()` method to print `"Drawing a round circle"`. Use the `@Override` annotation.
- Create a `Circle` in `main` and call `draw()`.

**3. Expected Console Output:**

```text
Drawing a round circle
```

---

## 4. Polymorphism

Polymorphism means "many forms". Because a `Dog` *is an* `Animal`, you can store a `Dog` object inside an `Animal` variable! 

Java will automatically run the *overridden* methods of the actual object in memory.

```java
Animal pet1 = new Dog(); // A Dog in an Animal box!
pet1.speak(); // Prints "Woof!" because it's actually a Dog.
```

---

## ⚠️ Common Pitfalls

1. **`super` must be first:**
   If you use `super()` in a constructor, it MUST be the very first line.
   ```java
   public Student(String name) {
       System.out.println("Setting up!");
       super(name); // ❌ Error: Constructor call must be first statement
   }
   ```
2. **Missing `@Override`:**
   If you misspell a method you are trying to override (e.g., `speek()` instead of `speak()`), and you don't use `@Override`, Java will think you just created a brand new method. `@Override` catches this typo for you!

---

## 🧠 Brain Teasers & Concept Checks

1. Can a class inherit from more than one class in Java? (e.g., `class Dog extends Animal, Pet`)
2. If `class C extends B`, and `class B extends A`, does `C` inherit methods from `A`?

---

## 🚀 Stage 7 Project: RPG Characters

**The Goal:** Create a base character class and two specific classes that override an attack method.

**1. Starter Setup:**
```java
class Character {
    String name;

    public Character(String name) {
        this.name = name;
    }

    public void attack() {
        System.out.println(name + " attacks with bare hands!");
    }
}

// 1. Create Warrior class
// 2. Create Mage class

public class Main {
    public static void main(String[] args) {
        // 3. Test here
    }
}
```

**2. Your Task:**
- Create a `Warrior` class that extends `Character`.
  - Override `attack()` to print `"[Name] swings a huge sword!"`.
  - Remember to add a constructor that calls `super(name)`.
- Create a `Mage` class that extends `Character`.
  - Override `attack()` to print `"[Name] casts a fireball!"`.
  - Remember to add a constructor.
- In `main`, create an array or just two separate variables of type `Character`. Assign one a `Warrior` and one a `Mage`. Call `attack()` on both.

**3. Expected Console Output:**
```text
Conan swings a huge sword!
Gandalf casts a fireball!
```
