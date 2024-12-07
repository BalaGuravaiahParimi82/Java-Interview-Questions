## Question 1: What are the 4 pillars of OOPS?
<details>
  <summary>View Answer</summary>
  
 ##### 4 pillars of OOPS are:

  1. **Abstraction**: Abstraction is a process of hiding the implementation details and showing only functionality to the user.

     Real world examples:
     - **TV remote**: To start the TV, you have to press the power button, you don't have to know about the internal circuit operations like how infrared waves are passing.
     - **Car gears**: We know what happens when we change the gear. But we don't know how changing gear works under the hood, that information is irrelevant to us, so it is abstracted.

     In Java, Abstraction can be achieved in two ways:
     - Abstract classes
     - Interfaces

  2. **Encapsulation**: Encapsulation is a process of **`Binding data and methods within a class`**</ins>. Think of it like showing the essential details of a class by using the access control modifiers (*public, private, protected*). So, we can say that Encapsulation leads to the desired level of Abstraction.

     Example:
     - **`Java Bean`**, where all data members are made private and you define certain public methods to the outside world to access them.

  3. **Inheritance**: Using inheritance means defining a **`parent-child relationship between classes`**, by doing so, you can reuse the code that is already defined in the parent class. Code reusability is the biggest advantage of Inheritance.

     Java does not allow multiple inheritance through classes but it allows it through interfaces.

  4. **Polymorphism**: Poly means many and Morph means forms. Polymorphism is the process in which an object or function takes different forms.

     There are 2 types of Polymorphism:
     - **Compile Time Polymorphism** (Method Overloading)
     - **Run Time Polymorphism** (Method Overriding)

     In <ins>Method Overloading</ins>, two or more methods in one class have the `same method name but different arguments.` It is called *Compile-time polymorphism* because it is decided at compile time which overloaded method will be called.

     <ins>Method Overriding</ins> means when we have two methods with the `same name and same parameters in the parent and child class`. Through overriding, the child class can provide specific implementation for the method already defined in the parent class.

</details>


---


## Question 2: What is an abstract class?
<details>
  <summary>View Answer</summary>
  
  ##### An abstract class is:

  A class that is declared using the **`abstract`** keyword. It can have **abstract methods** (methods without a body) as well as **concrete methods** (methods with a body).

  **Main points to remember:**

  - **`An abstract class cannot be instantiated`**: You cannot create an object of the abstract class. It has no use unless extended by another class.

  - **`If there is any abstract method in a class`**, the class must be declared **abstract**.

  - **`The first non-abstract class`** that extends from an abstract class must provide the implementation of the abstract methods defined in the abstract class.

 *Example:*

This is an example of an abstract class `MyAbstractClass` with an abstract method `print()` and a concrete method `display()`.

```java
package com.tech;

public abstract class MyAbstractClass {
	
    // abstract method
    abstract void print();
	
    public void display() {
        System.out.println("In display method");
    }
}
```

This is an example of an `AbstractDemo` class that extends an abstract class and overrides its methods.

```java
package com.tech;

public class AbstractDemo extends MyAbstractClass {
	
    void print() {
        System.out.println("In Print method");
    }
	
    public static void main(String[] args) {
        AbstractDemo obj = new AbstractDemo();
        obj.print();
        obj.display();
    }
}
```

---

hij
