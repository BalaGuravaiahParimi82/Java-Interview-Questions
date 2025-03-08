# Exception Handling

## Question 1: What is exception and exception handling?

## Answer:
An exception is an event that disrupts the normal flow of the program. It is an object that is thrown at runtime, so exception handling is a mechanism by which the normal flow of the program is maintained.

---

### Program showing the exception being thrown:

```java
public class ExceptionExample {
    public static void main(String[] args) {
        int result = 10 / 0;  // This will throw ArithmeticException
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

### Program demonstrating exception handling:

```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;  // This will throw ArithmeticException
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
## Question 15: Difference between Error and Exception

### Answer:

**Error:**
Errors in a program are irrecoverable; they indicate that something severe has gone wrong in the application, causing the program to terminate. Examples include:

- Running out of memory: `OutOfMemoryError`
- Making too many recursive calls: `StackOverflowError`

**Exception:**
Exceptions, on the other hand, are issues that we can recover from by handling them properly. Examples include:

- Trying to access a property/method from a null object: `NullPointerException`
- Dividing an integer by zero: `ArithmeticException`

## Question 16: What are the different types of exceptions?

### Answer:
There are two types of exceptions:

- **Checked Exceptions:** All exceptions other than `RuntimeException` and `Error` are known as Checked Exceptions. These exceptions are checked by the compiler at compile time.
  
  **Example:** When trying to read from a file, the compiler enforces handling of `FileNotFoundException` because the file may not exist. Some other checked exceptions are `SQLException`, `IOException`, etc.

- **Unchecked Exceptions:** Runtime Exceptions are known as Unchecked Exceptions. The compiler does not force us to handle these exceptions, but as a programmer, it is our responsibility to handle them properly.
  
  **Example:** `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`, etc.

---

## Question 17: How is exception handling done in Java?

### Answer:
Exception handling in Java is done using a `try-catch` block. If certain statements may throw an exception, they should be surrounded with a `try` block.

- A `try` block is always followed by either a `catch` block, a `finally` block, or both.
- You **cannot** use a `try` block alone.

#### Example:
```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // This will throw ArithmeticException
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

## Question 18: Can we write a try block without a catch block?

### Answer:
Yes, we can write a `try` block with a `finally` block, but we **cannot** write a `try` block alone.

#### Example:
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

## Question 19: How to handle multiple exceptions together?

### Answer:
You can handle multiple exceptions in Java using:
1. **Multiple catch blocks**
2. **Single catch block with multiple exception types using a pipe (|) symbol**

### Example using multiple catch blocks:
```java
public class MultipleCatchExample {
    public static void main(String[] args) {
        try {
            int arr[] = new int[5];
            arr[10] = 50; // This will throw ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index out of bounds: " + e.getMessage());
        } catch (ArithmeticException e) {
            System.out.println("Arithmetic Exception: " + e.getMessage());
        }
    }
}
```

### Example using pipe `|` operator:
```java
public class MultiCatchExample {
    public static void main(String[] args) {
        try {
            int number = Integer.parseInt("abc"); // This will throw NumberFormatException
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

## Question 20: When finally block will not get executed

## Answer:
- When `System.exit()` is called.
- When JVM crashes.

---

## Question 21: Difference between throw and throws keyword. And discuss Exception Propagation

## Answer:
- `throw` is a keyword which is used to explicitly throw an exception in the program, inside a function or inside a block of code, whereas `throws` is a keyword which is used with the method signature to declare an exception which might get thrown by the method while executing the code.
- `throw` keyword is followed by an instance of an Exception class whereas `throws` is followed by Exception class names.
- You can throw one exception at a time but you can declare multiple exceptions using the `throws` keyword.
- Using `throw` keyword, only unchecked exceptions are propagated, whereas using `throws` keyword both checked and unchecked exceptions can be propagated.

### Exception Propagation:
An exception is first thrown from the top of the stack and if it is not caught, it drops down the call stack to the previous method. If not caught there, the exception again drops down to the previous method, and so on until they are caught or until they reach the very bottom of the call stack. This is called **exception propagation**.

- When method `m1()` calls method `m2()` which calls method `m3()`, a stack is formed which gets unfolded from the top. If method `m3()` throws an exception and it is not handled there, it will drop down the call stack to method `m2()`. If it is not handled there, it will drop down the call stack to method `m1()`. This happens until we reach the bottom of the stack or until the exception is caught.

---

## Example: Unchecked exception is thrown and it can be seen from the call stack that it is propagated

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
    at UncheckedExceptionPropagation.m3(UncheckedExceptionPropagation.java:4)
    at UncheckedExceptionPropagation.m2(UncheckedExceptionPropagation.java:7)
    at UncheckedExceptionPropagation.m1(UncheckedExceptionPropagation.java:10)
    at UncheckedExceptionPropagation.main(UncheckedExceptionPropagation.java:13)
```

---

## Example: Here the unchecked exception is handled

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

## Example: Checked exceptions are not propagated down the call chain by default

```java
import java.io.*;
public class CheckedExceptionPropagation {
    static void m3() throws IOException {
        throw new IOException("Checked Exception in m3");
    }
    static void m2() {
        try {
            m3();
        } catch (IOException e) {
            System.out.println("Exception caught in m2: " + e.getMessage());
        }
    }
    public static void main(String[] args) {
        m2();
        System.out.println("Program continues...");
    }
}
```

**Output:**
```
Exception caught in m2: Checked Exception in m3
Program continues...
```

---

## Example: Using `throws` keyword to propagate checked exceptions

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

---

## Example: Using `throws` with unchecked exceptions (though it is of no use since they are propagated by default)

```java
public class ThrowsUncheckedException {
    static void m3() throws ArithmeticException {
        throw new ArithmeticException("Unchecked Exception in m3");
    }
    static void m2() throws ArithmeticException {
        m3();
    }
    static void m1() throws ArithmeticException {
        m2();
    }
    public static void main(String[] args) {
        try {
            m1();
        } catch (ArithmeticException e) {
            System.out.println("Exception caught in main: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Exception caught in main: Unchecked Exception in m3
```
