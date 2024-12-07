Question 1: What are the 4 pillars of OOPS?
The 4 pillars of OOPS are:

Abstraction
Abstraction is a process of hiding the implementation details and showing only functionality to the user.

Real-world examples:

TV remote: To start the TV, you have to press the power button. You don’t have to know about the internal circuit operations, like how infrared waves are passing.
Car gears: We know what happens when we change the gear, but we don’t know how changing gear works under the hood. That information is irrelevant to us, so it is abstracted.
In Java, Abstraction can be achieved in two ways:

Abstract classes
Interfaces
Encapsulation
Encapsulation is a process of binding data and methods within a class. Think of it as showing the essential details of a class by using access control modifiers (public, private, protected).

Example:
A Java Bean, where all data members are made private and you define certain public methods to the outside world to access them.

Encapsulation leads to the desired level of Abstraction.

Inheritance
Inheritance defines a parent-child relationship between classes. By doing so, you can reuse the code that is already defined in the parent class.

Advantage: Code reusability is the biggest benefit of Inheritance.

Java Restriction:
Java does not allow multiple inheritance through classes but allows it through interfaces.

Polymorphism
Poly means many, and Morph means forms. Polymorphism is the process in which an object or function takes different forms.

Types of Polymorphism:

Compile-Time Polymorphism (Method Overloading): Two or more methods in one class have the same name but different arguments. It is decided at compile time which overloaded method will be called.
Run-Time Polymorphism (Method Overriding): When we have two methods with the same name and parameters in parent and child classes. Through overriding, the child class can provide a specific implementation for a method already defined in the parent class.
