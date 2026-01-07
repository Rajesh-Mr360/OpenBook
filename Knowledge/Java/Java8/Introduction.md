Java8 has introduced many new features to enhance productivity in Java. Some notable features include the introduction of **Lambda Expressions**, **Functional Interfaces**, and **Streams**, which brought functional programming capabilities to the language.

Some of important features are:
1. Lambda Expressions
2. Functional Interfaces
3. Method References
4. Streams
5. Comparable & Comparator
6. Optional Class
7. Date & Time API
8. Foreach()
9. Default Methods in Interface

---

## 1. Lambda Expressions

**Lambda Expressions** is a powerful feature introduced in Java8 that brought functional programming capabilities to Java. With lambda expressions, we can easily create compact blocks of code that can be passed as method parameter or assigned to a variable. Lambda expressions make use of **anonymous classes** to achieve this behavior. 

Lambda expressions reduce the need for writing lot of boilerplate code that was previously required when using anonymous classes:
- There is **no need to declare a class name**
- There is **no need to specify the method name**
- There is **no need to declare the return type**, as it is identified by the compiler at runtime
- If there is **only one parameter**, the parentheses around the argument can be omitted
- If the method body contains **only a single statement**, curly braces `{}` and the `return` keyword are not required

This makes the code **more readable, expressive, and concise**, while still maintaining strong type safety provided by Java.
 
### Let's get deeper

To get a deeper and better understanding, you need to understand the problem they are trying to solve and how they have evolved with the Java language. ***The core idea behind the introduction of lambda expressions(lambdas) is to allow developers to write cleaner, shorter more readable, and reusable code***.

So let’s get right into code! our journey starts with a class. This class implements an interface in the `java.util` package called the **Consumer interface**. This generic interface has a single abstract method called accept which accepts one parameter and returns nothing.

```java
public class PrintWords implements Consumer<String> {  
  
	@Override  
	public void accept(String sentence) {  
		String[] words = sentence.split(" ");  
		for (String word: words) {  
			System.out.println(word);  
		}  
	}  
}
```

As you can see, the overridden accept method in our `PrintWords` class does one simple thing. It takes a string, splits them by spaces, and prints out the words in new lines. In our main method, we can execute this code as follows.

```java
public static void main(String[] args) {
	String mySentence = "Using lambdas in java";
	PrintWords separator = new PrintWords();
	separator.accept(mySentence);
}
```

This is rather a large number of code lines for such a simple task, isn’t it? Let’s simplify this a little bit more. Rather than creating a separate class, we can replace the `PrintWords` class we created earlier with an anonymous class inside the main method itself. An anonymous class is a type of nested class in Java that you can create without explicitly giving it a name.

```java
public static void main(String[] args) {  
  
	Consumer<String> printWords = new Consumer<String>() {  
	  
	@Override  
	public void accept(String sentence) {  
		String[] words = sentence.split(" ");  
			for (String word: words) {  
				System.out.println(word);  
			}  
		}  
	};  
	  
	printWords.accept(mySentence);  
}
```

Here we specify the Consumer interface being implemented, followed by the definition of the class body within curly braces. This anonymous class can be directly replaced by a lambda expression.

```java
Consumer<String> lambda = sentence -> {  
	String[] words = sentence.split(",");  
	for (String word: words) {  
		System.out.println(word);  
	}  
};  
  
lambda.accept(mySentence);
```

Notice the changes we made to the right of the assignment operator here.

- We are not specifying that we create a new class that implements the Consumer interface with the new keyword.
- We are not specifying that we implement the accept method of the interface

This compiles and works without issues. 

**So how does the compiler know about the Consumer interface and which method of the consumer interface do we implement here?** Well, the key here is the type of the reference variable lambda. We specify that the variable lambda is of type `Consumer<String>` and the rest is inferred by the compiler. 

