# List Interface
List is an interface that represents an ordered Collection of elements which may contain duplicates. It extends the `Collection` interface. Java provides several List implementations each with it's own strength and weakness. They are `ArrayList` , `LinkedList` , `Vectors`  and `Stack`.

## ArrayList 
ArrayList is a resizable array implementation of List interface. It implements all the optional methods of List interface and provide some additional methods to access or manipulate the elements.

ArrayList internally uses index based data structure to store the elements. The default size of the ArrayList is `10` . ArrayList grows dynamically and ensures that there’s always a room for adding new elements. When we add an element to the ArrayList, it first checks to see whether the array has enough capacity to insert the new elements. If not then the capacity of the ArrayList will be increased by `50%` percent of the previous capacity. But the size of the array cannot be increased dynamically. So, what happens internally is, a new array is created with higher capacity and the old array is copied into the new array.

We can set the initial size of an ArrayList instance before adding a large number of elements using the `ensureCapacity()` method. This may reduce the amount of incremental reallocation.

In ArrayList, manipulation is a little bit slower compared to LinkedList in Java because a lot of shifting needs to occur if any element is removed from the ArrayList.

**The ArrayList is not synchronized.** If multiple threads try to access an ArrayList instance concurrently, and at least one of the them modifies the list structurally, then it will throw `ConcurrentModificationException`. We can prevent this by wrapping the list in `Collections.synchronizedList()` method or by Synchronizing it externally.

## LinkedList

A LinkedList is a linear data structure in which elements are stored in a contiguous memory location. 
LinkedList internally uses node based data structure to store the elements. Each node consists of two parts, namely the data part and the address part. The data part is the value of the element, and the address part consists of the pointers and addresses that are used to link the elements. Each element in the list is called a node.

LinkedList is better choice for manipulating data. Manipulating with LinkedList is faster than ArrayList as there is no need for shifting during manipulation.

**I have mentioned that LinkedList use a doubly linked list structure internally. But how does this allow for random access?** Here's the catch: the `get(index)` method starts from the head (first node) and traverses the list one node at a time until it reaches the `index`th node. It returns the data from that node. This traversal can be time-consuming for large lists, as it needs to iterate through all nodes before the target index.

**Important points to remember!**
1. LinkedList internally uses a doubly linked list to store the elements.
2. LinkedList follows insertion order and it allows duplicate elements and null values.
3. LinkedList is better for manipulating data.
4. LinkedList class can act as a list and queue both as it implements both List and Deque interfaces.
5. Manipulation with LinkedList is faster then ArrayList because it uses a doubly linked list and hence no bit shifting need to occur.
6. It is best to use when we need to add and remove items from the beginning or middle of the list and random access is not required.


## Vector
In Java, both ArrayList and Vector implements the List interface and provides the same functionalities. However, there exist some differences between them.

**Vectors are synchronized**, which implies that at a time, only one thread is able to access the code while other threads have to wait. Due to this, Vectors are slower in performance as they acquire a lock on a thread. This means whenever we want to perform some operation on vectors, the Vector class automatically applies a lock to that operation. It is because when one thread is accessing a vector, and at the same time another thread tries to access it, an exception called `ConcurrentModificationException` is generated. Hence, this continuous use of lock for each operation makes vectors less efficient.

It is recommended to use the Vector class in the thread-safe implementation only. If you don't need to use the thread-safe implementation, you should use the ArrayList, the ArrayList will perform better in such case.

The default capacity of the vector is 10. As an array gets initialized with some given size during creation, Similarly, Vector also gets initialized with the default capacity of 10. Size and capacity are mainly two different things. Size refers to the number of elements inserted in the vector or list, and capacity refers to the initialization of the vector.

At the creation of Vector, it initializes with a default capacity of 10 and a size of 0. As soon as we start inserting elements into the vector, the size will grows, and the capacity will remain the same as 10 till the addition of the 10th element. The capacity will change to 20, which is double once we insert the 11th element.

## Stack


The stack data structure is based on **Last In First Out (LIFO)** principle and in Java it implements List interface extends Vector class. The basic operations supported by Java stack are :
- `push()`     : Adds an element at the top of stack.
- `pop()`       : Removes the topmost element of the stack.
- `peek()`     : Returns an element that is on top of the stack.