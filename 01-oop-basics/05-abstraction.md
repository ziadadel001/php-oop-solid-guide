# Abstraction in PHP

## Introduction

**Abstraction** is an OOP principle that allows you to **focus on the essential characteristics of an object** while **hiding unnecessary implementation details**. It provides a way to define **what an object does**, without specifying exactly **how it does it**.

In PHP, abstraction is achieved using **abstract classes** and **interfaces**. This file explains abstraction in detail, including examples, best practices, and advanced notes.

---

## Why Abstraction is Important

Abstraction is important for:

* Simplifying complex systems
* Hiding internal implementation
* Defining a clear contract for child classes
* Facilitating polymorphism and code reuse

### Problem Example

Imagine you are building a system for different shapes:

* Each shape has a different way to calculate area
* Without abstraction, every function has to know exactly which shape it is dealing with

```php
$circle = new Circle(5);
$rectangle = new Rectangle(4,6);

echo calculateCircleArea($circle);
echo calculateRectangleArea($rectangle);
```

* Problem: functions are tied to specific classes, not scalable

### How Abstraction Solves It

* Define an abstract class `Shape` with an abstract method `area()`
* Each shape implements `area()` in its own way
* Functions can accept `Shape` type and work with any shape

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

function printArea(Shape $shape) {
    echo $shape->area();
}

$shapes = [new Circle(5), new Rectangle(4,6)];
foreach ($shapes as $shape) {
    printArea($shape);
}
```

* Now, `printArea` can work with any new shape class without modification
* This is **abstraction + polymorphism**

---

## Abstract Classes

**Abstract classes** cannot be instantiated directly. They can contain:

* Abstract methods: must be implemented by child classes
* Concrete methods: shared code usable by child classes

```php
abstract class Vehicle {
    abstract public function start(): string;

    public function describe(): string {
        return 'I am a vehicle';
    }
}

class Car extends Vehicle {
    public function start(): string {
        return 'Car started';
    }
}

$car = new Car();
echo $car->start();
echo $car->describe();
```

* `Car` must implement `start()`
* `describe()` is inherited as is

---

## Interfaces

**Interfaces** define a contract. Any class implementing the interface must implement all methods.

```php
interface Payment {
    public function pay(float $amount): string;
}

class CreditCard implements Payment {
    public function pay(float $amount): string {
        return "Paid $amount using Credit Card";
    }
}

class PayPal implements Payment {
    public function pay(float $amount): string {
        return "Paid $amount using PayPal";
    }
}
```

* Interfaces enforce **abstraction** without implementation details
* Classes can implement multiple interfaces (unlike single inheritance)

---

## Abstract vs Interface

| Feature     | Abstract Class                 | Interface                                      |
| ----------- | ------------------------------ | ---------------------------------------------- |
| Methods     | Can have abstract and concrete | Only abstract methods (PHP 8 can have default) |
| Properties  | Can have properties            | Cannot have properties                         |
| Inheritance | Single inheritance             | Can implement multiple interfaces              |
| Constructor | Can have constructor           | Cannot have constructor                        |

---

## Best Practices

* Use abstract classes when you have **shared code** and a common base
* Use interfaces to define **contracts** for multiple unrelated classes
* Combine abstract classes and interfaces for maximum flexibility
* Keep abstract methods focused and minimal
* Facilitate polymorphism by type-hinting abstract class or interface
* Avoid implementing logic in interfaces (except default methods in PHP 8+)

---

## Summary

* Abstraction hides implementation details and exposes essential behavior
* Achieved via **abstract classes** and **interfaces**
* Supports **polymorphism** and **SOLID principles**
* Essential for building maintainable, scalable systems
* Use abstract classes for shared code, interfaces for contracts

---

## Next Steps

After mastering abstraction, proceed to `06-notes.md` and `07-advanced.md` to review advanced notes, tips, and full OOP best practices in PHP.
