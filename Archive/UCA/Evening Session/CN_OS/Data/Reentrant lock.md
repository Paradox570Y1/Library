# Race condition

[[ExampleCode]]
- Here thread1 and thread2 are simultaneously updating the shared resource, which results in lost update. (Reader Writer Problem)
	- Semaphore example
		- There are multiple tolls for cars to pass.
	- Mutex example(lock)
		- There is only one toll for cars to pass.



# How to solve this issue
[[ExampleCode]]
[[tryLock() Method]]
- Use `sychronized` keyword in common shared resource method.
	![[Pasted image 20250728203137.png|400]]
	- Java, `synchronized` is the simplest way to make sure **only one thread** at a time can execute a certain block of code. But `synchronized` has limitations:

| Feature                         | `synchronized` | `ReentrantLock`           |
| ------------------------------- | -------------- | ------------------------- |
| Try to acquire without blocking | ❌              | ✅ (`tryLock()`)           |
| Interrupt while waiting         | ❌              | ✅ (`lockInterruptibly()`) |
| Fair ordering (FIFO)            | ❌              | ✅ (constructor flag)      |
| Multiple `Condition` variables  | ❌              | ✅ (`newCondition()`)      |
| Explicit lock/unlock control    | ❌              | ✅                         |


# Reentrant Lock

- Make a custom lock using `ReentrantLock()`
	![[Pasted image 20250728203834.png]]

## **0. Must-know facts about ReentrantLock**

- **Always** call `unlock()` in a `finally` block to prevent lock leaks.
- Reentrant means a thread can lock multiple times before unlocking.
- You can check lock state with:
    - `isLocked()`
    - `isHeldByCurrentThread()`
    - `getHoldCount()`
- Use `tryLock(timeout, unit)` if you want to avoid blocking forever.
- `ReentrantLock` gives you **more control** but also **more responsibility** than `synchronized`.

So, `ReentrantLock` is part of **`java.util.concurrent.locks`** — it’s a more flexible, more feature-rich replacement for `synchronized`.
"Reentrant" means:  
If the thread that already owns the lock tries to acquire it again, it **doesn’t block itself** — instead, it increases an **internal hold count**.

```java
ReentrantLock lock = new ReentrantLock();

lock.lock();   // hold count = 1
lock.lock();   // hold count = 2 (same thread)
lock.unlock(); // hold count = 1
lock.unlock(); // hold count = 0 → actually releases
```
Without reentrancy, a thread could deadlock itself if it tried to acquire a lock it already holds.

# Non-reentrant lock
Normally, a **non-reentrant lock** does not allow a thread that already holds the lock to acquire it again. If the same thread tries to lock it twice, it will **wait for itself** — which can never happen — and thus get stuck forever (**self-deadlock**).

---

### **Example of self-deadlock with a non-reentrant lock**

Imagine we had a "simple lock" (not reentrant):

```java
SimpleLock lock = new SimpleLock();

public void outer() {
    lock.lock();  // acquires lock
    inner();      // calls another method that also tries to lock
    lock.unlock();
}

public void inner() {
    lock.lock();  // ❌ waits forever — but the same thread already has it!
    // ...
    lock.unlock();
}

```
Here:

- Thread enters `outer()` and locks the resource.
- Inside `outer()`, it calls `inner()` which also tries to lock the same resource.
- Because the lock isn’t reentrant, the lock sees “resource already locked” and makes the thread wait… but that thread **is the one holding it**, so it can’t progress to unlock. That’s **self-deadlock**.

### **How ReentrantLock fixes this**

With a **reentrant lock**:

- When the thread already holding the lock calls `lock()` again, it doesn’t block.
- Instead, it increases an **internal counter** (hold count).
- The thread must call `unlock()` the same number of times before the lock is actually released.

```java
ReentrantLock lock = new ReentrantLock();

public void outer() {
    lock.lock();   // hold count = 1
    inner();       // hold count = 2 after lock in inner()
    lock.unlock(); // hold count = 1
    lock.unlock(); // hold count = 0 → actually releases
}

public void inner() {
    lock.lock();
    // do stuff
    lock.unlock();
}
```

This way, the **same thread** can safely enter multiple synchronized sections guarded by the same lock without blocking itself.

## **3. How it works internally (conceptually)**

1. **Thread calls `lock()`** → If lock is free, thread becomes the owner; if not, it waits.
2. **Thread calls `unlock()`** → Decrements hold count; if it reaches zero, lock is released and another waiting thread may get it.
3. **Fair mode (optional)** → If created with `new ReentrantLock(true)`, threads get the lock in **first-come-first-serve** order.  
    If false (default), lock is **unfair** and may allow barging (better throughput, less fairness).

## **4. Synchronization behavior**

When you protect code with a `ReentrantLock`, you ensure **mutual exclusion** — at most **one thread** at a time can execute that code.

#final_keyword
- **Meaning:** Once a variable is assigned a value, it cannot be reassigned.
- For **primitives** → value itself can’t change.
- For **references** → the reference can’t point to a different object, but the object’s internal state can still change (unless the object is immutable).
- Declaring the **lock reference** as `final` so that once it is assigned, it **cannot point to a different lock object** later.  
	This is a **best practice** for synchronization fields, because:
	- It ensures all threads are synchronizing on the **same lock object** for the life of the instance.
	- Avoids accidental reassignment, which could break thread safety.

```java
import java.util.concurrent.locks.ReentrantLock;

public class Counter {
    private int count = 0;
    private final ReentrantLock lock = new ReentrantLock();

    public void increment() {
        lock.lock();  // acquire
        try {
            count++;
        } finally {
            lock.unlock(); // always release in finally!
        }
    }

    public int getCount() {
        lock.lock();
        try {
            return count;
        } finally {
            lock.unlock();
        }
    }
}

```

Here:
- Multiple threads can call `increment()` safely without race conditions.
- The `try/finally` ensures lock release **even if an exception happens**.

