The Map interface in Java is a powerful data structure that allows us to store and manipulate data in the form of key and value pairs. It provides an efficient way to associate values with unique keys and offers various methods for accessing, inserting, and removing elements. Java offers several map implementations, each with it’s own strength and weakness. They are `HashMap` , `LinkedHashMap` , `TreeMap`  and `ConcurrentHashMap`.

# HashTable

A **`Hashtable`** in Java is a data structure used to store **key-value pairs**, similar to `HashMap`, but with some important differences in behavior and usage. 

`Hashtable` is an **older, synchronized** implementation of a hash-based map.  It stores key-value pairs in buckets based on the **hashcode of the key**, and retrieves values efficiently using `get()`. It’s part of **Java’s legacy collection classes** (introduced in Java 1.0).


## HashMap

https://howtodoinjava.com/java/collections/hashmap/how-hashmap-works-in-java/

Java HashMap is the basic implementation of Map interface of Java. It is used to store the data in the form of `Key - Value` pairs. We can use key’s to access the corresponding Values. In Java HashMap we can store one `Null` key and any number of `Null` values. Java HashMap doesn’t allow to store duplicate keys, If we try to do it then the value associated with it will be replaced by the new value. 

**Internal Working :** HashMap uses a hashing algorithm to store data. When you add an element using the `put` method, a hash code is generated for the provided key. The index is then calculated by applying a bitwise AND operation with the current capacity, ensuring the index remains within bounds.

Sometime, same Hash Code will be generated for multiple keys, which is called as ***Hashing Collision***. In such cases, HashMap stores the entries in a linked list data structure, using internally created Node objects in the same Hash Bucket.

Starting from Java 8, if the number of entries in a bucket exceeds the threshold (default is 8), the LinkedList is converted into a Red-Black Tree for faster lookups (O(log n) instead of O(n)). In this tree structure, smaller values are stored on the left and larger values on the right within `TreeNode` objects.

Note that when nodes in a bucket reduced to less than _UNTREEIFY_THRESHOLD_ the _Tree_ again converts to _LinkedList_. This helps balance performance with memory usage because _TreeNodes_ takes more memory than _Map.Entry_ instances. So **_Map_ uses _Tree_ only when there is a considerable performance gain in exchange for memory wastage**.

**HashMap is not Synchronized.** When multiple threads accessing the map and one tried to modify the data then a `ConcurrentModificationException` will be thrown.
index = (capacity - 1) & hash;//It will calculate the index

## 1️⃣ What is HashMap?

- Stores data as **Key – Value** pairs
- Each **key is unique**
- Uses **hashing** to store and retrieve data fast

Example:
```java
map.put("A", 10);

   
## 2️⃣ Internal Structure

HashMap internally uses:
- An **array** (called *table* or *bucket array*)
- Each index of the array is called a **bucket**
- Each bucket can store:
  - One entry
  - Multiple entries (**due to collision**)
   Index   Bucket
    0  ---> null
    1  ---> (A,10)
    2  ---> (B,20) -> (C,30)
    3  ---> null
    
## 3️⃣ What happens when you call `put(key, value)`?

### Step 1: Calculate Hash
- Java calls:
  ```java
  key.hashCode();
    - Then improves it internally:
  ```java
  hash = hash ^ (hash >>> 16);//This spreads keys evenly.
    ### Step 2: Find Bucket Index
- Bucket index is calculated using:
  ```java
  index = (capacity - 1) & hash;
  # Default capacity = 16
  # This ensures the index is always between 0 – 15
    ### Step 3: Store Entry
- If the bucket is **empty** → store the entry directly
- If the bucket already contains entries → **collision occurs**

## 4️⃣ What is Collision & how it is handled?

### Collision
- When two different keys map to the **same bucket index**, it is called a **collision**

### Handling Collision
- HashMap stores multiple entries in the same bucket using:
  - **LinkedList** (initially)
  - **Red-Black Tree** (from Java 8+, when the list grows)

## 5️⃣ LinkedList → Red-Black Tree (Java 8+)

- When a bucket’s size exceeds **8**
- AND the overall HashMap capacity is **≥ 64**
- The **LinkedList is converted into a Red-Black Tree**

### Why this conversion?
| Data Structure | Time Complexity |
|---------------|----------------|
| LinkedList    | O(n)           |
| Red-Black Tree| O(log n)       |


## 6️⃣ How `get(key)` works?

### Steps:
1. Compute the **hash** of the key (e.g., `"A"`)
2. Find the **bucket index**
3. Traverse the bucket:
   - Compare **hash**
   - Then compare using **`equals()`**
4. Return the corresponding **value**


## 7️⃣ Role of `equals()` & `hashCode()`

- ✔ Same key → must return the same **hashCode()**
- ✔ HashMap uses:
  - **hashCode()** → to find the bucket
  - **equals()** → to find the exact key
- ❌ Wrong implementation can cause **bugs** and **performance issues**


## 8️⃣ Resizing (Rehashing)

### When resizing happens?
- Resizing occurs when:
- size > capacity × loadFactor
    
### Default values:
- Capacity = **16**
- Load Factor = **0.75**

- Resize happens when size > 12  
- New capacity becomes **32**


## 9️⃣ Null Key Handling

- HashMap allows **one null key**  
- Null key is always stored at **bucket index 0**  
- Multiple **null values** are allowed


## 🔄 Time Complexity

| Operation | Average Case | Worst Case |
|-----------|--------------|------------|
| put()     | O(1)         | O(log n)  |
| get()     | O(1)         | O(log n)  |



# Linked HashMap

