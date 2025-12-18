# Polymorphism in PHP

## Introduction

**Polymorphism** is an OOP concept that allows objects of different classes to be treated as objects of a **common superclass or interface**. The word "polymorphism" means **many forms**.

### Why Polymorphism is Important

Polymorphism is essential for building **flexible, scalable, and maintainable code**. It allows you to:

* Write code that can work with different object types interchangeably
* Avoid rewriting methods for each specific class
* Enable clean **dependency injection** and **loose coupling**
* Improve testability by mocking objects via interfaces

### Problem Example

Imagine you are building a payment system:

* You have multiple payment methods: `CreditCard`, `PayPal`, `BankTransfer`
* Without polymorphism, your code would need separate functions for each payment method:

```php
function payWithCreditCard(CreditCard $credit, float $amount) {}
function payWithPayPal(PayPal $paypal, float $amount) {}
function payWithBank(BankTransfer $bank, float $amount) {}
```

* This approach is **not scalable**. Adding a new payment method requires changing many places in your code.

### How Polymorphism Solves It

* Define a common interface `PaymentMethod`
* Each payment class implements this interface
* A single function can process any payment method

```php
interface PaymentMethod {
    public function pay(float $amount): string;
}

function processPayment(PaymentMethod $payment, float $amount) {
    echo $payment->pay($amount);
}
```

* Now, adding a new payment method requires **only creating a new class implementing PaymentMethod**
* No changes are needed in `processPayment` or other code using it

This approach reduces **duplication, increases flexibility**, and follows **SOLID principles** (especially Open/Closed and Liskov Substitution).

---

## 1. Polymorphism via Inheritance

A child class can override parent methods to provide specific behavior.

```php
class Vehicle {
    public function start(): string {
        return 'Vehicle is starting';
    }
}

class Car extends Vehicle {
    public function start(): string {
        return 'Car is starting';
    }
}

class Bike extends Vehicle {
    public function start(): string {
        return 'Bike is starting';
    }
}

function beginJourney(Vehicle $vehicle) {
    echo $vehicle->start();
}

$car = new Car();
$bike = new Bike();

beginJourney($car); // Car is starting
beginJourney($bike); // Bike is starting
```

* `beginJourney` can accept any object of type `Vehicle` or its child
* Each object behaves differently (`Car` vs `Bike`)
* This is **runtime polymorphism** or **method overriding**

---

## 2. Polymorphism via Interfaces

**Interfaces** define a contract. Any class implementing the interface must implement all its methods.

```php
interface PaymentMethod {
    public function pay(float $amount): string;
}

class CreditCard implements PaymentMethod {
    public function pay(float $amount): string {
        return "Paid $amount using Credit Card";
    }
}

class PayPal implements PaymentMethod {
    public function pay(float $amount): string {
        return "Paid $amount using PayPal";
    }
}

function processPayment(PaymentMethod $payment, float $amount) {
    echo $payment->pay($amount);
}

$credit = new CreditCard();
$paypal = new PayPal();

processPayment($credit, 100);
processPayment($paypal, 200);
```

* Any class implementing `PaymentMethod` can be passed to `processPayment`
* Different payment methods behave differently
* This is **interface polymorphism**

---

## 3. Polymorphism via Abstract Classes

**Abstract classes** can define methods that must be implemented by child classes.

```php
abstract class Shape {
    abstract public function area(): float;
}

class Circle extends Shape {
    public function __construct(private float $radius) {}
    public function area(): float {
        return pi() * $this->radius ** 2;
    }
}

class Rectangle extends Shape {
    public function __construct(private float $width, private float $height) {}
    public function area(): float {
        return $this->width * $this->height;
    }
}

$shapes = [new Circle(5), new Rectangle(4,6)];

foreach ($shapes as $shape) {
    echo $shape->area();
}
```

* All shapes implement `area()` differently
* Can be used interchangeably in arrays or functions
* This is **abstract class polymorphism**

---

## 4. Static vs Dynamic Polymorphism

* **Static polymorphism (compile-time)**: method overloading is not directly supported in PHP; you can use optional parameters to emulate it.
* **Dynamic polymorphism (runtime)**: method overriding and interface implementation

```php
class Logger {
    public function log(string $message, string $level = 'info') {
        echo "[$level] $message";
    }
}

$logger = new Logger();
$logger->log('System started');
$logger->log('Something went wrong', 'error');
```

* Optional parameter allows multiple forms of the same method

---

## 5. Common Questions About Polymorphism

1. **Can PHP overload methods like Java?**

   * Not directly. Use optional parameters or different method names.
2. **Why is polymorphism important?**

   * Allows code reuse, scalability, and flexibility
3. **Difference between interface and abstract class for polymorphism?**

   * Interfaces: only define methods; a class can implement multiple interfaces
   * Abstract classes: can have properties and methods; single inheritance
4. **Can traits achieve polymorphism?**

   * Yes, but more like code reuse; cannot enforce a contract like interfaces
5. **How to combine polymorphism with dependency injection?**

   * Accept parent type or interface in constructor/method; pass child objects

---

## 6. Best Practices

* Use interfaces to define contracts
* Use abstract classes for shared code and enforced methods
* Avoid long class hierarchies; prefer composition when possible
* Always type-hint methods to accept base class or interface
* Keep method overriding consistent with parent expectations
* Combine polymorphism with dependency injection for clean, testable code

---

## Summary

* Polymorphism = objects can take many forms
* Achieved via **inheritance**, **interfaces**, **abstract classes**
* Dynamic polymorphism (runtime) is most common in PHP
* Allows flexible, reusable, and maintainable code
* Essential for **SOLID** principles (especially Liskov Substitution and Open/Closed)

---

## Next Steps

After mastering polymorphism, proceed to `05-abstraction.md` to understand how **abstract classes** enforce a structure for your objects and combine with polymorphism.
