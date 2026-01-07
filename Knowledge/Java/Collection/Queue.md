# Queue
The interface Queue is available in the `java.util` package and does extend the Collection interface. It is used to keep the elements that are processed in the **First In First Out (FIFO)** manner. It is an ordered list of objects, where insertion of elements occurs at the end of the list, and removal of elements occur at the beginning of the list.

**Some important points to remember:**

- As discussed earlier, FIFO concept is used for insertion and deletion of elements from a queue.
- The Java Queue provides support for all of the methods of the Collection interface including deletion, insertion, etc.
- `PriorityQueue` , `ArrayBlockingQueue` and `LinkedList` are the implementations that are used most frequently.


## PriorityQueue
PriorityQueue is also class that is defined in the collection framework that gives us a way for processing the objects on the basis of priority. It is already described that the insertion and deletion of objects follows FIFO pattern in the Java queue. However, sometimes the elements of the queue are needed to be processed according to the priority, that's where a PriorityQueue comes into action.

You must provide a Comparator when creating the PriorityQueue to define the ordering. Or the elements class must implement `Comparable` , and override `compare()` method otherwise it will throw `ClassCastException` at runtime.