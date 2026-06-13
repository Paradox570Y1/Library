Java defines **exactly six thread states** in `Thread.State`.  
These represent the _logical_ state of the thread **inside the JVM**.

Let’s go one by one:

---

# **1. NEW**

The thread object is created but **`start()` is not called yet**.

`Thread t = new Thread(() -> {}); // State: NEW`

✔ Exists in memory  
✔ Has never run  
❌ Not scheduled by CPU yet

---

# **2. RUNNABLE**

‼️ Important: In Java, _RUNNABLE means both “Ready to run” and “Actually running”_.

The moment you call:

`t.start();`

the thread becomes **RUNNABLE**.

So RUNNABLE includes:

- **Ready/Waiting for CPU time**
    
- **Currently running on CPU**
    

Java **does NOT have separate Ready + Running** states.

---

# **3. BLOCKED**

Thread wants to enter a **synchronized block**, but another thread already holds the lock.

Example:

```java
synchronized(lock) {     // Thread A holds lock 
}  
synchronized(lock) {     // Thread B tries to enter → BLOCKED 
}
```

BLOCKED **only means waiting to acquire a monitor lock**.

➡️ It is NOT waiting for sleep, or join, or I/O—only lock.

---

# **4. WAITING**

Thread waits **indefinitely** (no time limit).

Happens when:

###### `Object.wait()`

```java
synchronized(lock) {
    lock.wait();  // indefinitely
}
```
###### `Thread.join()` (without timeout)

```java
t.join();  // wait forever until t finishes
```

###### `LockSupport.park()`

Thread is **waiting for another thread to signal it**.

---

# **5. TIMED_WAITING**

Same as WAITING but **with a time limit**.

Happens when:

###### `sleep(time)`

`Thread.sleep(2000);  // timed waiting`

###### `wait(time)`

`lock.wait(5000);`

###### `join(time)`

`t.join(1000);`

###### `parkNanos()` or `parkUntil()`

Thread will automatically wake up when:

- time completes OR
    
- it gets notified
    

---

# **6. TERMINATED**

Thread has finished executing its `run()` method.

```java
public void run() {
    System.out.println("done");
}
// After run completes → TERMINATED
```

Also happens if:

- The thread thrown an exception
- The thread completed normally

This is the **final state**.

---

# 🧠 **Summary Table**

| State             | Meaning                  | Example            |
| ----------------- | ------------------------ | ------------------ |
| **NEW**           | Created, not started     | new Thread()       |
| **RUNNABLE**      | Ready or running         | start()            |
| **BLOCKED**       | Waiting for monitor lock | synchronized(lock) |
| **WAITING**       | Waiting indefinitely     | wait(), join()     |
| **TIMED_WAITING** | Waiting with timeout     | sleep(1000)        |
| **TERMINATED**    | Finished run()           | after completion   |