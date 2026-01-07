# What is Java ?

Java is a platform-independent, object-oriented programming language, based on the principle of '***write once, run anywhere***' This means that once a Java program is compiled, it can be executed on any system equipped with a **Java Virtual Machine (JVM)**, regardless of the underlying operating system. We can build a wide range of applications using java, such as web applications, mobile and desktop applications, IoT products, and game development.

Java platform consists of three key components that are important to understand:
1. JVM - Java Virtual Machine
2. JRE - Java Runtime Environment
3. JDK - Java Development Kit

## JVM - Java Virtual Machine

JVM is the heart of Java, using which Java achieves platform independence. It reads the compiled Java bytecode and translates it into native machine code that underlying operation system can understand. Its responsibilities are not limited to this; JVM also handles memory management using the **Garbage Collector** and includes an **Execution Engine** that helps improve application performance.

### Execution Engine

The **Java execution engine** is ==a core component of the **Java Virtual Machine (JVM)** responsible for running Java bytecode==. It converts the platform-independent bytecode into native machine code that the underlying hardware can execute

The execution engine consists of three primary sub-components:
- **Interpreter :** This component reads and executes the bytecode instructions line by line. While this approach ensures a quick start-up time for an application, it is slow for repeated execution of the same code because it re-interprets the same methods every time they are called.
- **(Just-In-Time) JIT Compiler :** To overcome the performance limitations of the interpreter, the JIT compiler was introduced. It identifies "hot spots" (frequently executed code segments) converts them into optimized native machine code at runtime. This native code is stored in a cache and reused for subsequent calls, significantly improving the overall execution speed of long-running applications.
- **Garbage Collector :** Garbage collection in Java is the process by which Java programs perform automatic memory management. Java programs compile to bytecode that can be run on a Java Virtual Machine, or JVM for short. When Java programs run on the JVM, objects are created on the heap, which is a portion of memory dedicated to the program. Eventually, some objects will no longer be needed. The garbage collector finds these unused objects and deletes them to free up memory.


## JRE - Java Runtime Environment
The **Java Runtime Environment** is essential component in Java that lets you run Java applications. It consists of **Java Virtual Machine - JVM** and **Core Libraries** needed for execution of Java applications. While developers use complete Java Development Kit - JDK to build and run applications, end-user only need the Java Runtime Environment - JRE to execute compiled Java applications on their Operating Systems.

## JDK - Java Development Kit
**JDK (Java Development Kit)** is a **software development kit used to develop Java applications**. It provides everything required to **write, compile, run, and debug Java programs**. JDK includes the **Java compiler (`javac`)**, the **Java Runtime Environment (JRE)**, and various development tools such as debuggers, documentation tools, and monitoring utilities. When you write Java code (`.java` file), the JDK compiler converts it into bytecode (`.class` file), which can then be executed by the JVM. In simple terms, **JDK is meant for developers**, while JRE is only for running Java applications.

---
# Data Types

In any programming language, we need to **store and work with different kinds of data** such as numbers, characters, text. Java uses **data types** to clearly define **what kind of value a variable can hold**, how much **memory** should be allocated, and what **operations** can be performed on that data. This helps Java programs run efficiently and prevents errors caused by storing the wrong type of data in a variable.

Since Java is a **strongly typed language**, every variable must be declared with a data type before it is used. This ensures **type safety**, better memory management, and improved program reliability.

In Java, data types are fundamentally divided into two categories: 
1. Primitive Data Types
2. Non-Primitive Data Types

## 1. Primitive Data Types
Primitive Data Type are predefined key words in Java used to store simple values without need for creating objects. They do not provide any methods to perform operations on the stored data. 

| boolean | byte   | char   | short  | int    | long   | float  | double |
| ------- | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 1 bit   | 1 byte | 2 byte | 2 byte | 4 byte | 8 byte | 4 byte | 8 byte |

### 1.1. Why is the Size of char 2 bytes in Java?

So, other languages like C/C++ use only ASCII characters, and to represent all ASCII characters 8 bits is enough. But Java uses the Unicode system not the ASCII code System and to represent the Unicode system 8 bits is not enough to represent all characters. So, Java uses 2 bytes for characters. Unicode defines a fully international character set that can represent most of the world’s written languages. It is a unification of dozens of character sets, such as Latin, Greek, Cyrillic, Katakana, Arabic, and many more.

## 2. Non – Primitive data types

**Non-primitive data types**, are used to store data in the form of objects. Instead of storing actual values directly, they store **references (memory addresses)** to the data. Unlike primitive data types, non-primitive data types are **created using classes** and they **provide methods** to perform operations on the stored data. They can also hold multiple values, can be `null`, and their size is not fixed.