***But how does it know which method of the Consumer interface we implement?*** the answer is simple, as I mentioned above, the consumer interface has only one abstract method called accept. These types of interfaces with only one abstract method are known as functional interfaces. So when we specify the type of the variable lambda as `Consumer<String>`, the compiler knows that our lambda expression will take a single argument to the accept method and doesn't return anything. And this brings us to one of the key things you should know when it comes to lambda expressions. Lambda expressions can only be created for functional interfaces.

In the above code, we created a multi-line lambda expression. Let’s simplify it even more.

```Java
Consumer<String> shortLambda = sentence -> Arrays.asList(sentence.split(" ")).forEach(word -> System.out.println(word));  
shortLambda.accept(mySentence);
```

Here we are using a single-line lambda expression. Also here we are using nested lambda expressions. The `forEach()` method of the List interface takes the same functional interface Consumer as an argument. So we can pass a lambda expression to the `forEach()` method as well.

Let’s go just one step further and shorten this expression just a bit more.

```Java
Consumer<String> shortLambda = sentence -> Arrays.asList(sentence.split(" ")).forEach(System.out::println);  
shortLambda.accept(mySentence);
```

Here we modified the lambda expression passed to the forEach method. This is known as a method reference. Introduced in java 8, method references allow developers to simplify lambda expressions even more by directly referencing methods instead of writing a lambda expression that duplicates the method’s signature and implementation. So here each element of the list will be directly passed as an argument to the println method.

So as you can see, we started with a separate class declaration and simplified it just to two lines of code. Hopefully, this helped you understand just how powerful lambdas can be in Java and how we can utilize them to improve our code.


---
# 2. Functional Interface

Lambda functions provide a concise and expressive way to represent anonymous functions, making it easier to work with functional programming concepts in Java. However, to use lambda expressions effectively, we need to understand functional interfaces, as they form the foundation of lambda expressions in Java.
## 2.1. What are Functional Interfaces

Functional Interfaces are foundation of Lambda expression through which functional programming is achieved in java. ==A functional interface is an interface that contains only one abstract method. The presence of a single abstract method ensures that the interface can be used with lambda expressions.== To indicate that an interface is intended to be a functional interface, we use the `@FunctionalInterface` annotation. Although the annotation is optional, it is good practice to use it as it helps developers understand the intended use of the interface.

```java
@FunctionalInterface  
interface MyFunctionalInterface {  
	void doSomething();  
}
```

In this example, `MyFunctionalInterface` is a functional interface because it contains only one abstract method, `doSomething()`.

## 2.2. Built-in Functional Interfaces in Java
Java provides a set of built-in functional interfaces in the `java.util.function` package to cover a wide range of use cases. These functional interfaces are categorized into four main types based on the operation they perform: **Consumer**, **Supplier**, **Function**, and **Predicate**.

### 2.2.1. Consumer
A `Consumer` is a functional interface that represents an operation that takes a single input and performs some action on it. It does not return any value.
```Java
@FunctionalInterface  
interface Consumer<T> {  
	void accept(T t);  
}
```
`accept(T t)`: This abstract method takes a parameter of type `T` and performs the desired action on it.

**Example: Using Consumer Interface**

```Java
import java.util.List;  
import java.util.ArrayList;  
import java.util.function.Consumer;  
  
public class ConsumerExample {  
	public static void main(String[] args) {  
		List<String> names = new ArrayList<>();  
		names.add("Alice");  
		names.add("Bob");  
		names.add("Charlie");  
		  
		// Using a Consumer to print each element of the list  
		Consumer<String> printName = name -> System.out.println(name);  
		names.forEach(printName);  
	}  
}
```

In this example, we create a `Consumer` called `printName` that prints each element of the `names` list.

### 2.2.2. Supplier
A `Supplier` is a functional interface that represents an operation that supplies (provides) a result. It does not take any input.
```Java
@FunctionalInterface  
interface Supplier<T> {  
	T get();  
}
```
`get()`: This abstract method returns a result of type `T`.

