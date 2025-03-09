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

## Question 17: How to Handle Exceptions in Java?

**Java uses the `try-catch` block for exception handling.**  
- A `try` block must be followed by at least one `catch` or `finally` block.
- **You cannot write a `try` block alone.**

### Example:

```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // Throws ArithmeticException
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("Exception caught: " + e.getMessage());
        } finally {
            System.out.println("Finally block executed");
        }
    }
}
```

**Output:**
```
Exception caught: / by zero
Finally block executed
```

---

## Question 18: Can we write a `try` block without a `catch` block?

Yes, we **can** write a `try` block **with a `finally` block**, but we **cannot** write a `try` block alone.

### Example:

```java
public class TryFinallyExample {
    public static void main(String[] args) {
        try {
            System.out.println("Inside try block");
        } finally {
            System.out.println("Finally block executed");
        }
    }
}
```

**Output:**
```
Inside try block
Finally block executed
```

---

## Question 19: Handling Multiple Exceptions

Java provides **two ways** to handle multiple exceptions:
1. **Multiple `catch` blocks**
2. **Single `catch` block using the `|` (pipe) operator**

### Example: Using multiple `catch` blocks

```java
public class MultipleCatchExample {
    public static void main(String[] args) {
        try {
            int arr[] = new int[5];
            arr[10] = 50; // Throws ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index out of bounds: " + e.getMessage());
        } catch (ArithmeticException e) {
            System.out.println("Arithmetic Exception: " + e.getMessage());
        }
    }
}
```

### Example: Using `|` operator

```java
public class MultiCatchExample {
    public static void main(String[] args) {
        try {
            int number = Integer.parseInt("abc"); // Throws NumberFormatException
        } catch (NumberFormatException | NullPointerException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Exception caught: For input string: "abc"
```

---

## Question 20: When does the `finally` block **not** get executed?

- When **`System.exit()`** is called.
- When the **JVM crashes**.

---

## Question 21: Difference between `throw` and `throws` & Exception Propagation

### **`throw` vs `throws`**
| `throw`  | `throws`  |
|----------|----------|
| Used to **explicitly throw** an exception. | Used to **declare exceptions** in method signature. |
| Follows an **exception instance**. | Follows **exception class names**. |
| Only **one** exception can be thrown at a time. | Multiple exceptions can be declared. |

---

### **Exception Propagation**
- When a method throws an **unchecked exception**, it **propagates up** the call stack until it is caught.
- Checked exceptions **do not propagate automatically**; they must be handled or declared using `throws`.

### Example: **Unchecked Exception Propagation**

```java
public class UncheckedExceptionPropagation {
    static void m3() {
        throw new ArithmeticException("Exception thrown in m3");
    }
    static void m2() {
        m3();
    }
    static void m1() {
        m2();
    }
    public static void main(String[] args) {
        m1();
    }
}
```

**Output:**
```
Exception in thread "main" java.lang.ArithmeticException: Exception thrown in m3
```

---

### Example: **Handling Unchecked Exceptions**

```java
public class HandledUncheckedException {
    static void m3() {
        throw new ArithmeticException("Exception thrown in m3");
    }
    static void m2() {
        try {
            m3();
        } catch (ArithmeticException e) {
            System.out.println("Exception caught in m2: " + e.getMessage());
        }
    }
    static void m1() {
        m2();
    }
    public static void main(String[] args) {
        m1();
        System.out.println("Program continues...");
    }
}
```

**Output:**
```
Exception caught in m2: Exception thrown in m3
Program continues...
```

---

## Example: **Checked Exception Propagation (Handled with `throws`)**

```java
import java.io.*;

public class CheckedExceptionUsingThrows {
    static void m3() throws IOException {
        throw new IOException("Checked Exception in m3");
    }
    static void m2() throws IOException {
        m3();
    }
    static void m1() throws IOException {
        m2();
    }
    public static void main(String[] args) {
        try {
            m1();
        } catch (IOException e) {
            System.out.println("Exception handled in main: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Exception handled in main: Checked Exception in m3
```