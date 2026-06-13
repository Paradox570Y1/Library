Think of a **Semaphore** like a parking lot gate:

- The parking lot has **limited spots** (permits).
- Before entering, a car (thread) must **acquire()** a spot.
- If no spots are free, the car waits until another car leaves.
- When a car leaves, it **release()** the spot for someone else.

---
## **Core Theory**

In Java, `Semaphore` is in **`java.util.concurrent`** package and is used to control access to a **shared resource** by a **fixed number of threads**.

---
### **Key Points**

1. **Permits**
    - The number of available "entries" or "tickets".
    - Set when creating the semaphore:
```java
Semaphore semaphore = new Semaphore(3); // 3 permits
```
        
2. **acquire()**
    - Decreases the available permits by 1.
    - If no permit is available, the thread **blocks** until one is released.
    - Can throw `InterruptedException`.
3. **release()**
    - Increases available permits by 1.
    - Wakes up one waiting thread (if any).
4. **Types**
    - **Binary Semaphore** → like a **mutex**, only 1 permit.
    -  **Counting Semaphore** → more than 1 permit, multiple threads can work at the same time.
```java
Semaphore semaphore = new Semaphore(1); //binary semamphore
```
        
        
5. **Fairness**
    - Semaphores can be **fair** or **non-fair**:
        - `new Semaphore(1, true)` → fair, first-come-first-served.
        - Default (false) → no guaranteed order, but faster.

### **Must-know Things**

- Semaphores don’t automatically release permits — you **must** call `release()`.
- Use **try-finally** to ensure release happens even if an exception occurs.
- `Semaphore(1)` can replace `synchronized` or `ReentrantLock` in some cases.
- Useful for **limiting concurrency**, like controlling API requests or database connections.

Example code
```java
import java.util.concurrent.Semaphore;

public class Example {
    static Semaphore semaphore = new Semaphore(2); // 2 permits

    static class Task implements Runnable {
        @Override
        public void run() {
            try {
                semaphore.acquire(); // Get a permit
                System.out.println(Thread.currentThread().getName() + " acquired a permit");
                Thread.sleep(1000); // simulate work
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            } finally {
                semaphore.release(); // Give permit back
                System.out.println(Thread.currentThread().getName() + " released a permit");
            }
        }
    }

    public static void main(String[] args) {
        for (int i = 1; i <= 5; i++) {
            new Thread(new Task(), "Thread-" + i).start();
        }
    }
}

```