**Example: Using Supplier**

```Java
import java.util.function.Supplier;  
  
public class SupplierExample {  
	public static void main(String[] args) {  
		// Using a Supplier to generate a random number  
		Supplier<Double> randomNumberSupplier = () -> Math.random();  
		double randomNumber = randomNumberSupplier.get();  
		System.out.println("Random Number: " + randomNumber);  
	}  
}
```

In this example, we create a `Supplier` called `randomNumberSupplier` that generates a random number using `Math.random()`.

### 2.2.3. Function
A `Function` is a functional interface that represents an operation that takes an input of type `T` and produces an output of type `R`.
```Java
@FunctionalInterface  
interface Function<T, R> {  
	R apply(T t);  
}
```
`apply(T t)`: This abstract method takes a parameter of type `T` and returns a result of type `R`.

**Example: Using Function**

```Java
import java.util.function.Function;  
  
public class FunctionExample {  
	public static void main(String[] args) {  
		// Using a Function to convert a string to its length  
		Function<String, Integer> stringLengthFunction = s -> s.length();  
		int length = stringLengthFunction.apply("Java is awesome!");  
		System.out.println("Length of the string: " + length);  
	}  
}
```

In this example, we create a `Function` called `stringLengthFunction` that converts a string to its length using the `length()` method.

### 2.2.4. Predicate

A `Predicate` is a functional interface that represents an operation that takes an input of type `T` and returns a boolean result.

```Java
@FunctionalInterface  
interface Predicate<T> {  
	boolean test(T t);  
}
```

`test(T t)`: This abstract method takes a parameter of type `T` and returns a boolean result.

**Example: Using Predicate**
```Java
import java.util.function.Predicate;  
  
public class PredicateExample {  
	public static void main(String[] args) {  
		// Using a Predicate to check if a number is even  
		Predicate<Integer> isEvenPredicate = number -> number % 2 == 0;  
		boolean isEven = isEvenPredicate.test(10);  
		System.out.println("Is the number even? " + isEven);  
	}  
}
```

In this example, we create a `Predicate` called `isEvenPredicate` that checks if a number is even using the condition `number % 2 == 0`.
## 2.3. Custom Functional Interface

While Java provides a set of useful built-in functional interfaces, you may encounter scenarios where none of the built-in interfaces precisely match your requirements. In such cases, you can create custom functional interfaces to suit your specific needs.

To create a custom functional interface, follow these steps:

1. Define an interface with a single abstract method that represents the functionality you want the lambda expression to perform.
2. Optionally, use the `@FunctionalInterface` annotation to indicate that the interface is intended to be a functional interface.

There's nothing to go more deeper into this, find below example: 
```Java
@FunctionalInterface  
interface MyCustomFunctionalInterface {  
	void doSomething(int value);  
}
```

---
# 3. Method References

A Method Reference is a short hand way to reference to existing methods using Lambda Expressions. A **method reference** allows you to refer to a method **without invoking it** immediately, using the `::` operator. Which means that, the method (behavior) is passed as an argument to be used later when required.

There are four types of method references:
1. **Reference to a Static Method**: `ClassName::staticMethodName`.
2. **Reference to an Instance Method of a Particular Object**: `instance::instanceMethodName`.
3. **Reference to an Instance Method of an Arbitrary Object of a Particular Type**: `ClassName::instanceMethodName`.
4. **Reference to a Constructor**: `ClassName::new`.

---

# Streams

Read [[Streams]]

---

# Optional Class

When working with Java, we often encounter `NullPointerException` in applications. This occurs when we try to perform operations on variables that are not referencing any object or have not been initialized. In simple terms, the variable has no assigned value or the value is absent.

To handle such scenarios effectively, `Optional` was introduced in Java8, which acts as a container to wrap the object, indicating possibility of present or absent. Its primary purpose is to provide a safer alternative  for dealing with null values reducing the chances of running into `NullPointerException`.
