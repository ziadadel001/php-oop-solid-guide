# OOP Notes 

## Introduction

This file contains **advanced notes and best practices** for Object-Oriented Programming (OOP) in PHP. It serves as a reference to consolidate everything learned in previous sections: **Basics, Encapsulation, Inheritance, Polymorphism, and Abstraction**.

---

## 1. General Principles

* Always design classes with a **single responsibility** in mind
* Use **meaningful class and method names**
* Keep methods **short and focused**
* Prefer composition over inheritance when it reduces complexity
* Favor **interfaces and type hints** for flexibility
* Avoid unnecessary public properties; encapsulate data

---

## 2. Visibility and Access

* **public**: accessible anywhere
* **private**: accessible only inside the class
* **protected**: accessible inside class and subclasses
* Use **getters and setters** even if validation is minimal; ensures **future-proofing**
* Use **readonly properties** (PHP 8.1+) for immutable data

---

## 3. Inheritance Notes

* PHP supports **single inheritance** only
* Use `parent::method()` when overriding to extend functionality
* Call parent constructors explicitly if child class has its own constructor
* Avoid deep inheritance chains; they are hard to maintain
* Combine inheritance with **Traits** for code reuse without multiple inheritance

---

## 4. Traits Notes

* Traits allow **code reuse across unrelated classes**
* Multiple traits can be used in a single class
* Resolve conflicts using `insteadof` and `as`
* Avoid overusing traits; they can introduce complexity if misused

---

## 5. Polymorphism Notes

* Objects can take **many forms**: achieved via inheritance, interfaces, and abstract classes
* Accept **base class or interface types** in functions and constructors
* Helps with **scalability, flexibility, and testability**
* Key for **SOLID principles**: Liskov Substitution, Open/Closed

---

## 6. Abstraction Notes

* Abstraction **hides internal implementation details**
* Use **abstract classes** when you need shared code and enforced structure
* Use **interfaces** for contracts among multiple unrelated classes
* Combine abstraction with polymorphism for flexible and maintainable code

---

## 7. Best Practices and Tips

* **Type hint everything** (parameters, return types, properties)
* Validate data in setters
* Keep constructors simple; avoid heavy logic
* Use **Dependency Injection** instead of hard-coded dependencies
* Prefer **composition over inheritance** when possible
* Keep class responsibilities minimal and focused
* Use **exceptions** for error handling instead of returning false/null
* Always write code that is **easy to read and maintain**
* Document your classes and methods

---

## Summary

* Encapsulation, Inheritance, Polymorphism, and Abstraction form the foundation of PHP OOP
* Traits, interfaces, and abstract classes enhance flexibility and maintainability
* Applying these principles consistently will result in **clean, scalable, and testable code**
* Follow SOLID principles alongside OOP for best practices

---

## Next Steps

After reviewing these notes, proceed to `07-advanced.md` to explore **advanced OOP techniques and tips**, including **real-world PHP examples, design patterns, and optimization strategies**.
