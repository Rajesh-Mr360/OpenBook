Multi-threaded programs may often come to a situation where multiple threads try to access the same resources and finally produce erroneous and unforeseen results.

## Java Synchronization

Java synchronization solves the problem of concurrent access to shared resources by multiple threads. When multiple threads are executing concurrently, they may access shared resources such as variables, objects, or methods simultaneously. Without proper synchronization, this concurrent access can lead to data corruption, inconsistent behaviour, and race conditions.

## How Synchronization works in Java?

Synchronization in Java works by ensuring that only one thread can access a synchronized block of code or method at a time. This prevents concurrent access to shared resources and helps maintain data consistency and integrity in multi-threaded programs. Here’s how synchronization works in Java:

1. **Locking Mechanism:** When a thread enters a synchronized block of code or method, it attempts to acquire a lock associated with the object or class that owns the synchronized block. If the lock is available, the thread acquires the lock and proceeds to execute the synchronized code. If the lock is not available (i.e., another thread holds the lock), the thread enters a blocked state and waits until the lock becomes available.
2. **Exclusive Access:** Once a thread acquires the lock, it has exclusive access to the synchronized block of code or method. Other threads that attempt to enter the synchronized block are blocked until the owning thread releases the lock by exiting the synchronized block or method.
3. **Reentrant Locks:** Java supports reentrant locks, which allow a thread to acquire the same lock multiple times without deadlocking itself. Reentrant locks maintain a count of the number of times a thread has acquired the lock and ensure that the lock is released only when the thread exits the synchronized block or method the same number of times it entered it.
4. **Intrinsic Locks:** In Java, every object has an associated intrinsic lock (also known as a monitor lock) that can be used for synchronization. When a thread enters a synchronized block or method, it acquires the intrinsic lock of the object on which the synchronized block is synchronized. This ensures that only one thread can execute the synchronized block for that object at a time.
5. **Coordinated Access:** Synchronization mechanisms like locks and monitors help coordinate access to shared resources among multiple threads. By ensuring that only one thread can access a critical section of code or data at a time, synchronization prevents race conditions, data corruption, and inconsistent state.

Overall, synchronization in Java provides a powerful mechanism for writing thread-safe concurrent programs and ensuring correct behaviour in multi-threaded environments.


---

## Lock and Monitor in Java concurrency

In Java, concurrency is a technique that allows multiple tasks or processes to run simultaneously on a single processor or multiple processors. It can improve the performance and responsiveness of applications.

However, it also introduces new challenges and complexities to the Java developers, such as synchronization and deadlock. To handle these complexities, Java provides a lock and monitor. Both are correlated to each other and used to synchronize access to shared resources and ensure thread safety.

### Lock vs Monitor

**Monitor** : When we work in a multi-threading environment, where multiple threads access shared resources then, we need some way to ensure that only one thread accesses a resource at a time. The core of the synchronization is the monitor which is an object that establishes mutually exclusive lock. **The monitor is like a synchronized region that can be acquired by only one thread at a specific time**.

**Lock** : If any thread want to access instance variables of that object; then thread must “own” the object’s lock. Threads request to acquire the Lock object through `tryLock()` method. When lock gets assigned to it and it releases the lock after the completion of task. All other threads that attempt to access the object’s variables have to wait in a Queue until the owning thread releases the object’s lock. 

Once a thread owns a lock, it can request the same lock again multiple times, but then has to release the lock the same number of times before it is made available to other threads. For example, If a thread requests a Lock three times, that thread will continue to own the lock until it has released it three times.

> [!NOTE]
> The Lock and Monitor are the base of synchronization. Logically speaking, there is no difference between them, they actually complement each other. When a thread acquires a **Lock**, it enters the **Monitor**, which is a synchronized region.


## Synchronization

There are two type of Thread Synchronization in Java.
1. Mutual Exclusive
2. Cooperation (Inter - thread communication)

<span style="background:#ff4d4f">TODO: Explain about the above points.</span>


### Real world example
Let’s consider a scenario where multiple threads represent spectators trying to buy tickets for a sports event. Without synchronization, multiple spectators might end up buying the same ticket, leading to overbooking or inconsistencies in ticket sales. With synchronization, we can ensure that only one spectator can buy a ticket at a time, preventing these issues.

**Java Code without Synchronization (Problematic)**

