# Stage 9: Data Organization (Arrays & Collections)

So far, every variable we've created holds exactly one thing (one `int`, one `String`, one `Dog`). How do we store a list of things? 

---

## 1. Standard Arrays (Fixed Size)

A standard array is a list of a specific type. **Crucial Rule:** Standard Java arrays have a *fixed size*. Once you say an array holds 5 items, it can never hold 6.

```java
// Create an array that holds exactly 3 ints
int[] scores = new int[3];

scores[0] = 90; // Indexes start at 0!
scores[1] = 85;
scores[2] = 100;

System.out.println(scores[1]); // Prints 85
```

You can also initialize an array with data immediately:

```java
String[] days = {"Monday", "Tuesday", "Wednesday"};
System.out.println(days.length); // Prints 3
```

### 🏋️ Micro-Exercise: The Roster

**1. Setup:**

```java
String[] students = new String[2];
```

**2. Your Task:**

- Assign `"Alice"` to the first slot.
- Assign `"Bob"` to the second slot.
- Use a `for` loop to iterate from `0` up to `students.length` (exclusive) and print each student's name.

**3. Expected Console Output:**

```text
Alice
Bob
```

---

## 2. Introduction to ArrayList (Dynamic Size)

Because fixed arrays can be annoying, Java provides the `ArrayList` class in the `java.util` package. An `ArrayList` can grow and shrink automatically!

```java
import java.util.ArrayList; // Must import this!

public class Main {
    public static void main(String[] args) {
        // Create an ArrayList of Strings
        ArrayList<String> colors = new ArrayList<>();
        
        colors.add("Red");      // Size is 1
        colors.add("Blue");     // Size is 2
        
        System.out.println(colors.get(0)); // Prints "Red"
        
        colors.remove("Red");   // Size is now 1
    }
}
```

> **Generics `<Type>`**
> The `<String>` part tells Java what type of objects go into this list. This is called a Generic.

### 🏋️ Micro-Exercise: The Shopping List

**1. Setup:**

```java
import java.util.ArrayList;

// In main...
```

**2. Your Task:**

- Create an `ArrayList<String>` called `groceries`.
- Add `"Milk"`, `"Eggs"`, and `"Bread"`.
- Use the `.size()` method to print how many items are in the list.

**3. Expected Console Output:**

```text
3
```

---

## 3. Wrapper Classes

There's a catch with `ArrayList`: it can ONLY hold Objects, not primitives! You cannot write `ArrayList<int>`. 

Instead, Java provides "Wrapper Classes" that wrap a primitive inside an Object.

- `int` -> `Integer`
- `double` -> `Double`
- `boolean` -> `Boolean`
- `char` -> `Character`

```java
// ❌ ArrayList<int> numbers = new ArrayList<>(); 
//  Correct:
ArrayList<Integer> numbers = new ArrayList<>();
numbers.add(42); // Java automatically wraps the primitive 42 into an Integer!
```

---

## 4. The Enhanced `for` Loop (For-Each)

When looping through arrays or ArrayLists, Java has a shortcut loop that is much easier to read:

```java
String[] fruits = {"Apple", "Banana", "Cherry"};

// Read as: "For each String f in fruits"
for (String f : fruits) {
    System.out.println(f);
}
```

---

## ⚠️ Common Pitfalls

1. **`ArrayIndexOutOfBoundsException`:**
   If an array has a length of 3, the valid indexes are `0`, `1`, and `2`. Trying to access `arr[3]` will crash your program.
2. **`length` vs `.size()` vs `.length()`:**
   - Standard Arrays use `.length` (a property).
   - `ArrayList` uses `.size()` (a method).
   - `String` uses `.length()` (a method). 
   Yes, it's confusing!

---

## 🧠 Brain Teasers & Concept Checks

1. Can a standard array hold a mix of `int`s and `String`s?
2. If you don't know how many items a user will add to a list, should you use an Array or an `ArrayList`?

---

## 🚀 Stage 9 Project: The Task Manager

**The Goal:** Build a simple To-Do list using an `ArrayList`.

**1. Starter Setup:**
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // Write your list logic here
    }
}
```

**2. Your Task:**
- Create an `ArrayList<String>` called `tasks`.
- Add three tasks to it: `"Do homework"`, `"Wash car"`, `"Buy groceries"`.
- Use an enhanced `for` loop to print all tasks, but add a dash before each one (e.g., `"- Do homework"`).
- Remove `"Wash car"`.
- Print a blank line using `System.out.println();`
- Print `"Tasks remaining: " + tasks.size()`.

**3. Expected Console Output:**
```text
- Do homework
- Wash car
- Buy groceries

Tasks remaining: 2
```
