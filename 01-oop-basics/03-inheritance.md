# Inheritance in PHP 

## Introduction

**Inheritance** is a core OOP concept that allows a class (child/subclass) to acquire the properties and methods of another class (parent/superclass). It enables **code reuse**, **logical hierarchy**, and **polymorphic behavior**.

This file explains inheritance in PHP in detail, including **limitations, advanced notes, and traits**.

---

## Basic Inheritance

To inherit a class in PHP, use the `extends` keyword.

```php
class Vehicle {
    public string $brand;

    public function start(): string {
        return 'Vehicle started';
    }
}

class Car extends Vehicle {
    public int $doors;
}

$car = new Car();
$car->brand = 'BMW';
$car->doors = 4;
echo $car->start(); // inherited method
```

* `Car` inherits `brand` property and `start()` method from `Vehicle`
* Child class can add its own properties and methods

---

## Overriding Methods

Child classes can **override** parent methods to provide custom behavior.

```php
class Car extends Vehicle {
    public function start(): string {
        return 'Car is ready to drive';
    }
}

$car = new Car();
echo $car->start(); // output: Car is ready to drive
```

* Use the same method name in child class
* Can also call parent method using `parent::` keyword

```php
class Car extends Vehicle {
    public function start(): string {
        return parent::start() . ' - Car is ready';
    }
}
```

---

## Constructors and Inheritance

Child classes do **not automatically call parent constructors** unless explicitly using `parent::__construct()`.

```php
class Vehicle {
    public function __construct(public string $brand) {}
}

class Car extends Vehicle {
    public function __construct(public string $brand, public int $doors) {
        parent::__construct($brand);
    }
}

$car = new Car('BMW', 4);
```

* Important to initialize parent properties manually if child has its own constructor

---

## Single Inheritance in PHP

PHP **does not support multiple inheritance** (a class cannot extend more than one class).

```php
// Not allowed in PHP
// class Car extends Vehicle, Engine {} // Syntax error
```

* This restriction prevents **diamond problem** and complexity in method resolution
* To achieve multiple inheritance-like behavior, PHP uses **Traits**

---

## Traits - Multiple Inheritance Alternative

**Traits** allow you to reuse code in multiple classes without using traditional inheritance.

```php
trait EngineTrait {
    public function startEngine(): string {
        return 'Engine started';
    }
}

trait GPSModule {
    public function activateGPS(): string {
        return 'GPS activated';
    }
}

class Car {
    use EngineTrait, GPSModule;
}

$car = new Car();
echo $car->startEngine();
echo $car->activateGPS();
```

* `use` keyword includes traits in the class
* Can include multiple traits
* Allows code reuse without multiple inheritance

### Trait Conflicts

If two traits have the same method, you must **resolve conflicts**:

```php
trait A {
    public function hello() {
        return 'Hello from A';
    }
}

trait B {
    public function hello() {
        return 'Hello from B';
    }
}

class MyClass {
    use A, B {
        B::hello insteadof A;
        A::hello as helloFromA;
    }
}

$obj = new MyClass();
echo $obj->hello(); // uses B
echo $obj->helloFromA(); // uses A
```

* `insteadof` resolves which trait method to use
* `as` creates alias for original method

---

## Notes - Advanced

* Single inheritance is sufficient in most cases
* Traits provide a flexible way to share methods among unrelated classes
* Avoid overusing traits to prevent confusion
* You can combine inheritance and traits in a single class
* Use parent method calls (`parent::`) when overriding to extend functionality
* Always initialize parent constructors if required
* Understand the **diamond problem** conceptually: multiple inheritance ambiguity is why PHP disallows it

---

## Summary

* Inheritance allows child classes to reuse parent class properties and methods
* PHP supports **single inheritance** only
* Child classes can **override methods** and call parent methods with `parent::`
* Constructors must be called explicitly from child if needed
* Multiple inheritance is simulated via **Traits**
* Traits can be combined and conflicts resolved using `insteadof` and `as`

---

## Next Steps

After understanding inheritance, move on to `04-polymorphism.md` to learn how objects can behave differently while sharing the same interface.