```Java ln:false
import java.util.ArrayList;  
import java.util.List;  
import java.util.Random;  
  
class TicketCounter {  
	private int totalTickets;  
	private List<Integer> tickets;  
	  
	public TicketCounter(int totalTickets) {  
		this.totalTickets = totalTickets;  
		tickets = new ArrayList<>();  
		for (int i = 1; i <= totalTickets; i++) {  
			tickets.add(i);  
		}  
	}  
	  
	public int buyTicket() {  
		if (tickets.isEmpty()) {  
			return -1; // No tickets available  
		}  
		Random random = new Random();  
		int index = random.nextInt(tickets.size());  
		int ticketNumber = tickets.remove(index);  
		return ticketNumber;  
	}  
}  
  
class SpectatorThread extends Thread {  
	private TicketCounter ticketCounter;  
	private String spectatorName;  
	  
	public SpectatorThread(TicketCounter ticketCounter, String spectatorName) {  
		this.ticketCounter = ticketCounter;  
		this.spectatorName = spectatorName;  
	}  
	  
	@Override  
	public void run() {  
		int ticketNumber = ticketCounter.buyTicket();  
		if (ticketNumber == -1) {  
			System.out.println(spectatorName + " couldn't buy a ticket. Tickets sold out.");  
		} else {  
			System.out.println(spectatorName + " bought ticket number: " + ticketNumber);  
		}  
	}  
}  
  
public class TicketSaleWithoutSynchronization {  
	public static void main(String[] args) {  
		TicketCounter ticketCounter = new TicketCounter(10); // Total tickets available  
		  
		// Create multiple spectator threads  
		SpectatorThread spectator1 = new SpectatorThread(ticketCounter, "Spectator 1");  
		SpectatorThread spectator2 = new SpectatorThread(ticketCounter, "Spectator 2");  
		SpectatorThread spectator3 = new SpectatorThread(ticketCounter, "Spectator 3");  
		  
		// Start the spectator threads  
		spectator1.start();  
		spectator2.start();  
		spectator3.start();  
	}  
}
```

In this code, multiple `SpectatorThread` instances represent spectators trying to buy tickets from a `TicketCounter`. However, without synchronization, multiple spectators might end up buying the same ticket, leading to overbooking or selling out of tickets incorrectly.


**Java Code with Synchronization (Solution)**

```Java ln:false
import java.util.ArrayList;  
import java.util.List;  
import java.util.Random;  
  
class SynchronizedTicketCounter {  
	private int totalTickets;  
	private List<Integer> tickets;  
	  
	public SynchronizedTicketCounter(int totalTickets) {  
		this.totalTickets = totalTickets;  
		tickets = new ArrayList<>();  
		for (int i = 1; i <= totalTickets; i++) {  
			tickets.add(i);  
		}  
	}  
	  
	public synchronized int buyTicket() {  
		if (tickets.isEmpty()) {  
			return -1; // No tickets available  
		}  
		Random random = new Random();  
		int index = random.nextInt(tickets.size());  
		int ticketNumber = tickets.remove(index);  
		return ticketNumber;  
	}  
}  
  
class SynchronizedSpectatorThread extends Thread {  
	private SynchronizedTicketCounter ticketCounter;  
	private String spectatorName;  
	  
	public SynchronizedSpectatorThread(SynchronizedTicketCounter ticketCounter, String spectatorName) {  
		this.ticketCounter = ticketCounter;  
		this.spectatorName = spectatorName;  
	}  
	  
	@Override  
	public void run() {  
		synchronized (ticketCounter) {  
			int ticketNumber = ticketCounter.buyTicket();  
			if (ticketNumber == -1) {  
				System.out.println(spectatorName + " couldn't buy a ticket. Tickets sold out.");  
			} else {  
				System.out.println(spectatorName + " bought ticket number: " + ticketNumber);  
			}  
		}  
	}  
}  
  
public class TicketSaleWithSynchronization {  
	public static void main(String[] args) {  
		SynchronizedTicketCounter ticketCounter = new SynchronizedTicketCounter(10); // Total tickets available  
		  
		// Create multiple synchronized spectator threads  
		SynchronizedSpectatorThread spectator1 = new SynchronizedSpectatorThread(ticketCounter, "Spectator 1");  
		SynchronizedSpectatorThread spectator2 = new SynchronizedSpectatorThread(ticketCounter, "Spectator 2");  
		SynchronizedSpectatorThread spectator3 = new SynchronizedSpectatorThread(ticketCounter, "Spectator 3");  
		  
		// Start the synchronized spectator threads  
		spectator1.start();  
		spectator2.start();  
		spectator3.start();  
	}  
}
```

In this code, `SynchronizedTicketCounter` class and `SynchronizedSpectatorThread` class are introduced. The `buyTicket()` method of `SynchronizedTicketCounter` class is now synchronized to ensure that only one spectator can buy a ticket at a time. Additionally, in `SynchronizedSpectatorThread` class, the `run()` method is synchronized on the `ticketCounter` object to ensure thread safety while buying tickets.

This synchronization ensures that spectators can’t buy the same ticket simultaneously, solving the problem of overbooking or incorrect ticket sales.


## Deadlock Scenario
Deadlock occurs in a multi-threaded environment when two or more threads are blocked forever, each waiting for the other to release a resource, resulting in a deadlock situation where none of the threads can proceed.