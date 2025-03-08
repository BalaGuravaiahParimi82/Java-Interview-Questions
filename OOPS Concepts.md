# 4 Pillars of OOPS

## Question 1: What are the 4 pillars of OOPS?

### Answer: The 4 pillars of OOPS are:
1. Abstraction
2. Encapsulation
3. Inheritance
4. Polymorphism

---

## 1. Abstraction
Abstraction is the process of hiding the implementation details and showing only functionality to the user.

### Real-world examples:
- **TV Remote:** To start the TV, you press the power button. You don’t need to know about the internal circuit operations like how infrared waves are passing.
- **Car Gears:** We know what happens when we change the gear, but we don’t know how the mechanism works internally. That information is abstracted from us.

### In Java, Abstraction can be achieved in two ways:
- **Abstract classes**
- **Interfaces**

---

## 2. Encapsulation
Encapsulation is the process of binding data and methods within a class. It ensures that essential details of a class are controlled using access modifiers (**public, private, protected**). This leads to the desired level of Abstraction.

### Example:
A **Java Bean**, where all data members are made `private` and public methods are provided to access them.

---

## 3. Inheritance
Inheritance defines a **parent-child relationship** between classes, enabling code reuse. The child class inherits properties and behaviors from the parent class.

### Key Points:
- **Code reusability** is the biggest advantage of Inheritance.
- Java does not support **multiple inheritance** through classes but allows it through **interfaces**.

---

## 4. Polymorphism
Polymorphism means "many forms." It allows an object or function to take different forms.

### Types of Polymorphism:
1. **Compile-Time Polymorphism (Method Overloading)**
   - Method overloading occurs when two or more methods in a class have the **same method name** but **different arguments**.
   - The method to be called is decided at **compile-time**.

2. **Run-Time Polymorphism (Method Overriding)**
   - Overriding happens when a **child class** provides a specific implementation for a method that is already defined in the **parent class**.
   - The method call is resolved at **runtime**.

---

## Question 2: What is an abstract class?

### Answer:
A class that is declared using the `abstract` keyword is known as an **abstract class**. It can have both **abstract methods** (methods without a body) and **concrete methods** (methods with a body).

### Key Points to Remember:
- An **abstract class cannot be instantiated**, meaning you cannot create an object of an abstract class.
  - This also means an abstract class has no use unless it is **extended** by some other class.
- If there is any **abstract method** in a class, then that class **must be declared abstract**.
- The first **non-abstract class** that extends an abstract class **must provide implementations** for all abstract methods defined in the abstract class.

### Example Code:
```java
package com.tech;

abstract class MyAbstractClass {
    // Abstract method
    abstract void print();
    
    // Concrete method
    public void display() {
        System.out.println("In display method");
    }
}

public class AbstractDemo extends MyAbstractClass {

    @Override
    void print() {
        System.out.println("In print method");
    }

    public static void main(String[] args) {
        AbstractDemo obj = new AbstractDemo();
        obj.print();
        obj.display();
    }
}
```
### Output:
```
In print method  
In display method  
```

---

## Question 3: Does an Abstract class have a constructor?

### Answer:
Yes, abstract classes have constructors. You can either provide one explicitly or Java will provide a default constructor.

### Why do abstract classes need constructors?
Although you cannot create an object of an abstract class, **constructors are used to initialize data members** when a child class extends the abstract class.

When an abstract class is extended, its constructor is invoked when an object of the subclass is created. The first line of a subclass constructor always calls the **superclass constructor**, ensuring proper initialization.

### Example Code:
```java
package com.tech;

// Abstract class with parameterized constructor
abstract class MyAbstractClass {
    public int a;
    public int b;

    public MyAbstractClass(int a, int b) {
        this.a = a;
        this.b = b;
    }

    public void print() {
        System.out.println("a = " + a);
        System.out.println("b = " + b);
    }
}

// Concrete subclass
public class AbstractDemo extends MyAbstractClass {
    
    public AbstractDemo(int x, int y) {
        super(x, y);  // Explicit call to superclass constructor
    }

    public static void main(String[] args) {
        AbstractDemo obj = new AbstractDemo(5, 10);
        obj.print();
    }
}
```
### Output:
```
a = 5  
b = 10  
```

---

## Question 5: Difference between Abstract Class and Interface

### Answer:
| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Methods | Can have both abstract and concrete methods | Can only have abstract methods (except Java 8+ which allows default & static methods) |
| Access Modifiers | Can have any access modifier | Methods are implicitly public and abstract |
| Variables | Can have final, non-final, static, and non-static variables | Variables are always static and final |
| Inheritance | A class can extend only one abstract class | A class can implement multiple interfaces |
| Extending & Implementing | Can extend another class and implement multiple interfaces | Can only extend other interfaces |

---

## Question 6: What to choose – Interface or Abstract Class?

### Answer:
- Use **abstract class** when you want to provide **default implementations** of methods that subclasses can directly use.
- Use **interfaces** when your **contract keeps changing** to avoid forcing changes on implementing classes.
- **Best practice:** Prefer **interfaces** in most cases.

---