The `LinkedHashMap` in Java works similar to a `HashMap`, but the key difference is that `LinkedHashMap` maintains the insertion order, whereas `HashMap` does not guarantee any specific order.

`LinkedHashMap` preserves insertion order by using a doubly-linked list–based data structure that maintained alongside the HashTable. Each entry is connected to the next and previous entries in the map, regardless of where they are stored in the hash table.

Like a regular `HashMap`, `LinkedHashMap` stores data in hash buckets using a hashing mechanism to determine the bucket index. However, to maintain insertion order, each new entry is appended to the end of a globally maintained doubly-linked list. Each node in this list contains `before` and `after` references, which link the previous and next entries to preserve the sequence.

This means the hash table handles the **lookup location**, while the doubly-linked list handles the **sequence order**.

When you request an iterator to traverse the map (for example, using a `for-each` loop or calling `entrySet().iterator()`):

- The iterator ignores the structure of the hash table buckets entirely.
- Instead, it starts at the `head` of the global doubly-linked list and follows the `after` pointers from one entry to the next until it reaches the `tail`.

Because the list is constructed sequentially during insertion, following these links guarantees that elements are accessed in the exact order they were originally added to the map.

# ConcurrentHashMap

Source: https://dzone.com/articles/how-concurrenthashmap-works-internally-in-java
- https://medium.com/@shivu.a.1945/concurrenthashmap-how-it-works-and-why-its-so-damn-fast-also-where-s-my-thread-605bccbad7a7

## Introduction

As we have seen above the HashMap is used for storing data in the form of key-value pairs. If we use this HashMap to store the data that may be accessed by multiple threads we will end up with `ConcurrentModificationException`.  You may think that we can still use HashMap by synchronizing it externally using `Collections.synchronizedMap(new HashMap<>())` But it's like putting the data in a house and allowing only one thread at a time to access. One-In & One-Out. 

To overcome this issue `ConcurrentHashMap` was introduced. Concurrent HashMap works in such a way that instead of locking complete house, let's restrict access at room level. So multiple rooms can be accessed at a time by multiple threads without disturbing each other. 

## Conclusion

`ConcurrentHashMap` works very much similar HashMap except that while HashMap doesn't allow multiples thread to modify the map concurrently, the `ConcurrentHashMap` allows this behavior. This is achieved by dividing the internally created Hash buckets in segments. So instead of locking complete Hash bucket array, here only each bucket maintains their own lock allowing multiple threads to access multiple buckets concurrently. 

Think of `ConcurrentHashMap` as a **large cabinet made of many drawers**, not one big box.

Instead of locking the _entire cabinet_ when someone wants to change something, it locks **only the drawer that’s being changed** — and sometimes not even that. Let’s break it down.

A regular `HashMap` also uses buckets, but `ConcurrentHashMap` uses them in a smarter way:
- Each key goes into one specific bucket.
- Threads working on **different buckets** don’t interfere with each other.
- Result Many threads can work in parallel.
- When a thread just wants to **read**, it doesn't lock anything. It simply looks at the bucket and reads the value.
- When a thread wants to insert/update/delete: It **locks only the tiny bucket** (a node or small part), not the whole map. No other threads are blocked except the ones touching the exact same bucket. Imagine 100 people accessing 100 drawers. Only 1 drawer is locked; the other 99 are still open.

## Summery 

ConcurrentHashMap works much like a regular HashMap, but it allows multiple threads to access and modify it at the same time without corrupting the data. Instead of locking the entire internal array of buckets, it achieves concurrency by locking only the specific bucket (or even the specific node) that a thread is modifying. This means different threads can safely work on different buckets simultaneously. Reads are mostly lock-free, and writes use very small, fine-grained locks or atomic operations (CAS). Because only the affected bucket is locked—not the entire map—Concurrent HashMap provides high performance and true parallel access compared to a fully synchronized HashMap.


# Tree Map

TreeMap is implementation of java Map interface that stores data in the form of key-value pairs in a sorted order using self balancing red-black tree mechanism.

`TreeMap` internally uses a Red-Black Tree, which is a self-balancing binary search tree. This structure ensures that operations like `get()`, `put()`, and `remove()` have a guaranteed time complexity of O(log n), where 'n' is the number of elements in the map.

`TreeMap` does not allow `null` keys by default when using natural ordering, as it relies on key comparison. However, it can allow `null` keys if a custom `Comparator` is provided that handles nulls. `null` values are always permitted.

## Self-Balancing Binary Search Tree

A self-balancing binary search tree is a data structure that automatically maintains a balanced structure while storing elements in a sorted manner. It combines the efficient searching of a binary search tree with the self-adjusting mechanism that ensures the tree remains balanced.

In a binary search tree, each node can have at most two child nodes: a left child and a right child. The elements are arranged in such a way that the value of any node's left child is smaller, and the value of its right child is greater. This allows for fast searching by comparing values and moving down the tree accordingly.

However, over time, the initial balance of the tree may be disrupted due to insertions or deletions, resulting in an inefficient and skewed structure. This is where self-balancing binary search trees come into play. They automatically make adjustments after each insertion or deletion, ensuring that the tree remains balanced.

By employing different balancing techniques, such as rotations and re-coloring, self-balancing binary search trees distribute the elements in a way that guarantees a relatively equal number of elements on both sides of each node. As a result, the tree's height remains logarithmic, which ensures efficient searching, insertion, and deletion operations.

Some popular self-balancing binary search tree algorithms include the AVL tree, Red-Black tree, and Splay tree. Each algorithm has its own unique rules and operation strategies to maintain balance and optimize performance.

