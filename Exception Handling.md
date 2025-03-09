# Exception Handling in Java

## Question 1: What is an Exception and Exception Handling?

### Answer:
An **exception** is an event that **disrupts** the normal flow of a program. It is an **object** that is thrown at runtime.  
**Exception Handling** is the process of **managing** these exceptions to ensure the program continues to run smoothly.

---

### Example: Exception being thrown

```java
public class ExceptionExample {
    public static void main(String[] args) {
        int result = 10 / 0;  // Throws ArithmeticException
        System.out.println("Result: " + result);
    }
}
```

**Output:**
```
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at ExceptionExample.main(ExceptionExample.java:3)
```

---

### Example: Exception Handling using `try-catch`

```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;  // Throws ArithmeticException
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
        System.out.println("Program continues...");
    }
}
```

**Output:**
```
Exception caught: / by zero
Program continues...
```

---

## Question 15: Difference between **Error** and **Exception**

### **Error:**
- **Irrecoverable** and indicates serious issues.
- Causes program **termination**.
- **Examples:**  
  - `OutOfMemoryError` (Running out of memory)
  - `StackOverflowError` (Excessive recursion)

### **Exception:**
- **Recoverable** using **exception handling**.
- **Examples:**  
  - `NullPointerException` (Accessing methods on `null`)
  - `ArithmeticException` (Division by zero)

---

## Question 16: Types of Exceptions

### **1. Checked Exceptions**  
- Enforced by the **compiler** at **compile-time**.  
- **Examples:** `IOException`, `SQLException`, `FileNotFoundException`

### **2. Unchecked Exceptions**  
- Occur at **runtime** and are **not checked** by the compiler.  
- **Examples:** `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`

---

## Question 22: Exception Handling with Method Overriding

### **Rules:**
1. **If the parent class method does not declare an exception, the child class cannot throw a checked exception.**
   
   ```java
   class Parent {
       public void hello() {
           System.out.println("Parent class hello method");
       }
   }

   class Child extends Parent {
       public void hello() throws IOException { // ❌ Compilation Error
           System.out.println("Child class hello method");
       }
   }
   ```

   **Error:**
   ```
   Exception IOException is not compatible with throws clause in Parent.hello()
   ```

2. **A child class can throw an unchecked exception even if the parent class method does not declare one.**

   ```java
   class Parent {
       public void hello() {
           System.out.println("Parent class hello method");
       }
   }

   class Child extends Parent {
       public void hello() throws ArithmeticException { // ✅ Allowed
           System.out.println("Child class hello method");
       }
   }

   public class TestException {
       public static void main(String[] args) {
           Parent p = new Child();
           p.hello();
       }
   }
   ```

   **Output:**
   ```
   Child class hello method
   ```

3. **If a child class method throws a broader exception than the parent class method, it results in a compilation error.**

   ```java
   class Parent {
       public void hello() throws ArithmeticException {
           System.out.println("Parent class hello method");
       }
   }

   class Child extends Parent {
       public void hello() throws Exception { // ❌ Compilation Error
           System.out.println("Child class hello method");
       }
   }
   ```

   **Error:**
   ```
   Exception Exception is not compatible with throws clause in Parent.hello()
   ```

4. **A child class can throw the same exception as the parent class.**

   ```java
   class Parent {
       public void hello() throws Exception {
           System.out.println("Parent class hello method");
       }
   }

   class Child extends Parent {
       public void hello() throws Exception { // ✅ Allowed
           System.out.println("Child class hello method");
       }
   }

   public class TestException {
       public static void main(String[] args) {
           Parent p = new Child();
           try {
               p.hello();
           } catch (Exception e) {
               System.out.println("Handled");
           }
       }
   }
   ```

   **Output:**
   ```
   Child class hello method
   ```

5. **A child class method can declare a narrower exception than the parent class method.**

   ```java
   import java.io.IOException;

   class Parent {
       public void hello() throws Exception {
           System.out.println("Parent class hello method");
       }
   }

   class Child extends Parent {
       public void hello() throws IOException { // ✅ Allowed
           System.out.println("Child class hello method");
       }
   }

   public class TestException {
       public static void main(String[] args) {
           Parent p = new Child();
           try {
               p.hello();
           } catch (Exception e) {
               System.out.println("Handled");
           }
       }
   }
   ```

   **Output:**
   ```
   Child class hello method
   ```

6. **If the parent class method declares an exception, the child class can override it without declaring an exception.**

   ```java
   class Parent {
       public void hello() throws Exception {
           System.out.println("Parent class hello method");
       }
   }

   class Child extends Parent {
       public void hello() { // ✅ Allowed (No exception)
           System.out.println("Child class hello method");
       }
   }

   public class TestException {
       public static void main(String[] args) {
           Parent p = new Child();
           try {
               p.hello();
           } catch (Exception e) {
               System.out.println("Handled");
           }
       }
   }
   ```

   **Output:**
   ```
   Child class hello method
   ```

---

This document provides a comprehensive understanding of **exception handling in Java**, including **try-catch, multiple exceptions, exception propagation, and method overriding rules**.  
Let me know if you need any modifications!