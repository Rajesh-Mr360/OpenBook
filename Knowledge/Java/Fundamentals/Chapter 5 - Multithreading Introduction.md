## What is Multithreading?

Multithreading in Java is the process of executing multiple threads at the same time for the maximum utilization of CPU. A thread in Java is indeed a lightweight process within a program that can be executed to perform some operation concurrently with the main program. 

In Java, there are two types of threads, <font color="#92d050">Daemon threads</font> and <font color="#92d050">Non-Daemon threads</font>. Daemon threads are basically low priority threads that used to perform supporting tasks, while Non-Daemon threads are the high priority threads that designed to perform specific tasks.

In fact, JVM always waits until non-daemon threads to finish their work. It never exits until the last non-daemon thread finishes its work.

---
## Thread lifecycle

The thread lifecycle in Java refers to the various stages a thread goes through during its execution.
Here's a breakdown of the different states and their characteristics:

1. **New State**
	- This is the initial state when a thread object is created using the `Thread` class constructor or by implementing the `Runnable` interface.
	- The thread hasn't been scheduled to run yet and doesn't have any resources allocated to it.
2. **Runnable State**
	- In this state, the thread object is ready to run. It might be waiting for its turn to be scheduled by the thread scheduler in the operating system. The thread might also be waiting for resources to become available (e.g., waiting for a file to be unlocked).
	- The thread might also be paused in the Runnable state because it's waiting for resources to become available. This could involve waiting for an I/O operation to complete (like reading from a file) or waiting to acquire a lock on a shared resource to prevent data corruption.
3. **Running State**
	- This is the active state where the thread is currently executing its defined tasks.
	- The thread is assigned resources (CPU time, memory) by the operating system and is actively processing instructions.
4. **Waiting State**
	- The thread is temporarily suspended because it's waiting for an event to occur before it can continue.
	- Common reasons for blocking include:
		1. Waiting for I/O operations (e.g., reading from a file, network communication)
		2. Waiting to acquire a lock on a shared resource to prevent race conditions
		3. Waiting for another thread to finish a task
5. **Dead State**
	- This is the final state of a thread.
	- The thread has finished executing its tasks and has released all its resources.
	- A thread can reach this state for various reasons:
		1. The `run` method of the thread completes successfully.
		2. An uncaught exception is thrown within the `run` method.
		3. The `stop()` method (deprecated due to safety concerns) is called on the thread.
---

### Lock vs Monitor
**Monitor :** The monitor is like a synchronized region that can be acquired by only one thread at a specific time. 
**Lock :** When multiple threads try to access a shared resource then, the Lock object restricts access to a single thread at a time through `lock()` and `unlock()` methods.
## Wait and Notify

In a nutshell, Locks provide necessary support for implementing Monitors. Long answer read below.
- **Wait - Set :** The ability to make threads wait for certain conditions to be true.
- **Entry - Set :** An entry set is used to hold the threads that are already requested for the lock and the lock is not acquired by them yet.

## What is a Lock

A lock is kind of data which is logically part of an object’s header on the heap memory. Each object in a JVM has this lock (or mutex) that any program can use to coordinate multi-threaded access to the object. If any thread want to access instance variables of that object; then thread must “own” the object’s lock (set some flag in lock memory area). All other threads that attempt to access the object’s variables have to wait until the owning thread releases the object’s lock (unset the flag).

Once a thread owns a lock, it can request the same lock again multiple times, but then has to release the lock the same number of times before it is made available to other threads. If a thread requests a lock three times, for example, that thread will continue to own the lock until it has “released” it three times.

Please note that lock is acquired by a thread, when it explicitly ask for it. In Java, this is done with the synchronized keyword, or with wait and notify.

**Implementation:**

- **Implicit Locks (Monitors):** Java provides implicit locks associated with every object. Using the `synchronized` keyword on a method or code block automatically acquires and releases the lock on the object for that thread.
- **Explicit Locks (Java Concurrency API):** The `java.util.concurrent` package offers explicit locks via the `Lock` interface. This gives you more fine-grained control over synchronization, allowing you to create custom lock objects and use methods like `lock()`, `unlock()`, and `tryLock()` for advanced scenarios.

