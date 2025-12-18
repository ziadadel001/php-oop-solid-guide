# OOP Basics in PHP 

## Introduction

Object-Oriented Programming (OOP) is a programming paradigm that organizes code around objects. Each object represents a real-world entity and contains both **data** (properties) and **behavior** (methods).

This file is a **comprehensive reference for all OOP basics in PHP**, suitable for beginners and advanced users. It covers everything from core concepts to advanced notes.

---

## Why OOP?

Procedural code becomes hard to maintain as applications grow. OOP helps:

* Organize code logically
* Reduce duplication
* Improve maintainability
* Enable scalability
* Facilitate understanding of complex systems

Modern frameworks like Laravel are built entirely using OOP.

---

## Class

A **class** is a blueprint or template defining:

* Properties (data)
* Methods (behavior)

Example:

```php
class Car {
    public string $brand;
    public string $color;

    public function drive(): string {
        return 'The car is driving';
    }
}
```

---

## Object

An **object** is an instance of a class:

```php
$car = new Car();
$car->brand = 'BMW';
$car->color = 'Red';

echo $car->drive();
```

* `$car` is an object of class `Car`
* Each object has its own properties and can perform methods

---

## Properties

Properties store object data. Visibility can be:

* `public` – accessible everywhere
* `private` – accessible only inside the class
* `protected` – accessible inside class and child classes

Example:

```php
class User {
    public string $name;
    private string $password;
    protected int $age;
}
```

---

## Getters and Setters

Using **getters and setters** allows controlled access to private or protected properties. This is a key part of **encapsulation**.

```php
class User {
    private string $password;

    public function setPassword(string $password) {
        if (strlen($password) < 6) {
            throw new Exception('Password must be at least 6 characters');
        }
        $this->password = $password;
    }

    public function getPassword(): string {
        return $this->password;
    }
}

$user = new User();
$user->setPassword('secret123');
echo $user->getPassword();
```

* Setter validates or processes data before setting it
* Getter can control how the data is accessed or formatted
* Protects object state from unwanted changes

---

## Type Hints

**Type hints** specify the expected data type for properties, method parameters, and return values, improving clarity and preventing errors.

```php
class Product {
    private float $price;

    public function setPrice(float $price) {
        if ($price < 0) {
            throw new Exception('Price must be positive');
        }
        $this->price = $price;
    }

    public function getPrice(): float {
        return $this->price;
    }
}

$product = new Product();
$product->setPrice(99.99);
echo $product->getPrice();
```

* Helps PHP detect type mismatches early
* Improves code readability and maintainability
* Works for scalar types, arrays, objects, and nullable types

---

## Methods

Methods define object behavior:

```php
class User {
    public string $name;

    public function greet(): string {
        return 'Hello, ' . $this->name;
    }
}
```

* `$this` refers to the current object
* Methods operate on object properties or perform actions

---

## $this Keyword

`$this` refers to the current object instance. Use it inside class methods to access properties or other methods:

```php
$this->propertyName;
$this->methodName();
```

---

## self Keyword

`self` refers to the current class itself (not the object instance). It is used to access **static properties and methods**:

```php
class Counter {
    public static int $count = 0;

    public static function increment() {
        self::$count++;
    }
}

Counter::increment();
echo Counter::$count;
```

* Use `self::` for static members
* `$this->` for instance members

---

## Constructor and Destructor

**Constructor** (`__construct`) initializes objects automatically on creation:

```php
class User {
    public string $name;

    public function __construct(string $name) {
        $this->name = $name;
    }
}

$user = new User('Ahmed');
```

**Destructor** (`__destruct`) is called when the object is destroyed:

```php
class User {
    public function __destruct() {
        echo 'Object destroyed';
    }
}
```

---

## Object Lifecycle

1. **Declaration** – class is defined
2. **Instantiation** – object created using `new`
3. **Initialization** – constructor runs
4. **Usage** – object properties/methods accessed
5. **Destruction** – destructor runs when object goes out of scope

---

## Visibility and Access Modifiers

* `public` – accessible anywhere
* `private` – accessible only inside the class
* `protected` – accessible in class and subclasses
* `static` – class-level property/method, accessed with `self::` or `ClassName::`

---

## Attributes and Static Members

**Static properties/methods** belong to the class, not instances:

```php
class MathHelper {
    public static function square(int $x): int {
        return $x * $x;
    }
}

echo MathHelper::square(5);
```

* Good for utility methods and counters
* Do not use for instance-specific data

---

## Notes - Advanced

* Prefer private/protected over public properties for encapsulation
* Use getters and setters for controlled access and validation
* Use type hints for clarity and error prevention
* `$this` always refers to instance, `self` to class
* Constructors can accept parameters, and multiple constructors can be emulated using optional parameters
* Destructors are rarely needed but useful for cleanup (closing files, database connections)
* Understand the object lifecycle to prevent memory leaks and unexpected behavior
* Use static properties for shared data among all instances

---

## Summary of OOP Essentials

1. Class – blueprint
2. Object – instance
3. Properties – object data
4. Methods – object behavior
5. $this – current object
6. self – current class (static members)
7. Constructor – initialize object
8. Destructor – cleanup
9. Visibility – public, private, protected
10. Static – class-level members
11. Getters and Setters – controlled access
12. Type Hints – enforce data types
13. Object lifecycle – declaration, instantiation, usage, destruction

---

## Next Steps
Once you feel comfortable with these basics, move on to `02-encapsulation.md` to learn how to protect object data and write more robust OOP code.
