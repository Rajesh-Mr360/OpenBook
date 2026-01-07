# Set
`Set` is an unordered collection of elements which doesn’t allow duplicate values. Even if we try to add an element that is already present in the set, it will not store it. Set allows to store one null element. `Set` is implemented by `HashSet` , `LinkedHashSet`  and `TreeSet`.

## HashSet
A few important features of HashSet are mentioned below:
1. Implements `Set` interface.
2. The underlying data structure for HashSet is `HashMap` .
3. As it implements the Set Interface, duplicate values are not allowed.
4. Objects that you insert in HashSet are not guaranteed to be inserted in the same order. Objects are inserted based on their hash code.
5. HashSet allows to store one null element.
6. HashSet also implements Serializable and Cloneable interfaces.


**Internal working of Set :**

```Java
/**
 * Constructs a new, empty set; the backing HashMap instance has 
 * default initial capacity (16) and load factor (0.75).
 */
public HashSet() {  
    map = new HashMap<>();  
}
```
Now as you can see that whenever we create a HashSet, it internally creates a HashMap and if we insert an element into this HashSet using `add()` method, it actually call `put()` method on internally created HashMap object with element you have specified as it’s key and constant Object called `PRESENT` as it’s value. So we can say that a Set achieves uniqueness internally through HashMap. Now the whole story comes around how a HashMap and `put()` method internally works. As we know in a HashMap each key is unique and when we call put`(Key, Value)` method, it returns the previous value associated with key, or null if there was no mapping for key. So in `add()` method we check the return value of `map.put(key, value)` method with null value.

>  If `map.put(key, value)` returns `null` , then the statement `map.put(e, PRESENT) == null` will return true and element is added to the HashSet(internally HashMap).
> 
>  If `map.put(key, value)` returns old value of the key, then the statement `map.put(e, PRESENT) == null` will return false and element is not added to the HashSet(internally HashMap).


**Note that this implementation is not synchronized.** If multiple threads access a hash set concurrently, and at least one of the threads modifies the set, it must be synchronized externally. This is typically accomplished by synchronizing on some object that naturally encapsulates the set. If no such object exists, the set should be "wrapped" using the `Collections.synchronizedSet()` method. This is best done at creation time, to prevent accidental unsynchronized access to the set.


## LinkedHashSet

==LinkedHashSet is an extended version of HashSet. HashSet doesn’t follow any order where as LinkedHashSet maintains insertion order. HashSet uses HashMap object internally to store it’s elements where as LinkedHashSet uses LinkedHashMap object internally to store and process it’s elements==.
you might have noticed that all 4 constructors are calling the same super class constructor. This constructor is a package private constructor which is used only by the LinkedHashSet class. This constructor takes initial capacity, load factor and one `Boolean` dummy value as it’s arguments. This `Boolean` dummy value is just used to differentiate this constructor from other constructors of HashSet class which take initial capacity and load factor as their arguments. Here is the how this constructor is defined in HashSet class.

```java ln:false title:"HashSet.java"
public HashSet(int initialCapacity, float loadFactor, boolean dummy) {
	map = new LinkedHashMap<>(initialCapacity, loadFactor);
}
```

Did you see that ? this constructor internally creates one new `LinkedHashMap` object. This LinkedHashMap object is used by the LinkedHashSet to store it’s elements.

LinkedHashSet doesn’t have it’s own methods. All methods are inherited from it’s super class HashSet. So, all operations on LinkedHashSet work in the same manner as that of HashSet. The only change is the internal object used to store the elements. In HashSet, elements you insert are stored as keys of HashMap object. Where as in LinkedHashSet, elements you insert are stored as keys of LinkedHashMap object. The values of these keys will be the same constant i.e. `PRESENT` .


## SortedSet
The Java `SortedSet`  interface, `java.util.SortedSet` , is a subtype of the `java.util.Set` interface. The Java SortedSet interface behaves like a normal Set with the exception that the elements it contains are sorted internally. This means that when you iterate the elements of a SortedSet the elements are iterated in the sorted order.

All elements inserted into a sorted set must implement the Comparable interface. Attempts to violate this restriction will cause the offending method or constructor invocation to throw a `ClassCastException` .


## TreeSet
- Java TreeSet class contains unique elements only like HashSet.
- Java TreeSet class access and retrieval times are quite fast.
- Java TreeSet class doesn't allow null elements.
- Java TreeSet class is non-synchronized.
- Java TreeSet class maintains ascending order.
- The TreeSet can only allow those generic types that are comparable.