**Example (Implicit Lock)**
```Java ln:false
public class Counter { 
	private int count = 0; 
	public synchronized void increment() { 
		count++; 
	} 
}
```

In this example, the `synchronized` keyword ensures that only one thread can execute the `increment()` method at a time, protecting the `count` variable.


## What is Monitor

Monitors are a broader synchronization construct in Java concurrency that combine locks (mutual exclusion) with the ability for threads to wait for specific conditions to be met before proceeding (cooperation). Threads can call `wait()` within a synchronized block to relinquish control of the lock and enter a waiting state until another thread signals a condition using `notify()` or `notifyAll()`. This enables coordination between threads based on specific events.

**Relationship Between Locks and Monitors:**

- Monitors are higher-level abstractions that leverage locks for mutual exclusion.
- Locks are the core mechanism for exclusive access, while monitors add capabilities for thread cooperation through waiting and signalling.

Monitors are used to achieve mutual exclusion and synchronization. Before jumping into monitor, we need to understand two things. **Mutual exclusion** and **Cooperation/Synchronization**.

### Mutual Exclusion

Each object is associated with a monitor and this monitor has a **lock** where each thread can lock or unlock the object using this **lock** when it accesses the shared variables. Explicitly, it means only one thread at a time may hold a **lock** on a monitor. Any other threads attempting to lock that lock are blocked until they can obtain the lock.

When a new thread tries to acquire the lock and if already a thread owns the lock, then that thread will be waiting on the **entry set** to acquire the lock. When the thread which is acquired the lock completes its critical section, it will release the lock. So next thread will acquire the lock, but this next thread is taken from the entry set and will be determined by JVM based on some criteria like FIFO.


### Cooperation/Synchronization

Synchronization is achieved using the <font color="#9bbb59">Wait - Set</font> which is associated with the monitor and the <font color="#9bbb59">wait and notify</font> or <font color="#9bbb59">signal and continue</font> mechanism. Synchronization is important when one thread needs some data to be in a particular state, and another thread is responsible for getting the data into that state e.g. <font color="#9bbb59">producer/consumer</font> problem.

When a thread calls the `wait()` method with respect to the object then the thread is suspended and added to the <font color="#9bbb59">wait - set</font> to wait until some other thread invokes `notify()` or `notifyAll()` on the same object. The `notify()` method is used for waking up threads that are in the <font color="#9bbb59">wait - set</font> of the monitor of a particular object. There are two ways of notifying waiting threads.

`notify()`
	For all threads waiting on <font color="#9bbb59">wait - set</font> the method `notify()` notifies anyone of them to wake up arbitrarily. The choice of exactly which thread to wake is non-deterministic and depends upon the JVM.
	
`notifyAll()`
	This method simply wakes all threads that are waiting on the <font color="#9bbb59">wait - set</font>. The awakened threads will not be able to proceed until the current thread releases the lock on this object. The awakened threads will compete in the usual manner with any other threads that might be actively competing to synchronize.

---
## ThreadPool

In Java, a thread pool is a collection of reusable threads that are managed by a thread pool executor. It provides a mechanism to manage the creation and execution of tasks without creating new threads for each task. This helps to improve performance and resource utilization.

Here's a breakdown of how thread pools work:

1. #Thread_Creation 
	A fixed number of threads (worker threads) are initially created in the pool.
2. #Task_Submission 
	Tasks (`Runnable` or `Callable`) are submitted to the thread pool executor.
3. #Task_Queueing 
	If no idle threads are available, the tasks are queued until a thread becomes available.
4. #Task_Execution 
	An idle thread from the pool picks up a task from the queue and executes it.
5. #Thread_Reuse 
	Once a thread finishes executing a task, it becomes available to handle the next task in the queue.


Java provides various ThreadPool implementations through the `java.util.concurrent` package. They are:

> 1. **FixedThreadPool**
> 2. **CachedThreadPool**
> 3. **ScheduledThreadPool**
> 4. **SingleThreadExecutor**