## Wrapper Classes

Wrapper classes are a set of classes in Java that provide a way to use primitive data types as objects. They **_wrap_** primitive types in an object so that they can be included in activities reserved for objects, like being added to collections, passed as parameters in methods that expect objects, and more. These wrapper classes provide methods and constructors to convert primitive data types into objects and to perform various operations on them, making them useful in situations where objects are needed instead of primitives, such as in collections or generic classes that require objects.

---
## String

**String** is a predefined **non-primitive data type** in Java used to store a sequence of characters. Strings in Java are **immutable**, which means their values cannot be changed once created. However, when we try to modify a string or assign a new value to it, Java does not change the existing string. Instead, it **creates a new String object** with the updated value, and the reference is updated to point to the new object. A String can be created either using a **string literal** (`"Data"`) or by using the **`new` keyword** (`new String("Data")`). The String class also provides many built-in methods to access, manipulate, and compare strings.
## StringBuffer

`StringBuffer` is a class in Java that represents a mutable sequence of characters. It provides an alternative to the immutable String class, allowing you to modify the contents of a string without creating a new object every time.

**Some Important Features and Methods Of StringBuffer**

1. `StringBuffer` objects are mutable, meaning that you can change the contents of the buffer without creating a new object.
2. The initial capacity of a `StringBuffer`  can be specified when it is created, or it can be set later with the `ensureCapacity()`  method.
3. The `append()` method is used to add characters, strings, or other objects to the end of the buffer.
4. The`insert()`  method is used to insert characters, strings, or other objects at a specified position in the buffer.
5. The `delete()`  method is used to remove characters from the buffer.
6. The `reverse()`  method is used to reverse the order of the characters in the buffer.
 

## StringBuilder

`StringBuilder`  in Java represents a mutable sequence of characters. Since the String Class in Java creates an immutable sequence of characters, the `StringBuilder`  class provides an alternative to String Class, as it creates a mutable sequence of characters.

The function of `StringBuilder`  is very much similar to the `StringBuffer`  class, as both of them provide an alternative to String Class by making a mutable sequence of characters. However, the StringBuilder class differs from the StringBuffer class on the basis of synchronization. The StringBuilder class provides no guarantee of synchronization whereas the StringBuffer class does. Therefore this class is designed for use as a drop-in replacement for StringBuffer in places where the StringBuffer was being used by a single thread (as is generally the case). Where possible, it is recommended that this class be used in preference to StringBuffer as it will be faster under most implementations. Instances of StringBuilder are not safe for use by multiple threads. If such synchronization is required then it is recommended that StringBuffer be used. String Builder is not thread-safe and high in performance compared to String buffer.

---

## String Constant Pool

When Java applications are running, a large number of **String objects** are created and stored in **heap memory**. Over time, this number can become very large and may contain many **duplicate strings**, which leads to **memory wastage**. To address this problem and manage memory efficiently, the **String Constant Pool (SCP)** was introduced.

The **String Constant Pool** is a specialized area within the **heap memory** that is used to store **String literals**. Its primary purpose is to **save memory and improve performance**. 

When a String literal is created, the JVM first checks whether the same value already exists in the pool. If it does, the reference to the existing String object is returned. If it does not, a new String object is created in the pool and its reference is returned. This mechanism ensures that duplicate String objects are not created unnecessarily, thereby optimizing memory usage.

### Why is a new object created when using the `new` keyword with String?

This behavior is **intentional by design**. When you use the **`new` keyword**, you are explicitly instructing Java to **create a new String object**, regardless of whether the same value already exists in the String Constant Pool. To respect this instruction, Java always creates a **new String object in heap memory**. This object is separate from the pooled String and has a different reference, even though the content may be the same.

---
# Variables

Variables in Java are data containers that holds a value during program execution. Simply put ‘Variables’ in java language are the names that are used to refer to data stored in the memory. Following are the three main types of variables in Java.

**LOCAL VARIABLES**

**Local variables** in Java are declared inside the method body and the access to these variables to the outer world is restricted, which mean we won’t be able to access a local variable from outside of the method. A local variable will be destroyed automatically once the execution of method is completed. We can’t use access modifiers when declaring a local variable. Local variables are stored in stack memory. 

**INSTANCE VARIABLES**

**Instance variables** are declared at class level and outside of any blocks or methods. Instance variables can be both static and non-static. These variables can be accessed from any methods of the class they are declared. Instance variables can be used with access modifiers to define their access level.

**STATIC VARIABLES**

A variable that is prefixed with `static` key at the time of declaration is called ‘**static variable**’ . When a variable is declared as static variable in class, it’s state can be used by all the objects that class.
