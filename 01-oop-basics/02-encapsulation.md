# Encapsulation in PHP 

## Introduction

**Encapsulation** is one of the core principles of Object-Oriented Programming (OOP). It is the practice of **restricting direct access to some of an object's properties** and methods, and controlling it through specific interfaces like getters and setters.

The purpose is to **protect the object’s internal state**, **prevent unintended modifications**, and **provide a controlled way to interact with data**.

Encapsulation is often combined with **visibility modifiers**: `public`, `private`, and `protected`.

This file explains encapsulation in detail, with examples, best practices, and advanced notes.

---

## Why Encapsulation?

Without encapsulation:

* Any part of the code can modify object properties directly
* Leads to bugs and unexpected behavior
* Makes maintenance difficult

With encapsulation:

* You control access to data
* You can validate or process data before changing it
* The internal implementation can change without affecting external code

Example without encapsulation:

```php
class User {
    public string $name;
    public int $age;
}

$user = new User();
$user->name = '';
$user->age = -5; // invalid data, but no control
```

Problems:

* Invalid data can be assigned
* Other parts of the code directly manipulate properties

---

## Basic Encapsulation

Use **private or protected** properties and access them through **public getters and setters**.

```php
class User {
    private string $name;
    private int $age;

    public function setName(string $name) {
        if (empty($name)) {
            throw new Exception('Name cannot be empty');
        }
        $this->name = $name;
    }

    public function getName(): string {
        return $this->name;
    }

    public function setAge(int $age) {
        if ($age < 0 || $age > 120) {
            throw new Exception('Age must be between 0 and 120');
        }
        $this->age = $age;
    }

    public function getAge(): int {
        return $this->age;
    }
}

$user = new User();
$user->setName('Ahmed');
$user->setAge(25);
echo $user->getName();
echo $user->getAge();
```

Advantages:

* Data is validated before assignment
* Code outside the class cannot directly modify properties
* Implementation can change without affecting outside code

---

## Visibility Modifiers

Visibility controls **who can access properties and methods**.

* `public`: accessible from anywhere
* `private`: accessible only inside the class
* `protected`: accessible inside the class and subclasses

Example:

```php
class Account {
    public string $username;
    private string $password;
    protected float $balance;

    public function setPassword(string $pass) {
        $this->password = $pass;
    }

    protected function setBalance(float $amount) {
        $this->balance = $amount;
    }
}
```

* Public members can be accessed freely
* Private members are hidden from external code
* Protected members are hidden but accessible in child classes

---

## Advanced Getter and Setter Techniques

**Computed properties**: sometimes the getter returns a value calculated from other properties.

```php
class Rectangle {
    private float $width;
    private float $height;

    public function setWidth(float $width) {
        $this->width = $width;
    }

    public function setHeight(float $height) {
        $this->height = $height;
    }

    public function getArea(): float {
        return $this->width * $this->height;
    }
}

$rect = new Rectangle();
$rect->setWidth(5);
$rect->setHeight(10);
echo $rect->getArea();
```

* Area is computed, not stored
* Users cannot set invalid area directly

**Chaining setters**: allows multiple setter calls in one statement

```php
class User {
    private string $name;
    private int $age;

    public function setName(string $name): self {
        $this->name = $name;
        return $this;
    }

    public function setAge(int $age): self {
        $this->age = $age;
        return $this;
    }
}

$user = (new User())->setName('Ahmed')->setAge(25);
```

---

## Notes - Advanced

* Prefer **private** properties to **public** ones
* Use **getters and setters** even if no validation is needed (future-proofing)
* Getter/setter methods can implement logic: validation, transformation, or logging
* Keep methods focused; do not add unrelated behavior
* Encapsulation supports **SOLID principles**, especially Single Responsibility and Open/Closed
* You can also use **readonly properties** in PHP 8.1+ for immutable data

---

## Summary

* Encapsulation = hiding internal state + controlling access
* Use private/protected properties
* Provide public getters/setters
* Validate or compute data inside these methods
* Improves code maintainability, scalability, and safety
* Supports clean architecture and SOLID principles

---

## Next Steps

After mastering encapsulation, proceed to:

* `03-inheritance.md` to understand code reuse through parent/child relationships
* `04-polymorphism.md` for flexible, interchangeable objects