### Fixed Thread Pool

This type of thread pool creates a fixed number of threads that are reused to execute multiple tasks. Once all the threads are being used, new tasks are placed in a queue and are executed as soon as a thread becomes available.

```Java ln:false 
Executor executor = Executors.newFixedThreadPool(5);

for (int i = 0; i < 10; i++) {  
	Runnable worker = new WorkerThread("" + i);  
	executor. Execute(worker);  
}
```

In this example, a fixed thread pool with 5 threads is created and 10 tasks are submitted to it. Since the number of threads is less than the number of tasks, some of the tasks will be placed in a queue and executed as soon as a thread becomes available.


### Cached Thread Pool 

This type of thread pool creates new threads as needed, but also recycles unused threads. This means that the number of threads can be increased or decreased dynamically based on the number of tasks that need to be executed.

```Java ln:false
Executor executor = Executors.newCachedThreadPool();

for (int i = 0; i < 10; i++) {  
	Runnable worker = new WorkerThread("" + i);  
	executor. Execute(worker);  
}
```

In this example, a cached thread pool is created and 10 tasks are submitted to it. The thread pool will create new threads as needed to execute the tasks, but will also recycle unused threads to improve performance.


### Scheduled Thread Pool

Scheduled Thread Pools offer the capability to execute tasks with a delay or at a fixed rate. The following code will create a new scheduled thread pool with thread size 5 and will submit 50 tasks with 1 to 50 seconds delay each. This code will run for 50 seconds

```Java ln:false
int threadCount = 5;  
int numberOfTasks = 50;  
var threadPool = Executors.newScheduledThreadPool(threadCount); 

for (int i = 0; i < numberOfTasks; i++) {  
	String message = "Scheduled task started with " + i + " seconds delay";  
	threadPool.schedule(() -> System.out.println(message), i, TimeUnit.SECONDS);  
}
```

In this example, a scheduled thread pool with 5 threads is created and a task is scheduled to be executed every second.


### Single Thread Executor

It is a type of thread pool that uses a single worker thread to execute tasks. This is useful when you want to ensure that tasks are executed in a specific order.

```Java ln:false
Executor executor = Executors.newSingleThreadExecutor();  

for (int i = 0; i < 10; i++) {  
	Runnable worker = new WorkerThread("" + i);  
	executor. Execute(worker);  
}
```

In this example, a single-threaded executor is created and 10 tasks are submitted to it. The tasks will be executed one at a time in the order that they were submitted.


---

## Thread Scheduler

The scheduler is an integral part of the Java Virtual Machine ( JVM ) and is responsible for assigning processor time to threads.

A component of Java that decides which thread to run or execute and which thread to wait is called a thread scheduler in Java. In Java, a thread is only chosen by a thread scheduler if it is in the runnable state. However, if there is more than one thread in the runnable state, it is up to the thread scheduler to pick one of the threads and ignore the other ones. There are some criteria that decide which thread will execute first. There are two factors for scheduling a thread i.e., <font color="#92d050">Priority</font> and <font color="#92d050">Time Slicing</font>.

### Priority Scheduling

Priority of each thread lies between 1 to 10. If a thread has a higher priority, it means that thread has got a better chance of getting picked up by the thread scheduler. In case more than two threads have the same priority, then CPU allocates time slots for thread execution on the basis of <font color="#00b0f0">first-come, first-serve</font> manner.


**FIFO - First Come First Serve**

Suppose two threads of the same priority enter the runnable state, then priority cannot be the factor to pick a thread from these two threads. In such a case, arrival time of thread is considered by the thread scheduler. A thread that arrived first gets the preference over the other threads.

### Time Slicing Scheduling

Usually, the First Come First Serve algorithm is non-pre-emptive, which is bad as it may lead to infinite blocking (also known as <font color="#ffc000">Starvation</font>). To avoid that, some time-slices are provided to the threads so that after some time, the running thread has to give up the CPU. Thus, the other waiting threads also get time to run their job.

