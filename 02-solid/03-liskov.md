# Liskov Substitution Principle (LSP) 

## Introduction

The **Liskov Substitution Principle (LSP)** states that **objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program**.

In simpler terms, a subclass must be able to stand in for its parent class without breaking the expected behavior.

LSP is critical for **polymorphism**, **reliability**, and **maintainable OOP design**.

---

## Why LSP is Important

* Ensures **subclasses are true substitutes** for their parent classes
* Maintains **behavioral consistency** across the hierarchy
* Reduces **runtime errors and unexpected behavior**
* Supports **polymorphism** and design flexibility

---

## Problem Example Violating LSP

```php
class Bird {
    public function fly() {
        echo "Flying";
    }
}

class Duck extends Bird {}
class Ostrich extends Bird {
    public function fly() {
        throw new Exception('Cannot fly');
    }
}

function makeBirdFly(Bird $bird) {
    $bird->fly();
}

makeBirdFly(new Duck()); // Works fine
makeBirdFly(new Ostrich()); // Throws exception, violates LSP
```

**Problems:**

* `Ostrich` cannot fly but inherits `fly()` from `Bird`
* Substituting `Bird` with `Ostrich` breaks expected behavior
* Clients depending on `Bird` expect `fly()` to work

---

## Solution With LSP

Redesign the hierarchy based on **capabilities, not a general class**:

```php
interface Flyable {
    public function fly();
}

class Bird {}
class Duck extends Bird implements Flyable {
    public function fly() {
        echo "Duck is flying";
    }
}
class Ostrich extends Bird {}

function makeBirdFly(Flyable $bird) {
    $bird->fly();
}

makeBirdFly(new Duck()); // Works
// Ostrich is not Flyable, cannot be passed, avoids violation
```

**Benefits:**

* Subclasses adhere to **expected behavior**
* Prevents **runtime errors**
* Encourages **interfaces for capabilities** rather than forcing all subclasses to implement methods

---

## When to Use LSP

* Always design class hierarchies based on **shared behavior and capabilities**
* Avoid forcing subclasses to inherit methods they cannot implement meaningfully
* Use **interfaces** or **traits** to define specific capabilities

---

## Practical Tips

* Test subclasses to ensure **they can replace the parent class without breaking functionality**
* Avoid methods in parent classes that **not all children can implement**
* Use **composition** if multiple behaviors are needed but inheritance is not suitable
* Combine with **OCP** to allow safe extensions without modifying existing code

---

## Summary

* LSP ensures **subtypes are substitutable for their base types**
* Solves problems of **unexpected behavior and runtime errors** in polymorphic code
* Encourages **capability-based design** using interfaces or traits
* Foundation for safe **polymorphism and clean OOP architecture**

---

## Next Steps

Proceed to `04-interface-segregation.md` to learn about the **Interface Segregation Principle (ISP)** and how it helps avoid fat interfaces in PHP.
