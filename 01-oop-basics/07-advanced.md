# Advanced OOP in PHP 

## Introduction

This file covers **advanced OOP concepts and techniques** in PHP, aimed at bridging the gap from junior to advanced levels. It builds on **Basics, Encapsulation, Inheritance, Polymorphism, Abstraction, and Notes**, and focuses on real-world practical applications.

---

## 1. Magic Methods

Magic methods in PHP start with `__` and allow you to define special behavior.

### Common Magic Methods

* `__construct()` - Object initialization
* `__destruct()` - Cleanup when object is destroyed
* `__get($name)` - Access undefined or private properties
* `__set($name, $value)` - Set undefined or private properties
* `__isset($name)` - Check if property exists
* `__unset($name)` - Unset a property
* `__call($method, $args)` - Handle calls to undefined methods
* `__callStatic($method, $args)` - Handle static undefined methods
* `__toString()` - String representation of an object
* `__invoke()` - Make object callable

```php
class Person {
    private array $data = [];

    public function __set($name, $value) {
        $this->data[$name] = $value;
    }

    public function __get($name) {
        return $this->data[$name] ?? null;
    }

    public function __toString() {
        return json_encode($this->data);
    }
}

$person = new Person();
$person->name = 'Ziad';
echo $person->name;
echo $person;
```

* Magic methods can **enhance flexibility** but should be used carefully for maintainability.

---

## 2. Late Static Binding (LSB)

* `static::` keyword allows referencing **called class instead of the defining class**

```php
class ParentClass {
    public static function who() {
        echo __CLASS__;
    }
    public static function test() {
        static::who();
    }
}

class ChildClass extends ParentClass {
    public static function who() {
        echo __CLASS__;
    }
}

ChildClass::test(); // Output: ChildClass
```

* Useful for **fluent interfaces, factory patterns, and inheritance chains**

---

## 3. Namespaces

* Organize code and avoid class name collisions

```php
namespace App\Models;
class User {}

namespace App\Controllers;
use App\Models\User;
$user = new User();
```

* Essential for **large applications and Laravel projects**

---

## 4. Type Declarations and Strict Types

* Enforce types for properties, parameters, and return values

```php
declare(strict_types=1);

class Calculator {
    public function add(int $a, int $b): int {
        return $a + $b;
    }
}
```

* Helps **catch errors early** and improves code quality

---

## 5. Dependency Injection (DI)

* Provide dependencies to a class instead of creating them inside

```php
class Mailer {
    public function send($message) {}
}

class UserService {
    public function __construct(private Mailer $mailer) {}
    public function notifyUser() {
        $this->mailer->send('Hello');
    }
}
```

* Enhances **testability** and **loose coupling**

---

## 6. Design Patterns (PHP Examples)

### Singleton

* Ensures only **one instance** of a class exists
* Provides **global access point** to that instance
* Sensitive points:

  * Prevent cloning (`__clone`) and unserialize (`__wakeup`)
  * Lazy initialization vs early initialization
  * Not ideal for **unit testing** or highly concurrent apps without careful design

```php
class Database {
    private static ?Database $instance = null;

    private function __construct() {}
    private function __clone() {}
    private function __wakeup() {}

    public static function getInstance(): Database {
        return self::$instance ??= new self();
    }
}
```

### Factory

* Encapsulates **object creation logic**
* Advantages:

  * Decouples client code from concrete classes
  * Can return different classes based on parameters

```php
interface Notification {
    public function send();
}

class EmailNotification implements Notification {
    public function send() { echo 'Email sent'; }
}

class NotificationFactory {
    public static function create($type): Notification {
        return match($type) {
            'email' => new EmailNotification(),
        };
    }
}
```

### Strategy

* Define a family of algorithms and make them interchangeable
* Advantages:

  * Behavior can be changed at runtime
  * Promotes **composition over inheritance**

```php
interface PaymentStrategy {
    public function pay(float $amount);
}

class CreditCardPayment implements PaymentStrategy {
    public function pay(float $amount) { echo "Paid $amount with Credit Card"; }
}

class PaymentContext {
    public function __construct(private PaymentStrategy $strategy) {}
    public function pay(float $amount) { $this->strategy->pay($amount); }
}
```

---

## 7. Advanced Notes and Best Practices

* Use **SOLID principles** consistently
* Combine **traits, interfaces, abstract classes** for flexible architecture
* Prefer **composition over deep inheritance chains**
* Use **magic methods** judiciously
* Leverage **namespaces** for large applications
* Type hint everything, enable **strict types**
* Apply **design patterns** where appropriate for maintainability and scalability
* Write code that is **readable, testable, and extendable**
* Be cautious with **Singleton**: global state can lead to hidden dependencies, threading issues, and testing difficulties
* **Factory** is more flexible and testable than Singleton for providing shared services
* Use **Strategy** to replace conditional logic and allow runtime behavior changes

---

## Summary

This advanced guide consolidates PHP OOP knowledge:

* Magic methods, LSB, namespaces, strict types
* Dependency injection for flexible architecture
* Common design patterns: Singleton, Factory, Strategy, with careful notes on pros/cons
* Advanced tips and best practices for writing **clean, scalable, maintainable PHP code**

---

## Next Steps

Use this knowledge as a reference when building real-world PHP projects, Laravel apps, and when applying **SOLID principles** and design patterns in your code.
