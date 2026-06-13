`lock.tryLock()` in Java is a **non-blocking attempt to acquire a lock**.
### **Normal `lock()`**
- When you call `lock.lock()`, the thread will **wait** (block) until the lock becomes available.
- If another thread is holding the lock, your thread just sits there until it can proceed.

### **`tryLock()`**

- Instead of waiting, `tryLock()` **immediately returns**:
    - `true` if the lock was acquired successfully.
    - `false` if the lock is already held by another thread.
- The thread **does not block** if it fails to get the lock.

```java
boolean tryLock();
boolean tryLock(long time, TimeUnit unit) throws InterruptedException;
```

1. **`tryLock()` without parameters**
    - Instantaneous attempt.
    - Useful if you want to skip work rather than wait.
```java
if (lock.tryLock()) {
    try {
        // Got the lock, do work
    } finally {
        lock.unlock();
    }
} else {
    // Couldn't get lock, do something else
}

```

2. **`tryLock(timeout, unit)`**
    
    - Waits up to the given time to acquire the lock.
    - If lock becomes available during the timeout, returns `true`.
    - If time expires, returns `false`.
    - Can throw `InterruptedException` if the waiting thread is interrupted.
    
    Example:

```java
if (lock.tryLock(500, TimeUnit.MILLISECONDS)) {
    try {
        // Work with lock
    } finally {
        lock.unlock();
    }
} else {
    // Timed out, handle accordingly
}
```