# Introduction

The **Abstract Factory Design Pattern** is a creational design pattern. It works very similar to **Factory Design Pattern** but works at higher level — it acts like a _factory of factories_. While the Factory pattern directly creates the required product, the Abstract Factory pattern instead provides the appropriate factory that will then create the product. This pattern is helpful when you want to delegate the responsibility of creating related objects (from the same family) to a separate component, ensuring consistency and flexibility in object creation.

![700](../images/AbstractFactoryPattern.jpg)


## How does the abstract factory pattern works

In Abstract Factory Pattern, we create an interface named `Abstract Factory` (say), which can be used as a generic structure to define a concrete factory. These concrete factories can now be used to create objects for their respective family.

**For example**, say we are working on a Food App, where different types of Foods can be created like Vegetarian and Non-Vegetarian. These are the **2 major categories**. Among these categories there are multiple individual products or objects, say for the Vegetarian category there is a Veg Burger, Veg Pizza, Veg Noodles, Veg Biryani, Veg Cutlet, etc. Similarly, for the Non-Vegetarian category, there is Non-Veg Burger, Non-Veg Pizza, Non-Veg Noodles, Non-Veg Biryani, Non-Veg Cutlet, etc.

In the above example, we can create an `AbstractFactory` interface which will be implemented by a `VegFactory` class and a `NonVegFactory` class. Now for Veg and Non-Veg there will be **2 interfaces** that will be implemented by specific product concrete classes. The specific factories will be consulted for any particular type of object as per the need.