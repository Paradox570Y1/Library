## **🔹 Operations of `LinkedHashSet`**

| Operation                    | Method                                      | Description                                                    |
| ---------------------------- | ------------------------------------------- | -------------------------------------------------------------- |
| **Add Element**              | `add(E e)`                                  | Adds `e` to the set (if not present). Returns `true` if added. |
| **Check Element**            | `contains(E e)`                             | Returns `true` if `e` is present in the set.                   |
| **Remove Element**           | `remove(E e)`                               | Removes `e` from the set. Returns `true` if removed.           |
| **Remove First (LRU logic)** | `iterator().next()` + `iterator().remove()` | Removes the oldest element (first inserted).                   |
| **Get Size**                 | `size()`                                    | Returns the number of elements in the set.                     |
| **Clear Set**                | `clear()`                                   | Removes all elements.                                          |
| **Check if Empty**           | `isEmpty()`                                 | Returns `true` if the set is empty.                            |
| **Get All Elements**         | `iterator()` or `forEach()`                 | Iterates over the set while maintaining insertion order.       |


```java
Iterator<Integer> it = cache.iterator();
if (it.hasNext()) {
    int firstElement = it.next(); // move the iterator to next element
    it.remove(); // Remove it
}
System.out.println(cache); // Output: Remaining elements after removal
	
```
[[How above code works]]
### **LinkedHashSet Implementation in Java**

`LinkedHashSet` is a combination of `HashSet` and `LinkedList`, providing **unique elements** like a `HashSet` but maintaining **insertion order** like a `LinkedList`. It is part of the **Java Collections Framework** and implements the `Set` interface.

---

### **1. Internal Implementation**

- **Uses a HashTable + Doubly Linked List**
    
    - It extends `HashSet`, meaning it relies on a **hash table** for fast lookup.
        
    - Additionally, it maintains a **doubly linked list** to **preserve the insertion order**.
        

---

### **2. Performance Comparison**

|Operation|`LinkedHashSet`|
|---|---|
|**Insertion (`add(E e)`)**|`O(1)`|
|**Deletion (`remove(E e)`)**|`O(1)`|
|**Search (`contains(E e)`)**|`O(1)`|
|**Iteration Order**|**Preserves insertion order**|
|**Duplicates Allowed?**|❌ No|
|**Null Elements Allowed?**|✅ Yes (Only one)|

---

### **3. Key Differences from Other Sets**

|Feature|`HashSet`|`LinkedHashSet`|`TreeSet`|
|---|---|---|---|
|**Order Preserved?**|❌ No|✅ Yes (Insertion Order)|✅ Yes (Sorted Order)|
|**Performance**|Fastest|Slightly Slower (due to LinkedList overhead)|Slowest (`O(log n)`)|
|**Allows Null?**|✅ Yes (1 Null)|✅ Yes (1 Null)|❌ No|
|**Duplicates?**|❌ No|❌ No|❌ No|

---

### **4. Example Usage**

```java
import java.util.*;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        LinkedHashSet<Integer> lhs = new LinkedHashSet<>();

        lhs.add(10);
        lhs.add(20);
        lhs.add(30);
        lhs.add(20);  // Duplicate, won't be added

        System.out.println(lhs);  // Output: [10, 20, 30] (insertion order maintained)

        lhs.remove(10);
        System.out.println(lhs.contains(10)); // Output: false
    }
}

```



---

### **5. When to Use `LinkedHashSet`?**

✅ **Use `LinkedHashSet` when you need:**

- Unique elements **with insertion order preserved**.
    
- **Fast `O(1)` insert, delete, and lookup**, but also care about maintaining order.
    
- A balance between **HashSet's speed** and **LinkedList's ordering**.
    

❌ **Don't use `LinkedHashSet` when:**

- You need **sorting** → Use `TreeSet`.
    
- Memory is a concern (it consumes more than `HashSet` due to linked list overhead).


