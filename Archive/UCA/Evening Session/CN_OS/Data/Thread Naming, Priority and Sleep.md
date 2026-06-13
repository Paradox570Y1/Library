## **1. Thread Naming**

**Theory:**

- Every thread in Java has a name, which helps in debugging and logging.
- You can set a thread’s name when creating it or later via `setName()`.

**Default behavior:**

- If you don’t name a thread, Java assigns it a default name like `"Thread-0"`, `"Thread-1"`, etc., in order of creation.

**Must-know:**

- Use descriptive names (e.g., `"DatabaseWorker"`, `"LoggerThread"`) to make logs more understandable.
- You can get a thread’s name via `Thread.currentThread().getName()`.

## **2. Thread Priorities**

**Theory:**

- Java thread priorities are **hints** to the JVM scheduler — not strict rules.
- The scheduler _may_ choose to run higher-priority threads first, but behavior depends on the OS & JVM implementation.

**Default behavior:**

- **Default priority:** `Thread.NORM_PRIORITY` (value 5)
- Priority range:
    - `Thread.MIN_PRIORITY` = 1
    - `Thread.MAX_PRIORITY` = 10

**Must-know:**

- High priority **does not guarantee** faster execution — CPU scheduling and OS policy are the deciding factors.
- Overusing priorities can make code unpredictable and less portable.
- Priorities are most relevant when multiple threads are competing for CPU.

## **3. Thread Sleep**
[[Detailed explanation on sleep]]
**Theory:**

- `Thread.sleep(milliseconds)` pauses the **current** thread for at least the given time.
- The sleeping thread releases the CPU but **does not release locks** it holds.

**Default behavior:**

- No default sleep; you must explicitly call `Thread.sleep()` when needed.
- Sleep time is **minimum wait** — OS can delay wake-up longer depending on CPU availability.

**Must-know:**

- Always handle `InterruptedException` when using `sleep()`.
- Good for simulating delays or throttling task execution.
- Sleep is **static**: it always affects the thread that calls it, not the one it’s called _on_.

```java
try {
    Thread.sleep(1000); // 1 second
} catch (InterruptedException e) {
    e.printStackTrace();
}
```


```java
public class Module9_NamingPrioritiesSleep {
    public static void main(String[] args) {
        Runnable task = () -> {
            String name = Thread.currentThread().getName();
            int priority = Thread.currentThread().getPriority();
            System.out.println("Thread started: " + name + " (Priority: " + priority + ")");
            try {
                Thread.sleep(1000); // sleep for 1 second
                System.out.println(name + " waking up after sleep");
            } catch (InterruptedException e) {
                System.out.println(name + " interrupted");
            }
        };

        Thread t1 = new Thread(task, "Worker-1");
        Thread t2 = new Thread(task, "Worker-2");
        Thread t3 = new Thread(task, "Worker-3");

        t1.setPriority(Thread.MIN_PRIORITY); // 1
        t2.setPriority(Thread.NORM_PRIORITY); // 5
        t3.setPriority(Thread.MAX_PRIORITY); // 10

        t1.start();
        t2.start();
        t3.start();
    }
}

```