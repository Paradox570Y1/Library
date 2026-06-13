### **TreeMap in Java**

A **TreeMap** in Java is a part of the `java.util` package and implements the `NavigableMap` interface. It is a **Red-Black Tree** based implementation of the `SortedMap` interface, meaning it maintains key-value pairs in **sorted order (ascending by default)**.

### **Key Properties of TreeMap**

1. **Sorted Order** – TreeMap automatically maintains the order of keys in ascending order.
    
2. **Unique Keys** – It does not allow duplicate keys, but values can be duplicate.
    
3. **Logarithmic Time Complexity** – Operations like `put()`, `get()`, `remove()`, and `containsKey()` take **O(log n)** time.
    
4. **Not Synchronized** – TreeMap is **not thread-safe**, but you can make it synchronized using `Collections.synchronizedMap()`.
    
5. **Allows Null Values, but Not Null Keys** – Unlike HashMap, TreeMap does **not allow null keys**, but it can store multiple null values.
    

---

## **Syntax and Usage**

### **1. Importing TreeMap**


`import java.util.TreeMap;`

---

### **2. Creating a TreeMap**

`TreeMap<Integer, String> map = new TreeMap<>();`

---

### **3. Adding Elements**

`map.put(101, "Alice"); map.put(103, "Bob"); map.put(102, "Charlie");`

🔹 The keys will be **sorted automatically** in ascending order:  
📌 Output: `{101=Alice, 102=Charlie, 103=Bob}`

---

### **4. Accessing Values**

`System.out.println(map.get(102));  // Output: Charlie`

---

### **5. Removing Elements**

`map.remove(103);   System.out.println(map);  // Output: {101=Alice, 102=Charlie}`

---

### **6. Iterating Over TreeMap**

#### **(a) Using Entry Set (Key-Value Pair)**

`for (var entry : map.entrySet()) {     System.out.println(entry.getKey() + " -> " + entry.getValue()); }`

#### **(b) Using Key Set (Only Keys)**

`for (Integer key : map.keySet()) {     System.out.println(key); }`

#### **(c) Using Values (Only Values)**


`for (String value : map.values()) {     System.out.println(value); }`

---

### **7. Checking If Key Exists**

`System.out.println(map.containsKey(101));  // Output: true`

---

### **8. Checking If Value Exists**

`System.out.println(map.containsValue("Alice"));  // Output: true`

---

### **9. Getting First and Last Key**

`System.out.println(map.firstKey());  // Smallest key System.out.println(map.lastKey());   // Largest key`

---

### **10. Getting Submaps**

#### **(a) HeadMap (Keys Less Than a Given Key)**

`System.out.println(map.headMap(102));  // Output: {101=Alice}`

#### **(b) TailMap (Keys Greater Than or Equal to Given Key)**


`System.out.println(map.tailMap(102));  // Output: {102=Charlie, 103=Bob}`

#### **(c) SubMap (Keys in a Range)**

`System.out.println(map.subMap(101, 103));  // Output: {101=Alice, 102=Charlie}`

---

### **11. Custom Sorting with Comparator**

If you want to **sort in descending order**, use a **Comparator**:

`TreeMap<Integer, String> descendingMap = new TreeMap<>((a, b) -> b - a); descendingMap.putAll(map); System.out.println(descendingMap);  // Output: {103=Bob, 102=Charlie, 101=Alice}`

---

## **Complete Example**


```java
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        TreeMap<Integer, String> map = new TreeMap<>();
        
        // Adding key-value pairs
        map.put(105, "Zara");
        map.put(102, "Mia");
        map.put(103, "Leo");
        map.put(101, "Alex");

        // Displaying the TreeMap (sorted by keys)
        System.out.println("TreeMap: " + map);

        // Retrieving a value
        System.out.println("Value at key 102: " + map.get(102));

        // Removing an element
        map.remove(103);
        System.out.println("After removing key 103: " + map);

        // Iterating using entrySet
        System.out.println("Iterating through TreeMap:");
        for (var entry : map.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}

```

📌 **Output:**

```java
TreeMap: {101=Alex, 102=Mia, 103=Leo, 105=Zara}
Value at key 102: Mia
After removing key 103: {101=Alex, 102=Mia, 105=Zara}
Iterating through TreeMap:
101 -> Alex
102 -> Mia
105 -> Zara

```

---

### **When to Use TreeMap?**

✅ When you need a **sorted** key-value structure.  
✅ When you need fast lookups, insertions, and deletions (**O(log n)** complexity).  
✅ When you require navigation methods like `firstKey()`, `lastKey()`, `subMap()`, etc.

🚀 **Best Use Case:** Storing **sorted** data like ranking systems, dictionaries, employee records (sorted by ID), etc.