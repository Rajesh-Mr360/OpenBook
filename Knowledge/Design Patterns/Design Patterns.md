Design patterns are reusable solutions to common software design problems. They offer a structured approach to solving issues in software development and are not specific to any particular programming language. In Java, design patterns help maintain code modularity and promote good coding practices.


![500](images/DesignPatterns.webp)

# Creational Design Patterns
Creational design patterns provide various object creation mechanisms, which increase flexibility and reuse of existing code.
## Singleton
**Singleton** is a creational design pattern that lets you ensure that a class has only one instance while providing a global access point to this instance. In simple words, the ==Singleton design pattern ensures that only one instance of the class will be created and that instance will have global access within the application==.

## Factory
The Factory Design Pattern is a creational design pattern that provides an interface for creating objects in a super class but allows subclasses to decide which class to instantiate. In other words, the ==Factory pattern is used to create objects without exposing the creation logic to the client. This pattern is useful when you need to create objects of different types based on a given input==.

**Key Components of Factory Design Pattern:**
1. **Product Interface/Abstract Class:** This defines the interface or abstract class that represents the products to be created by the factory. It declares the common methods that the concrete products must implement.
2. **Concrete Products:** These are the specific classes that implement the product interface or extend the abstract class. Each concrete product represents a different variation or implementation of the product interface.
3. **Factory Class:** The factory class is responsible for creating and returning instances of the concrete products. It provides a method or methods to create objects based on certain conditions or parameters.

## Abstract Factory
Abstract Factory is one of the **Creational patterns** and almost similar to **Factory Pattern** except for the fact that it’s more like a factory of factories. ==_The Abstract Factory design pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes._==

### How does the abstract factory pattern works
In Abstract Factory Pattern, we create an interface named `Abstract Factory` (say), which can be used as a generic structure to define a concrete factory. These concrete factories can now be used to create objects for their respective family.

**For example**, say we are working on a Food App, where different types of Foods can be created like Vegetarian and Non-Vegetarian. These are the **2 major categories**. Among these categories there are multiple individual products or objects, say for the Vegetarian category there is a Veg Burger, Veg Pizza, Veg Noodles, Veg Biryani, Veg Cutlet, etc. Similarly, for the Non-Vegetarian category, there is Non-Veg Burger, Non-Veg Pizza, Non-Veg Noodles, Non-Veg Biryani, Non-Veg Cutlet, etc.

In the above example, we can create an `AbstractFactory` interface which will be implemented by a `VegFactory` class and a `NonVegFactory` class. Now for Veg and Non-Veg there will be **2 interfaces** that will be implemented by specific product concrete classes. The specific factories will be consulted for any particular type of object as per the need.

## Builder
A **Builder Design Pattern** is a **Creational Design Pattern** that **lets you construct complex objects step by step**. It works by providing a constructor with required parameters and then different setter methods to set the optional parameters.

> Or we can say! A **Builder Pattern** solves the issue with a large number of optional parameters and inconsistent states by providing a way to build the object step-by-step and provide a method that will actually return the final Object.

Let’s see how we can implement builder design pattern in java.

1. First of all you need to create a static nested class and then copy all the arguments from the outer class to the Builder class. We should follow the naming convention and if the class name is `Computer` then builder class should be named as `ComputerBuilder`.
2. Java Builder class should have a public constructor with all the required attributes as parameters.
3. Java Builder class should have methods to set the optional parameters and it should return the same Builder object after setting the optional attribute.
4. The final step is to provide a `build()` method in the builder class that will return the Object needed by client program. For this we need to have a private constructor in the Class with Builder class as argument.

```java
public class Computer {  
    private String brand;  
    private String model;  
    private Integer price;  
  
    public Computer(ComputerBuilder builder) {  
        this.brand = builder.brand;  
        this.model = builder.model;  
        this.price = builder.price;  
    }  
  
    //Getters...  
  
    static class ComputerBuilder {  
	    //Required parameter
        private final String brand;  
        //Optional parameters  
        private String model;  
        private Integer price;  
  
        public ComputerBuilder(String brand) {  
            this.brand = brand;  
        }  
  
        public ComputerBuilder setModel(String model) {  
            this.model = model;  
            return this;  
        }  
  
        public ComputerBuilder setPrice(Integer price) {  
            this.price = price;  
            return this;  
        }  
  
        public Computer build() {  
            return new Computer(this);  
        }  
    }  
}
```


# Structural Design Pattern
Structural design patterns explain how to assemble objects and classes into larger structures, while keeping these structures flexible and efficient. They help in forming larger structures from individual parts, making the system more flexible and efficient.

1. **Adapter :** Acts as a connector between two incompatible interfaces.
2. **Bridge :** Decouples an abstraction from its implementation.
3. **Decorator :** This allows users to add new functionality to an existing class without altering its structure.
4. **Façade :** Hides the complexity of system and provides  a simple interface to the client.
5. **Proxy :** A class represents the functionality of another class.

## Adapter
The #Adapter Design Pattern **allows objects with incompatible interfaces to collaborate.** It acts as a bridge between two incompatible interfaces by converting the interface of one class into another interface that clients expect. This pattern is particularly useful when integrating new features or components into existing systems without modifying their source code.

**Key components:**
- **Target:** Defines the specific interface the client expects.
- **Adaptee:** Represents an existing class with an incompatible interface.
- **Adapter:** Implements the Target interface and delegates requests to the Adaptee.

## Bridge
**Bridge** is a structural design pattern that divides business logic or huge class into separate class hierarchies that can be developed independently. The Bridge design pattern allows you to separate the abstraction from the implementation. Bridge design pattern is most applicable in applications where we need to provide the components that are platform independence.
- The bridge pattern allows the Abstraction and the Implementation to be developed independently and the client code can access only the Abstraction part without being concerned about the Implementation part.
- The abstraction is an interface or abstract class and the implementer is also an interface or abstract class.
- The abstraction contains a reference to the implementer. Children of the abstraction are referred to as refined abstractions, and children of the implementer are concrete implementers. Since we can change the reference to the implementer in the abstraction, we are able to change the abstraction’s implementer at run-time. Changes to the implementer do not affect client code.
- It increases the loose coupling between class abstraction and it’s implementation.
![400](images/bridge-pattern-structure.webp)

## Decorator
Decorator pattern allows us to add a new functionality to existing objects without changing its structure at all. Simply, it allows to do runtime modifications to the objects.
**A decorator** is a structural design pattern that lets you attach new behaviours to objects by placing these objects inside special wrapper objects that contain the behaviours.

![600](images/decorator-diagram.PNG)


## Proxy
**Understanding the Proxy Pattern**
The Proxy pattern is a structural design pattern that provides a surrogate or placeholder for another object to control access to it. In essence, it's like having a representative or agent acting on behalf of another entity.  

**Key components:**
- **Subject interface:** Defines the common interface for both the real subject and the proxy.
- **Real Subject:** The actual object that performs the real work.
- **Proxy:** The intermediary object that controls access to the real subject.

**How it works:**
1. A client interacts with the proxy.
2. The proxy decides whether to forward the request to the real subject or handle it itself.
3. If forwarded, the proxy passes the request to the real subject and returns the result to the client.