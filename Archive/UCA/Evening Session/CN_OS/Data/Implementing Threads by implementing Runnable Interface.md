Another way to achieve multithreading in java is via the Runnable interface. Here as we have seen in the above example in way 1 where Thread class is extended. Here Runnable interface being a functional interface has its own run() method. Here classes are implemented to the Runnable interface. Later on, in the main() method, Runnable reference is created for the classes that are implemented in order to make bondage with Thread class to run our own corresponding run() methods.

Further, while creating an object of Thread class we will pass these references in Thread class as its constructor allows only one runnable object, which is passed as a parameter while creating Thread class object in a main() method. Now lastly just like what we did in Thread class, start() method is invoked over the runnable object who are now already linked with Thread class objects, so the execution begins for our run() methods in case of Runnable interface

## **Runnable Interface Approach** 🧵

### 1️⃣ What It Is

- **Runnable** is a functional interface in Java with **one method**:
   `public void run();`

- Instead of **extending Thread**, you **implement Runnable**.
- Then you give that Runnable to a `Thread` object to actually run it.

---

### 2️⃣ Why Use It Instead of Extending Thread?

- Java **does not allow multiple inheritance**.
    - If you extend Thread, you can’t extend another class.
    - If you implement Runnable, you can still extend any other class.
- Cleaner separation of **task** (Runnable) and **execution** (Thread).
	- Now can create multiple execution of same task by just passing its object to thread.
### **1. Runnable = The Script (The Task) 🎬**

- Contains **what should be done** (`run()` method).
- It **does not** know how or when it will be executed.

Example:
```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Reading a script...");
    }
}
```

---

### **2. Thread = The Actor (The Executor) 🎭**

- Knows **how to act**, but needs a **script** to follow.
- The `Thread` object takes a `Runnable` (script) and performs it when you call `start()`.

Example:
```java
MyTask script = new MyTask();
Thread actor = new Thread(script); 
actor.start(); // The actor performs the script
```

---

### **3. Why This is Cleaner**

- **Separation of Concerns**:
    - The **task logic** is in one class (`Runnable`).
    - The **execution mechanism** (thread scheduling, start, stop) is handled by `Thread`.
- You can reuse the **same task** in multiple threads without rewriting execution logic.
- You can still extend another class in your task class, since you’re not locked into extending `Thread`.

```java
// Java Program to illustrate Runnable Interface in threads
// as multiple inheritance is not allowed

// Importing basic packages
import java.io.*;
import java.util.*;

// Class 1
// Helper class implementing Runnable interface
class MyThread1 implements Runnable {

    // run() method inside this class
    public void run()
    {
        // Iterating to get more execution of threads
        for (int i = 0; i < 5; i++) {

            // Print statement whenever run() method
            // of this class is called
            System.out.println("Thread1");

            // Getting sleep method in try block to
            // check for any exceptions
            try {
                // Making the thread pause for a certain
                // time using sleep() method
                Thread.sleep(1000);
            }

            // Catch block to handle the exceptions
            catch (Exception e) {
            }
        }
    }
}

// Class 2
// Helper class implementing Runnable interface
class MyThread2 implements Runnable {

    // run() method inside this class
    public void run()
    {
        for (int i = 0; i < 5; i++) {

            // Print statement whenever run() method
            // of this class is called
            System.out.println("Thread2");

            // Getting sleep method in try block to
            // check for any exceptions
            try {

                // Making the thread pause for a certain
                // time
                // using sleep() method
                Thread.sleep(1000);
            }

            // Catch block to handle the exceptions
            catch (Exception e) {
            }
        }
    }
}

// Class 3
// Main class
public class GFG {

    // Main driver method
    public static void main(String[] args)
    {

        // Creating reference of Runnable to
        // our classes above in main() method
        Runnable obj1 = new MyThread1();
        Runnable obj2 = new MyThread2();

        // Creating reference of thread class
        // by passing object of Runnable in constructor of
        // Thread class
        Thread t1 = new Thread(obj1);
        Thread t2 = new Thread(obj2);

        // Starting the execution of our own run() method
        // in the classes above
        t1.start();
        t2.start();
    }
}
```