# Single Responsibility Principle (SRP)

## Introduction

The **Single Responsibility Principle (SRP)** states that **a class should have only one reason to change**. In other words, a class should **focus on a single responsibility or purpose**.

SRP is the foundation for clean, maintainable, and testable code. It ensures that changes in one aspect of a system do not inadvertently affect unrelated features.

---

## Why SRP is Important

* **Easier to maintain**: When classes have one responsibility, fixing bugs or updating features becomes simpler.
* **Easier to test**: Small, focused classes are easier to write unit tests for.
* **Reduces side-effects**: Changes in one functionality won't break others.
* **Promotes reusability**: A class with a single responsibility can be reused in multiple places without modification.

---

## Problem Example Without SRP

Imagine a class that handles both **invoice calculations** and **printing invoices**:

```php
class Invoice {
    public function calculateTotal(): float {
        // calculate total amount
    }

    public function printInvoice(): void {
        // print invoice logic
    }
}
```

**Problems:**

* If printing logic changes, it affects `Invoice` even though the calculation is unrelated.
* Harder to test calculation without involving printing logic.
* Class is doing two unrelated jobs: violating SRP.

---

## Solution With SRP

Split responsibilities into separate classes:

```php
class Invoice {
    public function calculateTotal(): float {
        // calculate total amount
    }
}

class InvoicePrinter {
    public function printInvoice(Invoice $invoice): void {
        // print invoice logic
    }
}
```

**Benefits:**

* Changes to printing logic **do not affect** invoice calculations.
* Each class has a **single responsibility**.
* Easier to maintain, extend, and test.

---

## When to Use SRP

* Always design classes to **do one thing**.
* Split classes when they have **multiple unrelated responsibilities**.
* Combine with **interfaces** when creating reusable components.

---

## Practical Tips

* Name classes after their **single responsibility** (e.g., `InvoiceCalculator`, `InvoicePrinter`).
* Avoid adding unrelated methods just because it seems convenient.
* Apply SRP in combination with other SOLID principles for **maximum benefit**.

---

## Summary

* SRP ensures **one reason to change per class**.
* Solves problems of **tight coupling, maintenance difficulty, and side-effects**.
* Makes code **clean, testable, and reusable**.
* Foundation for applying **other SOLID principles**.

---

## Next Steps
Proceed to `02-open-closed.md` to learn about the **Open/Closed Principle (OCP)** and how it allows extending functionality without modifying existing code.
