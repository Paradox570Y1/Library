`wait()` and `notify()` are part of Java’s **low-level thread communication mechanism**, but they operate on **intrinsic locks (monitor locks)**, not `ReentrantLock`.

## **The Core Idea**

Threads sometimes need to **coordinate**:

- One thread may need to **wait** until another thread signals that something has happened.
- Instead of constantly checking in a loop (_busy waiting_), Java lets threads **go to sleep** and be **woken up** when needed.

This is where `wait()` and `notify()` come in.

Think of `wait()` and `notify()` like a **walkie-talkie system** between threads:

- One thread says **"I'm waiting here until you tell me something"** → `wait()`
- Another thread later says **"Hey, you can continue now"** → `notify()`

They help **two or more threads coordinate work** without wasting CPU time by constantly checking a condition.

### **`wait()`**

- **What it does:**  
    Pauses the current thread **and releases the lock** on the object it’s called on.
    
- **Where to use:**  
    Inside a `synchronized` block or `synchronized` method.
    
- **Why:**  
    So other threads can get the lock and change the condition you’re waiting for.
    
- **Keyword behavior:**  
    The thread goes into **WAITING state** until another thread calls `notify()` or `notifyAll()` on the **same object**.

---

### **`notify()`**

- **What it does:**  
    Wakes up **one** thread that is waiting on the same object’s monitor.
    
- **Where to use:**  
    Also inside a `synchronized` block or method.
    
- **Note:**  
    The woken thread won’t run immediately — it must first **reacquire the lock**.

### **Basic Rule**

- Both `wait()` and `notify()` must be called on the **same object** that is used for synchronization.
- Always wrap `wait()` inside a **while loop** that checks the condition to avoid **spurious wakeups**.


```java
class SignalExample {
    private boolean signal = false;

    public synchronized void doWait() throws InterruptedException {
        while (!signal) { // Check condition
            wait(); // Release lock and wait
        }
        System.out.println("Signal received! Proceeding...");
    }

    public synchronized void doNotify() {
        signal = true;
        notify(); // Wake up one waiting thread
    }
}
```

### **Easy way to remember**

- **`wait()`** → “Pause me here and let others work until someone wakes me up.”
- **`notify()`** → “Wake up one person who is waiting.”