### ✅ 2. **Using `BitSet` class in Java**

If you meant a data structure to **manage bits**, Java has a built-in class for that: `java.util.BitSet`.

#### 🔧 Example:

```java
int number = 5;      // binary: 0101
int position = 1;    // we want to set the bit at position 1 (counting from 0)
number = number | (1 << position);
System.out.println(number); // Output: 7 (binary: 0111)

```

#### ✅ Features of `BitSet`:

- Grows automatically (not fixed size like arrays).
    
- Memory efficient for storing binary flags.
    
- Methods:
    
    - `set(index)`: sets bit to 1
        
    - `clear(index)`: clears bit (to 0)
        
    - `get(index)`: returns boolean
        
    - `flip(index)`: toggles bit
        

---

### 🔄 Summary:

| Concept                           | Use Case                                                     |
| --------------------------------- | ------------------------------------------------------------ |
| Bit manipulation (e.g. set a bit) | Used with integers for fast, low-level operations            |
| `BitSet` class                    | Use when you need to store lots of boolean flags efficiently |
### ✅ `.or(BitSet set)` in Java

The `.or()` method performs a **bitwise OR** between **two `BitSet` objects**.

![[Pasted image 20250724204955.png|300]]


![[Pasted image 20250724205442.png]]