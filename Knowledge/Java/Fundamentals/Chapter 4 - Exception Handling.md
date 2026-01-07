In Java an exception is an unwanted event that occurs during the execution of program and disrupts the normal flow of program execution. Exception handling is a powerful mechanism of Java to handle the runtime errors so that the normal flow of the application can be maintained.

## Advantages of Exception handling

The core advantage of exception handling is **to maintain the normal flow of the application**. An exception normally disrupts the normal flow of the application; that is why we need to handle exceptions. Let's consider a scenario:

Suppose there are 10 statements in a Java program and an exception occurs at statement 5; the rest of the code will not be executed, i.e., statements 6 to 10 will not be executed. However, when we perform exception handling, the rest of the statements will be executed. That is why we use exception handling in Java.

The `{Java}java.lang.Throwable` class is the root class of Java Exception hierarchy inherited by two subclasses: Exception and Error. There are mainly two types of exceptions: checked and unchecked. An error is considered as the unchecked exception. However, according to Oracle, there are three types of exceptions namely:

1.     Checked Exceptions
2.     Unchecked Exceptions
3.     Error


### Checked Exceptions

Checked exceptions, also known as compile-time exceptions, are exceptions that must be either caught or declared in the method signature using the `throws` keyword. These exceptions are typically used to handle expected error scenarios that a program can recover from. They force the developer to acknowledge and handle these exceptional conditions, ensuring that appropriate actions are taken. Some common examples of Checked exceptions are `IOException`, `SQLException`, `FileNotFoundException`, `ClassNotFoundException`.

To handle a checked exception, you can use a `try - catch` block. Alternatively, if you prefer not to handle the exception immediately, you can declare it in the method signature using the `throws` keyword. This transfers the responsibility of handling the exception to the caller of the method.


### Unchecked Exceptions

Unchecked exceptions, also known as runtime exceptions, are exceptions that do not need to be caught explicitly or declared using the `throws` keyword. They usually represent programming errors, such as invalid calculations or incorrect usage of APIs, that can be prevented by proper code design and testing. Some common examples of unchecked exceptions are…

#ArithmeticException If we divide any number by Zero, there occurs an ArithmeticException.

#NullPointerException If we have a null value in any variable, performing any operation on the variable throws a NullPointerException.

#NumberFormatException If the formatting of any variable or number is mismatched, it may result into NumberFormatException. Suppose we have a string variable that has characters; converting this variable into digit will cause NumberFormatException.

#ArrayIndexOutOfBoundsException When we try to access a element with help of a Index that is greater than the size of the array there occurs ArrayIndexOutOfBoundsException. there may be other reasons to occur ArrayIndexOutOfBoundsException.


## Custom Exception In Java

Java provides us the facility to create our own exceptions which are basically derived classes of Exception. Creating our own Exception is known as a custom exception or user-defined exception. Basically, Java custom exceptions are used to customize the exception according to user needs. In simple words, we can say that a User-Defined Exception or custom exception is creating your own exception class and throwing that exception using the ‘throw’ keyword.

Let's start with a basic example – imagine you are developing a banking application, and you want to handle a scenario where an account balance goes below a minimum threshold. In this example, `LowBalanceException` is a custom exception class that inherits from the standard `Exception` class. It includes a constructor that accepts a message, allowing you to provide specific details about the error.


```Java ln:false 
public class InsufficientFundsException extends RuntimeException {
	public InsufficientFundsException(String message) {
		super(message); 
	}
}

// Usage in another class 
public class BankAccount { 
	private double balance; 
	//Moves the responsibility of handling exception to the caller of this method.
	public void withdraw(double amount) throws InsufficientFundsException { 
		if (amount > balance) { 
			throw new InsufficientFundsException("Not enough funds in your account."); 
		} 
		// Perform withdrawal logic 
	} 
}
```


