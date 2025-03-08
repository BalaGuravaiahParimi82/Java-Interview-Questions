# 📘 Grokking The Java Developer Interview

> **More Than 200 Questions To Crack The Java, Spring, Spring Boot & Hibernate Interview**

## 📝 Table of Contents
- [Introduction](#introduction)
- [OOP Concepts](#oop-concepts)
- [Java Basics](#java-basics)
- [Exception Handling](#exception-handling)
- [Strings](#strings)
- [Collections & Generics](#collections--generics)
- [Multithreading](#multithreading)
- [Spring & Spring Boot](#spring--spring-boot)
- [JPA & Hibernate](#jpa--hibernate)
- [SQL & Database](#sql--database)
- [References](#references)

---

## 📌 Introduction
Grokking The Java Developer Interview helps you to crack Java, Spring & Hibernate interviews.

This book covers frequently asked Java interview questions, including topics like **multithreading, collections, design patterns, Spring Boot annotations, and more**, with detailed explanations and code examples.

## 📚 OOP Concepts

### 🔹 Question 1: What are the 4 pillars of OOPS?
**Answer:**
1. **Abstraction** - Hiding implementation details and exposing functionality.
   - Example: TV remote hides internal circuit operations.
2. **Encapsulation** - Wrapping data and methods together.
   - Example: Java Beans with private fields and public getters/setters.
3. **Inheritance** - Acquiring properties of parent class.
   - Example: `class Dog extends Animal {}`
4. **Polymorphism** - One interface, multiple implementations.
   - Example: Method Overloading & Overriding.

### 🔹 Question 2: What is an abstract class?
**Answer:**
An `abstract` class in Java **cannot be instantiated** and can contain **both abstract (without body) and concrete methods**.

```java
abstract class Animal {
    abstract void makeSound();
    void sleep() { System.out.println("Sleeping..."); }
}
class Dog extends Animal {
    void makeSound() { System.out.println("Bark"); }
}
```

---

## 🔹 Java Basics

### 🔹 Question 3: What is an interface?
**Answer:**
- An interface is a blueprint of a class, containing only **abstract methods** (before Java 8).
- After Java 8, interfaces can have **default and static methods**.
- Example:

```java
interface Vehicle {
    void start();
    default void honk() { System.out.println("Beep Beep!"); }
}
class Car implements Vehicle {
    public void start() { System.out.println("Car starting..."); }
}
```

### 🔹 Question 4: What is the difference between abstract class and interface?
| Feature           | Abstract Class | Interface |
|------------------|---------------|------------|
| Methods         | Can have both abstract & concrete methods | Only abstract methods (until Java 8) |
| Multiple Inheritance | No | Yes |
| Variables       | Can have instance variables | Only `public static final` constants |

---

## 🔥 Exception Handling

### 🔹 Question 5: What is an exception and how is it handled?
**Answer:**
An **exception** is an event that disrupts the normal flow of execution. It is handled using `try-catch-finally` blocks.

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero!");
} finally {
    System.out.println("Execution completed.");
}
```

### 🔹 Question 6: What is the difference between `throw` and `throws`?
| Keyword  | Usage |
|----------|--------|
| `throw`  | Used to explicitly throw an exception |
| `throws` | Declares exceptions in a method signature |

```java
void checkAge(int age) throws IllegalArgumentException {
    if (age < 18) throw new IllegalArgumentException("Underage!");
}
```

---

## 📌 Strings

### 🔹 Question 7: Why is `String` immutable in Java?
**Answer:**
- **String Pool** - If a string is modified, a new object is created.
- **Security** - Used in database connections, class loading.
- **Thread Safety** - Multiple threads can share the same string without synchronization.

```java
String s1 = "Hello";
String s2 = "Hello";
System.out.println(s1 == s2); // true (same reference)
```

### 🔹 Question 8: Difference between `StringBuilder` and `StringBuffer`?
| Feature         | StringBuilder | StringBuffer |
|---------------|--------------|--------------|
| Mutability   | Mutable | Mutable |
| Thread-Safe  | No | Yes |
| Performance  | Faster | Slower |

---

## 🔄 Collections & Generics

### 🔹 Question 9: What is the difference between `ArrayList` and `LinkedList`?
| Feature    | ArrayList | LinkedList |
|------------|----------|------------|
| Storage    | Dynamic Array | Doubly Linked List |
| Insertion  | Slow | Fast |
| Access     | Fast | Slow |

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
```

---

## 🔀 Multithreading

### 🔹 Question 10: How do you create a thread in Java?
**Answer:**
Two ways:
1. Extend `Thread` class.
2. Implement `Runnable` interface.

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running...");
    }
}
new MyThread().start();
```

---

## ☕ Spring & Spring Boot

### 🔹 Question 11: What is Dependency Injection?
**Answer:**
DI is a design pattern that allows objects to receive dependencies instead of creating them.

```java
@Service
class ServiceA {
    @Autowired
    private RepositoryA repo;
}
```

---

## 🔗 JPA & Hibernate

### 🔹 Question 12: What is Hibernate?
**Answer:**
- Hibernate is an ORM (Object-Relational Mapping) framework.
- It allows mapping Java objects to database tables using annotations.

```java
@Entity
class Employee {
    @Id @GeneratedValue
    private Long id;
}
```

---

## 📂 SQL & Database

### 🔹 Question 13: What is the difference between `DELETE` and `TRUNCATE`?
| Feature  | DELETE | TRUNCATE |
|----------|--------|----------|
| Rollback | Yes | No |
| Speed    | Slow | Fast |

---

## 📖 References
- [Java Docs](https://docs.oracle.com/javase/8/docs/)
- [Spring Boot Guide](https://spring.io/guides)
- [Effective Java](https://www.pearson.com/en-us/subject-catalog/p/effective-java/P200000003570/9780134685991)
