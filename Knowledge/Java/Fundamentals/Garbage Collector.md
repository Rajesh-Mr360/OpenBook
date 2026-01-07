# Introduction

Garbage collection in Java is the process by which Java programs perform automatic memory management. Java programs compile to bytecode that can be run on a Java Virtual Machine. When Java programs run on the JVM, objects are created on the heap, which is a portion of memory dedicated to the program. Eventually, some objects will no longer be needed. The garbage collector finds these unused objects and deletes them to free up memory. The programmer does not need to mark objects to be deleted explicitly. The garbage collection implementation lives in the JVM.

**Important Concepts Related to Garbage Collection in Java**
The garbage collector job is to automate the memory management. The main component of the Garbage collector is “Mark and Sweep algorithm”.  So how does it work at high level ?

The garbage collector scans at the dynamic memory areas for objects that are referenced and unreferenced. Unreferenced objects are identified and marked as ready for garbage collection. Marked objects are deleted and memory is compacted by moving the referenced objects together forming a contagious block on Heap.  This make it easier to allocate memory to new objects.

**Finalization**
Just before destroying an object, Garbage Collector calls `finalize()` method on the object to perform clean-up activities. Once `finalize()` method completes, Garbage Collector destroys that object. Based on our requirement, we can override `finalize()` method for performing our clean-up activities like closing connection from the database.

**Advantages of Garbage Collection in Java**
The advantages of Garbage Collection in Java are:
1. It makes java memory-efficient because the garbage collector removes the unreferenced objects from heap memory.
2. It is automatically done by the garbage collector(a part of JVM), so we don’t need extra effort.