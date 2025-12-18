# Dependency Inversion Principle (DIP) 

## Introduction

The **Dependency Inversion Principle (DIP)** states that:

1. High-level modules should not depend on low-level modules. Both should depend on abstractions.
2. Abstractions should not depend on details. Details should depend on abstractions.

DIP is about **decoupling your code** to make it flexible, maintainable, and testable.

---

## Why DIP is Important

* Reduces **tight coupling** between high-level and low-level code
* Improves **code flexibility and testability**
* Makes it easy to **swap implementations** without changing high-level modules
* Encourages use of **interfaces and abstractions**

---

## Problem Example Violating DIP

```php
class FileLogger {
    public function log(string $message) {
        echo "Logging to file: $message";
    }
}

class UserService {
    private FileLogger $logger;

    public function __construct() {
        $this->logger = new FileLogger();
    }

    public function createUser(string $name) {
        // create user logic
        $this->logger->log("User $name created");
    }
}
```

**Problems:**

* `UserService` is tightly coupled to `FileLogger`
* Cannot easily swap `FileLogger` with another logging method (e.g., `DatabaseLogger`)
* Violates DIP because high-level module depends on low-level module directly

---

## Solution With DIP

Depend on **abstractions (interfaces)** instead of concrete implementations:

```php
interface Logger {
    public function log(string $message);
}

class FileLogger implements Logger {
    public function log(string $message) {
        echo "Logging to file: $message";
    }
}

class DatabaseLogger implements Logger {
    public function log(string $message) {
        echo "Logging to database: $message";
    }
}

class UserService {
    public function __construct(private Logger $logger) {}

    public function createUser(string $name) {
        // create user logic
        $this->logger->log("User $name created");
    }
}

// Usage
$fileLogger = new FileLogger();
$userService = new UserService($fileLogger);
$userService->createUser('Ziad');
```

**Benefits:**

* `UserService` now depends on `Logger` interface, **not a concrete class**
* Easy to switch loggers without modifying `UserService`
* Code is **flexible, testable, and maintainable**

---

## When to Use DIP

* When high-level modules rely on low-level details
* When you want **swappable implementations** without changing the main code
* Always combine with **dependency injection** for best results

---

## Practical Tips

* Prefer **interfaces or abstract classes** for high-level module dependencies
* Inject dependencies via **constructor injection**
* Avoid instantiating concrete classes inside high-level modules
* Combine DIP with **OCP and SRP** to maintain clean, scalable architecture

---

## Summary

* DIP decouples **high-level modules from low-level modules**
* Relies on **abstractions, not concrete implementations**
* Enables **flexible, maintainable, and testable code**
* Works best when combined with **dependency injection, OCP, and SRP**

---

