### What is Object Oriented Programming language ?

**Object-Oriented-Programming** is a programming approach using where everything is treated as **Objects** which consists of **State** in the form of attributes and **Behavior** in the form of methods. The key concepts of OOP includes: 

1. Class
2. Object
3. Inheritance
4. Encapsulation
5. Polymorphism
6. Abstraction

## Class

Class is not a real-world entity. It is just a template or blueprint or prototype from which objects are created. A Class is a group of variables of different data types and a group of methods. We can also say that a Class is a user-defined data type. Also, it does not occupy any memory.

It is composed of name, attributes, and methods. Access Modifiers ( `public` , `private` , `default` , `protected` ) are used for having limited or public access to that class so that it can be used by other programs in Java.

---
## Object

An object is an instance of a Java class, which has its own identity, behavior, and state. Basically, an object is created using the new keyword and the state of an object is stored in a variable, whereas the behavior of an object is displayed using functions (methods).

---
## Inheritance

**Inheritance** is a fundamental concept of Object-Oriented Programming (OOP) using which a Java class can inherit the fields and methods of another Java class. It helps in reusing code from related classes, thereby reducing the need to write a lot of boilerplate code. The class that is inherited is called the **parent (or superclass)**, and the class that inherits is called the **child (or subclass)**. Inheritance is achieved using the `extends`  keyword.

_Java does not support multiple inheritance because it can lead to ambiguity and complexity, especially the diamond problem._

The diamond problem occurs when a class inherits from two classes that have a common ancestor. This can lead to conflicts in the inheritance of methods. For example, if a class inherits from two classes that both have a method called `foo()`, it is not clear which method should be called when the `foo()` method is invoked on an instance of the class.

---
## Encapsulation

Encapsulation is one of the fundamentals of OOP (object-oriented programming). Encapsulation in Java is a process of wrapping code and data together into a single unit. We can achieve encapsulation by making all the members of a class as private and providing public getters and setter to access or modify the data members.
#### Advantages of Encapsulation :

By providing only a setter or getter method, you can make the class `read-only or write-only`. In other words, you can skip the `getter()` or `setter()` methods.

---

## Polymorphism

The process of achieving one thing in different forms is known as Polymorphism. In Java we can achieve polymorphism in two ways:
1. Overloading (Compile time polymorphism)
2. Overriding (Runtime polymorphism)
### Overloading

This polymorphism is also known as static polymorphism. This type of polymorphism can be achieved by overloading the functions of a class. When there are multiple functions with the same name but different parameters then these functions are said to be overloaded. Functions can be overloaded by changes in the number of arguments or/and a change in the type of arguments.

### Overriding

It is also known as Dynamic Method Dispatch. It is a process in which a function call to the overridden method is resolved at Runtime. This type of polymorphism is achieved by Method Overriding. Method overriding, on the other hand, occurs when a derived class has a definition for one of the member functions of the base class. That base function is said to be overridden.

---

## Abstraction

Abstraction is the process of hiding implementation details and showing only functionality to the user. Abstraction lets you focus on, what an object does, instead of how it does. We can achieve abstraction in java in two ways. By using Abstract classes and by using Interfaces. We can achieve 100% abstraction by using interfaces.