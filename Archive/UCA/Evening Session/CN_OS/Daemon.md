[Resources](https://www.geeksforgeeks.org/java/daemon-thread-java/)
## The Purpose of Daemon Threads

The main **purpose** of daemon threads is to run **background support tasks** that:

- run _alongside_ main application logic,
- but **don’t need to block** the program from shutting down.

In other words —

> "Do background work _only while_ the program is alive. If the main program is done, no need to keep running."
## ⚙️ JVM Automatically Has Daemon Threads

Even if you never create one, the JVM already uses daemon threads internally:

- **Garbage Collector thread** — frees memory in the background
- **Finalizer thread** — runs `finalize()` on unused objects
- **JIT compiler thread** — optimizes bytecode during runtime


## 🧩 Real-Life Scenarios You’d Use Daemon Threads

Let’s go through _actual use cases_ 👇

---

### 🕒 1. Background Logging or Monitoring

You want to continuously log app metrics or memory usage while your main app runs —  
but once your app stops, logging doesn’t matter.

```java
Thread logger = new Thread(() -> {
    while (true) {
        System.out.println("Logging stats...");
        try { Thread.sleep(2000); } catch (InterruptedException e) {}
    }
});
logger.setDaemon(true);
logger.start();
```
✅ JVM won’t wait for the logger to finish when the main app ends.  
🧠 Saves you from having to manually stop it.

---

### 📡 2. Background Heartbeat or Cleanup Services

Some apps (like servers) run a background **heartbeat** or **cleanup** task to report system status or delete temp files.

Example:

```java
Thread cleanup = new Thread(() -> {
    while (true) {
        System.out.println("Cleaning temporary cache...");
        try { Thread.sleep(5000); } catch (InterruptedException e) {}
    }
});
cleanup.setDaemon(true);
cleanup.start();
```

➡️ It will keep running as long as main tasks are alive.  
➡️ When the app shuts down, no need to explicitly terminate it — it ends automatically.

---

### 📨 3. Daemon Thread Pool for Background Tasks

In larger systems (like web servers or message brokers),  
some thread pools are created as **daemon pools** — for example:

- asynchronous message listeners,
    
- cache refreshers,
    
- idle resource monitors.

>[Article](https://docs.snowflake.com/en/user-guide/resource-monitors)

If you used user threads for these, your program would _hang_ at the end waiting for them — which is unnecessary.

---

### 🧹 4. Cleanup or Auto-Save in Editors or IDEs

A text editor might use a daemon thread to **auto-save** periodically.  
If you close the editor, it shuts down immediately — no waiting for the next auto-save.

---

### 🧰 5. Background Tasks in GUI Applications

For instance, a Swing or JavaFX app might have:

- background animation,
    
- notification sound, or
    
- network polling thread.
    

If you close the app, daemon threads die with it automatically.

---

## 🚨 Why Not Use Daemon Threads for Everything?

Because daemon threads:

- can be **killed at any time** when JVM exits,
    
- don’t run `finally` blocks or close resources properly,
    
- are **not guaranteed** to finish their work.
    

👉 So use them **only** for _non-critical_, _background_, _supportive_ operations.

---

## 🧠 Analogy to Remember

Imagine your program as a **restaurant**:

- Chefs (user threads) cook meals — restaurant stays open until all meals are cooked.
    
- Cleaning staff (daemon threads) tidy up continuously.  
    If the restaurant closes, they stop immediately — no one waits for them.