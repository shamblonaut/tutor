# Stage 6: Encapsulation & State Protection

Encapsulation is the practice of hiding the internal state of an object and requiring all interaction to be performed through an object's methods.

---

## 1. Access Modifiers

By default, the fields we created in Stage 5 were accessible to anyone. We can restrict access using **modifiers**:

- **`public`**: Anyone can access this field or method from anywhere.
- **`private`**: Only the class itself can see or modify this field.

```java
class Wallet {
    // Hidden from the outside world!
    private double money; 

    public Wallet(double startingMoney) {
        money = startingMoney;
    }
}

public class Main {
    public static void main(String[] args) {
        Wallet myWallet = new Wallet(50.0);
        
        // myWallet.money = 1000000.0; // ❌ ERROR! money has private access.
    }
}
```

---

## 2. Getters and Setters

If fields are private, how do we read or change them? We provide `public` methods specifically designed for that purpose, usually called **getters** (to read) and **setters** (to write). 

This allows the class to control *how* things are changed (e.g., preventing a negative balance).

```java
class Wallet {
    private double money;

    public Wallet(double startMoney) {
        money = startMoney;
    }

    // Getter
    public double getMoney() {
        return money;
    }

    // Setter (with logic!)
    public void addMoney(double amount) {
        if (amount > 0) {
            money += amount;
        } else {
            System.out.println("Cannot add a negative amount!");
        }
    }
}
```

### 🏋️ Micro-Exercise: The Vault

**1. Setup:**

```java
class Vault {
    private String secretCode;

    public Vault(String code) {
        secretCode = code;
    }
    
    // Write getter here
}
```

**2. Your Task:**

- Add a `public` getter method named `getSecretCode()` that returns the `secretCode`.
- In `main`, create a `Vault` with the code `"1234"`.
- Use the getter to print the code. (Do not try to print `vault.secretCode` directly).

**3. Expected Console Output:**

```text
1234
```

---

## 3. The `this` Keyword

Sometimes, a method parameter has the exact same name as an instance variable. To tell Java "I mean the instance variable belonging to this specific object", use the `this` keyword.

```java
class User {
    private String username;

    public User(String username) {
        // 'this.username' is the field. 'username' is the parameter.
        this.username = username; 
    }
}
```

### 🏋️ Micro-Exercise: The Person

**1. Setup:**

```java
class Person {
    private int age;

    public void setAge(int age) {
        // Fix this method using 'this'
        age = age; 
    }
}
```

**2. Your Task:**

- Fix the `setAge` method by using `this.age` so that the object's field is actually updated.

---

## ⚠️ Common Pitfalls

1. **Forgetting Getters/Setters:**
   If you make fields `private` but forget to write getters, your `main` program will never be able to read the data inside the object.

2. **Shadowing Variables:**
   If you forget `this.` when the parameter name matches the field name, you end up assigning the parameter to itself. The object's field remains unchanged!
   ```java
   public void setName(String name) {
       name = name; // ❌ Does absolutely nothing to the object!
   }
   ```

---

## 🧠 Brain Teasers & Concept Checks

1. Why is making fields `private` generally considered a good idea?
2. If a class has a `private int score`, and you want the outside world to be able to read the score but NEVER change it, which method do you provide: a getter, a setter, or both?

---

## 🚀 Stage 6 Project: The Bank Account

**The Goal:** Create a secure bank account system.

**1. Starter Setup:**
```java
class BankAccount {
    // Add fields and methods here
}

public class Main {
    public static void main(String[] args) {
        // Test your account here
    }
}
```

**2. Your Task:**
- In `BankAccount`, create a `private String accountHolder` and a `private double balance`.
- Create a constructor that sets `accountHolder` and sets `balance` to `0.0`. Use the `this` keyword.
- Write a getter for the balance (`getBalance`).
- Write a `deposit(double amount)` method. Only add to the balance if `amount` is greater than 0.
- Write a `withdraw(double amount)` method. Only subtract if `amount` is greater than 0 AND they have enough balance. Otherwise, print `"Insufficient funds"`.
- Test it in `main` by depositing `100`, withdrawing `50`, and withdrawing `200` (which should fail). Print the final balance.

**3. Expected Console Output:**
```text
Insufficient funds
Final Balance: 50.0
```
