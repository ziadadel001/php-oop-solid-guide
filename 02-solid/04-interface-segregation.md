# Interface Segregation Principle (ISP) 

## Introduction

The **Interface Segregation Principle (ISP)** states that **clients should not be forced to depend on interfaces they do not use**. In other words, **split large, general-purpose interfaces into smaller, specific ones** so that implementing classes only need to worry about methods that are relevant to them.

ISP is essential for **clean architecture, maintainable code, and reducing unnecessary dependencies**.

---

## Why ISP is Important

* Reduces **tight coupling** between classes
* Avoids **fat interfaces** with unrelated methods
* Improves **maintainability and readability**
* Encourages **focused, reusable interfaces**

---

## Problem Example Violating ISP

```php
interface Worker {
    public function work();
    public function eat();
}

class HumanWorker implements Worker {
    public function work() {}
    public function eat() {}
}

class RobotWorker implements Worker {
    public function work() {}
    public function eat() {
        throw new Exception('Robots do not eat');
    }
}
```

**Problems:**

* `RobotWorker` is forced to implement `eat()` which is **irrelevant**
* Leads to **unnecessary exceptions** or empty method implementations
* Violates ISP because clients depend on methods they do not need

---

## Solution With ISP

Split interfaces into **smaller, focused ones**:

```php
interface Workable {
    public function work();
}

interface Feedable {
    public function eat();
}

class HumanWorker implements Workable, Feedable {
    public function work() {}
    public function eat() {}
}

class RobotWorker implements Workable {
    public function work() {}
}
```

**Benefits:**

* Classes only implement **methods relevant to them**
* Avoids unnecessary empty or exception-throwing methods
* Improves **flexibility, clarity, and maintainability**

---

## When to Use ISP

* When an interface has **methods not needed by all clients**
* When multiple types of classes implement the same interface differently
* Always split interfaces by **specific functionality** rather than using a generic interface

---

## Practical Tips

* Name interfaces based on **single capability or responsibility** (e.g., `Workable`, `Feedable`, `Renderable`)
* Avoid forcing classes to implement methods they do not need
* Combine ISP with **SRP and OCP** for clean, flexible design
* Use **composition** to combine multiple small interfaces for complex classes

---

## Summary

* ISP ensures **clients are not forced to depend on unused methods**
* Solves problems of **fat interfaces, tight coupling, and unnecessary exceptions**
* Encourages **small, focused, and reusable interfaces**
* Works best with **SRP and OCP** for maintainable OOP architecture

---

## Next Steps

Proceed to `05-dependency-inversion.md` to learn about the **Dependency Inversion Principle (DIP)** and how it decouples high-level modules from low-level implementations in PHP.
