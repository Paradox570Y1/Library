Using `setTimeout(func, 0)` in JavaScript may look like it executes `func` immediately, but **that's not what actually happens**. Here's what's different and important about using `0`:

---

### 🔁 What `setTimeout(func, 0)` Really Does

- It **schedules `func` to run after the current call stack is cleared**, not immediately.
    
- The **delay is never truly 0 ms** — it's the **minimum delay possible**, usually 4 ms or more depending on the browser.