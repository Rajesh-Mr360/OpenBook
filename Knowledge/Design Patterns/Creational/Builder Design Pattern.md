# Introduction

A **Builder Design Pattern** is a **Creational Design Pattern** that **lets you construct complex objects step by step**. It works by providing a constructor with required parameters and then different setter methods to set the optional parameters.

Let’s see how we can implement builder design pattern in java.

1. First of all you need to create a static nested class and then copy all the arguments from the outer class to the Builder class. We should follow the naming convention and if the class name is `Computer` then builder class should be named as `ComputerBuilder`.
2. Java Builder class should have a public constructor with all the required attributes as parameters.
3. Java Builder class should have methods to set the optional parameters and it should return the same Builder object after setting the optional attribute.
4. The final step is to provide a `build()` method in the builder class that will return the Object needed by client program. For this we need to have a private constructor in the Class with Builder class as argument.

**Example :**
```Java
public class Computer {  
    private String brand;  
    private String model;  
    private Integer price;  
  
    public Computer(ComputerBuilder builder) {  
        this.brand = builder.brand;  
        this.model = builder.model;  
        this.price = builder.price;  
    }  
  
    //Getters... (Setter aren't rquired - should be a read-only upon creation)
  
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