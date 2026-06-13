In Java, the `poll()` method is used with **priority queues** (or any queue that implements the `Queue` interface) to retrieve and remove the **head** of the queue.

### Key Points about `pq.poll()`:

1. **Retrieves and Removes the Head**: It removes the first element (head) of the queue, which in the case of a **PriorityQueue** is the smallest or highest-priority element (depending on the comparator used).
    
2. **Returns Null if Empty**: If the queue is empty, `poll()` returns `null`. This is different from the `remove()` method, which throws a `NoSuchElementException` if the queue is empty.
    
3. **Behavior with PriorityQueue**:
    
    - A **PriorityQueue** organizes elements based on their **natural ordering** (if the elements implement `Comparable`) or based on a provided **Comparator**.
    - The "head" of the queue is the element with the **highest priority** (smallest element by default).


Use `poll()` when you want to **safely remove** and retrieve the head of the queue without worrying about exceptions if the queue is empty. If you just want to peek at the head without removing it, you can use `peek()` instead.