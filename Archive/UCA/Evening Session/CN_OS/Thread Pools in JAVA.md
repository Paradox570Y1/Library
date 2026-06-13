## 🧩 What Is a Thread Pool?

> A **Thread Pool** is a **collection (or pool)** of **pre-created worker threads** that can execute multiple tasks **without creating new threads every time**.

Think of it as a **“thread factory + manager”** —  
you give it tasks to run, and it assigns them to available threads in the pool.

---

## ⚙️ Why We Need Thread Pools

Creating and destroying threads frequently is **expensive** —  
it takes memory, CPU, and time.

If you start a new thread for every small task, you can easily:

- overload the CPU,
    
- slow down the system, or
    
- run out of resources (thread explosion 😨).
    

So instead, we:

- create a **fixed number** of threads once,
- keep reusing them for future tasks.

✅ Efficient  
✅ Scalable  
✅ Easy to manage

---

## 🧠 Analogy

Imagine a **restaurant kitchen** 🍳

- You have 5 chefs (**threads in pool**).
- Orders (**tasks**) keep coming.
- When a chef finishes one order, they take the next one from the queue.

You **don’t hire a new chef** for every order — you **reuse** the existing ones.  
That’s exactly what a **thread pool** does!

---

## 💡 Real Code Example

Here’s a simple Java example using a thread pool:

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolExample {
    public static void main(String[] args) {
        // Create a thread pool with 3 threads
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Submit 5 tasks
        for (int i = 1; i <= 5; i++) {
            int taskId = i;
            executor.submit(() -> {
                System.out.println("Task " + taskId + " running in " + Thread.currentThread().getName());
                try { Thread.sleep(1000); } catch (InterruptedException e) {}
            });
        }

        // Shutdown pool after all tasks complete
        executor.shutdown();
    }
}
```

### 🧩 Output Example:

```java
Task 1 running in pool-1-thread-1
Task 2 running in pool-1-thread-2
Task 3 running in pool-1-thread-3
Task 4 running in pool-1-thread-1
Task 5 running in pool-1-thread-2
```

Notice:

- Only 3 threads (`thread-1`, `thread-2`, `thread-3`) exist.
    
- They **reuse** to complete all 5 tasks.
    

---

## 🧰 Main Types of Thread Pools (in `Executors`)

| Method                      | Description                                      | Example Use                           |
| --------------------------- | ------------------------------------------------ | ------------------------------------- |
| `newFixedThreadPool(n)`     | Fixed number of threads                          | Parallel processing (e.g., 5 workers) |
| `newCachedThreadPool()`     | Creates new threads as needed, reuses idle ones  | Many short tasks                      |
| `newSingleThreadExecutor()` | Only one thread                                  | Sequential background task            |
| `newScheduledThreadPool(n)` | Fixed threads + delayed/repeated task scheduling | Timers, [[cron-like tasks]]           |
![[Pasted image 20251113134735.png|300]]
---

## 🔧 Real-Life Use Cases

1. **Web servers** – Handle many client requests efficiently.  
    (Each request handled by a thread from pool)
    
2. **Database connection handlers** – Control concurrent query execution.
    
3. **Image processing / parallel computation** – Split tasks across multiple cores.
    
4. **Background job schedulers** – Cleanups, backups, reports, etc.
    
5. **Async systems** – Thread pools power things like `CompletableFuture`, Spring Boot async calls, etc.
    

---

## ⚠️ Without Thread Pool — The Problem

```java
for (int i = 0; i < 1000; i++) {     
  new Thread(() -> {         
    System.out.println("Task running...");     
  }).start();
}
```

💣 Creates **1000 separate threads**,  
which can easily overload your CPU and memory.

---

## ✅ With Thread Pool — The Solution

```java
ExecutorService pool = Executors.newFixedThreadPool(10); 
for (int i = 0; i < 1000; i++) {     
  pool.submit(() -> {         
    System.out.println("Task running...");     
    }); 
} 
pool.shutdown();
```

- `pool.shutdown();` is a method in Java’s ExecutorService framework — used to gracefully shut down a thread pool after its tasks are finished.
- You are telling the thread pool:
> 	"No new tasks will be accepted. Finish all currently running and queued tasks, then stop."


Only **10 threads** are reused for all 1000 tasks — much more efficient.



# Implementation

`findSum.java`
```java
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

class findSum{
  public static void main(String[] args) throws InterruptedException{
    ScheduledExecutorService worker1 = Executors.newScheduledThreadPool(10);
    int delay = 0;
    for (int task = 11; task < 200; task++) {
      calSumUpto job = new calSumUpto(task);
      worker1.schedule(job, delay, TimeUnit.SECONDS);
      if(task % 10 == 0) delay += 2;
    }
    worker1.shutdown();
  }
}
```
Scheduled thread pool mimicking fixed thread pool.
`calSumUpto.java`
```java
class calSumUpto implements Runnable{
  int limit;
  calSumUpto(int limit) {
    this.limit = limit;
  }

  @Override
  public void run() {
    int res = 0;
    for (int i = 1; i <= limit; i++) {
      res += i;
    }
    System.out.println(res);
  }
}
```