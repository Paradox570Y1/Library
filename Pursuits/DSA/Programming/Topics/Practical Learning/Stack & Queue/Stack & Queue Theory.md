Here’s a comparison of basic methods for **stack** and **queue** in **Java** and **C++**, including common operations like push, pop, peek, and checking emptiness:

---

### **Stack**

|**Operation**|**Java (using `Stack`)**|**C++ (using `std::stack`)**|
|---|---|---|
|**Create a Stack**|`Stack<Integer> stack = new Stack<>();`|`std::stack<int> stack;`|
|**Push an element**|`stack.push(10);`|`stack.push(10);`|
|**Pop an element**|`stack.pop();`|`stack.pop();`|
|**Peek/Top element**|`stack.peek();`|`stack.top();`|
|**Check empty**|`stack.isEmpty();`|`stack.empty();`|
|**Size of Stack**|`stack.size();`|`stack.size();`|

---

### **Queue**

| **Operation**          | **Java (using `Queue` interface with `LinkedList`)** | **C++ (using `std::queue`)** |
| ---------------------- | ---------------------------------------------------- | ---------------------------- |
| **Create a Queue**     | `Queue<Integer> queue = new LinkedList<>();`         | `std::queue<int> queue;`     |
| **Add/Enqueue**        | `queue.add(10);` (or `queue.offer(10);`)             | `queue.push(10);`            |
| **Remove/Dequeue**     | `queue.remove();` (or `queue.poll();`)               | `queue.pop();`               |
| **Peek/Front element** | `queue.peek();`                                      | `queue.front();`             |
| **Check empty**        | `queue.isEmpty();`                                   | `queue.empty();`             |
| **Size of Queue**      | `queue.size();`                                      | `queue.size();`              |
### **Differences to Note**

1. **Java**:
    
    - Uses `Stack` (a subclass of `Vector`) for stack implementation.
    - Uses `Queue` interface for queue operations (commonly implemented with `LinkedList` or `PriorityQueue`).
2. **C++**:
    
    - `std::stack` and `std::queue` are part of the **Standard Template Library (STL)**.
    - Provides `std::deque` as a double-ended queue, which can serve both as a stack and a queue.

![[Pasted image 20250211100344.png|400]]
