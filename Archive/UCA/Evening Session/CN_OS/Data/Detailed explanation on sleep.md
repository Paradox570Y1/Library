# What `Thread.sleep(...)` actually does

- `Thread.sleep(ms)` tells the JVM to _pause the current thread_ for at least `ms` milliseconds.
- The sleeping thread moves into the `TIMED_WAITING` state; the OS/JVM scheduler can run other threads.
- **Important:** sleep is a _timing / throttling_ primitive — **not** a synchronization primitive.
	- `Thread.sleep(...)` is designed **only** to control _when_ a thread runs, **not** to coordinate _how_ threads interact with each other.
### **Timing / throttling primitive**

- **Timing:** You can pause a thread for a specific amount of time.  
    Example: slowing down polling, adding a fixed delay, or pacing CPU usage.
- **Throttling:** Used to prevent a loop from running at full speed (e.g., limit request rate).

```java
for (int i = 0; i < 5; i++) {
    System.out.println("Tick " + i);
    Thread.sleep(1000); // delay between ticks
}
```

### **Not a synchronization primitive**

- Synchronization primitives exist to manage **safe access to shared data** and to **coordinate thread actions**.
    
- Examples:
    - `synchronized`
    - `ReentrantLock`
    - `Semaphore`
    - `CountDownLatch`
    - `wait()/notify()`
    - `Condition` objects
- These ensure correct ordering and prevent race conditions.

# Key point: sleep does **not** release locks

- If a thread is inside a `synchronized` block (owns the monitor) or holds a `ReentrantLock` and calls `Thread.sleep(...)`, it **keeps ownership of those locks** while sleeping.
- Other threads that need those locks remain blocked until the sleeping thread exits the synchronized block or releases the lock explicitly.