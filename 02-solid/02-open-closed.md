# Open/Closed Principle (OCP) 

## Introduction

The **Open/Closed Principle (OCP)** states that **software entities (classes, modules, functions) should be open for extension but closed for modification**. This means you can **add new functionality without changing existing code**.

OCP is crucial for **maintainable and scalable applications**. It reduces the risk of introducing bugs when adding new features.

---

## Why OCP is Important

* **Prevent regressions**: Existing code remains unchanged, minimizing new bugs.
* **Promotes flexibility**: Easy to add new functionality without touching old code.
* **Encourages abstraction**: Use interfaces and polymorphism to extend behavior.
* **Supports SOLID principles**: Works closely with SRP and DIP.

---

## Problem Example Without OCP

Imagine a payment processor class that handles multiple payment methods:

```php
class PaymentProcessor {
    public function pay($amount, $type) {
        if ($type === 'credit_card') {
            // process credit card payment
        } elseif ($type === 'paypal') {
            // process PayPal payment
        }
    }
}
```

**Problems:**

* Adding a new payment method requires **modifying existing class**.
* Violates OCP because the class is **not closed for modification**.
* Risk of **introducing bugs** in existing methods.

---

## Solution With OCP

Use **interfaces and polymorphism** to extend functionality without modifying existing code:

```php
interface PaymentMethod {
    public function pay(float $amount);
}

class CreditCardPayment implements PaymentMethod {
    public function pay(float $amount) {
        echo "Paid $amount using credit card";
    }
}

class PayPalPayment implements PaymentMethod {
    public function pay(float $amount) {
        echo "Paid $amount using PayPal";
    }
}

function processPayment(PaymentMethod $payment, float $amount) {
    $payment->pay($amount);
}
```

**Benefits:**

* Adding a new payment method (e.g., `BitcoinPayment`) **does not require changing `processPayment`**
* The code is **open for extension** via new classes and **closed for modification** of existing ones
* Each class has a **single responsibility** (SRP) and is **loosely coupled**

---

## When to Use OCP

* When you expect **new features to be added frequently**
* When you want **stable, production code that can evolve safely**
* Always combine with **interfaces or abstract classes**

---

## Practical Tips

* Use **interfaces or abstract classes** as the base for extensibility
* Avoid modifying existing classes; add **new subclasses** instead
* Apply **polymorphism** and dependency injection for flexibility
* Combine with **Factory pattern** to create new objects without changing existing code

---

## Summary

* OCP allows **extending behavior without modifying existing code**
* Reduces risk of bugs when adding new features
* Encourages **flexible, maintainable, and testable architecture**
* Works best when combined with **interfaces, abstraction, and other SOLID principles**

---

## Next Steps

Proceed to `03-liskov.md` to learn about the **Liskov Substitution Principle (LSP)** and why it ensures safe polymorphism in PHP.