## Question 7: Why was Java 8 introduced default methods?

### Answer:
Default methods were introduced in Java 8 to allow adding new methods to interfaces **without breaking existing implementations**.

### Example Scenario:
- If 100 classes implement an interface and a new method is added, all 100 classes would need modification.
- With **default methods**, the new method can have a default implementation, avoiding the need for updates in all classes.

### Diamond Problem:
If two interfaces define the same **default method**, a class implementing both must override the method to resolve ambiguity.

## Question: How does Java handle the Diamond Problem with default methods?

### Answer:
When two interfaces have default methods with the same name, and a class implements both interfaces **without overriding the method**, Java will throw a compilation error due to ambiguity. To resolve this, the implementing class must **explicitly override the conflicting method** and specify which interface's method to call.

### Example Code:
```java
interface Interface1 {
    default void hello() {
        System.out.println("Hello from Interface1");
    }
}

interface Interface2 {
    default void hello() {
        System.out.println("Hello from Interface2");
    }
}

public class Child implements Interface1, Interface2 {
    
    @Override
    public void hello() {
        System.out.println("inside Child class hello method");
        Interface1.super.hello();  // Explicitly call Interface1's implementation
    }

    public static void main(String[] args) {
        Child obj = new Child();
        obj.hello();
    }
}
```

### Output:
```
inside Child class hello method  
Hello from Interface1  
```

### Explanation:
- **`Interface1` and `Interface2`** both define a default method `hello()`.
- **`Child` class implements both interfaces**, leading to a potential conflict.
- **To resolve the ambiguity**, `Child` class **overrides `hello()`** and explicitly calls `Interface1.super.hello()` to specify which implementation to use.

By overriding the method, the Diamond Problem is resolved in Java.

## Question 8: Why Java 8 has introduced static methods?

### Answer:
Before Java 8, utility methods were typically placed in classes with static methods, such as `Collections` or `Math`. However, Java 8 introduced **static methods in interfaces** to allow utility methods to be defined directly within interfaces.

### Benefits of Static Methods in Interfaces:
- **Better Organization:** Utility methods related to an interface can be directly placed inside the interface rather than an unrelated helper class.
- **Performance Optimization:** Using an interface with static methods is more efficient than creating a separate utility class.
- **No Need for Implementation:** Unlike default methods, static methods do not require implementation in implementing classes.

### Example Code:
```java
interface UtilityInterface {
    static void show() {
        System.out.println("Static method in Interface");
    }
}

public class StaticMethodDemo {
    public static void main(String[] args) {
        UtilityInterface.show(); // Calling static method from interface
    }
}
```

### Output:
```
Static method in Interface  
```

This allows defining utility methods directly in interfaces without requiring an implementing class, improving modularity and design flexibility.

## Question 9: Why Java does not allow multiple inheritance?

### Answer:
Multiple inheritance occurs when a class has more than one parent class.

### Why Java does not allow this?
Let us consider there are two parent classes having a method named `hello()` with the same signature, and one child class extends these two classes. If you call this `hello()` method, which is present in both parents, it results in ambiguity—this is called the **Diamond Problem**.

If you try to extend more than one class in Java, you will get a **compile-time error**.

---

## Example Code:

```java
class Parent1 {
    public void hello() {
        System.out.println("Hello from Parent1 class");
    }
}

class Parent2 {
    public void hello() {
        System.out.println("Hello from Parent2 class");
    }
}

// Java does NOT support multiple class inheritance
public class Child extends Parent1 /* Syntax error here: cannot extend Parent2 */ {
    // Error: Java only allows single class inheritance
}
```

### Explanation:
- Since both `Parent1` and `Parent2` have a method with the same signature, Java does not allow the `Child` class to extend both.
- This restriction prevents ambiguity and makes Java **more maintainable and predictable**.

---

## Question 10: What are the rules for Method Overloading and Method Overriding?

### Answer:

## Method Overloading Rules:
Two methods can be called overloaded if they follow the rules below:
- **Both must have the same method name.**
- **Both must have different arguments.**

If both methods follow the above two rules, then they **may or may not**:
- Have different access modifiers.
- Have different return types.
- Throw different checked or unchecked exceptions.

---

## Method Overriding Rules:
The overriding method of a child class must follow the rules below:
- It must have the **same method name** as that of the parent class method.
- It must have the **same arguments** as that of the parent class method.
- It must have **either the same return type or a covariant return type** (child classes are covariant types to their parents).
- It must not throw **broader checked exceptions** than the parent method.
- It must not have a **more restrictive access modifier** (if the parent method is `public`, then the child method **cannot** be `private` or `protected`).

## Question 11: Can we override final methods?

### Answer:
No, final methods cannot be overridden.

---

## Question 12: Can constructors and private methods be overridden?

### Answer:
No.

---

## Question 13: What is the final keyword and where can it be used?

### Answer:
- If you use `final` with a **primitive type variable**, then its value cannot be changed once assigned.
- If you use `final` with a **method**, then you cannot override it in the subclass.
- If you use `final` with a **class**, then that class cannot be extended.
- If you use `final` with an **object type**, then that object cannot be referenced again.
