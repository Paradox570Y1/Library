## 1. **What is BitSet?**

- `BitSet` is a Java class that represents a **set of bits** (like an array of booleans but much more memory-efficient).
    
- Internally, it stores bits as **long[]**, where each `long` holds 64 bits.
    
- You can think of it like a **dynamic bitmask**.
    

---

## 2. **Why use BitSet?**

✅ Efficient in memory compared to `boolean[]`.  
✅ Fast bit operations (`and`, `or`, `xor`).  
✅ Useful for problems like:

- Set membership checks
    
- Graph reachability
    
- Compression
    
- Optimizing `HashSet<Integer>` when values are bounded
    

---

## 3. **Basic Syntax**

```java
import java.util.BitSet;

public class Example {
    public static void main(String[] args) {
        BitSet bs = new BitSet(); // empty BitSet
        bs.set(1);  // set bit at index 1
        bs.set(3);  // set bit at index 3
        bs.set(5);

        System.out.println(bs); // {1, 3, 5}

        System.out.println(bs.get(3)); // true (bit is set)
        System.out.println(bs.get(4)); // false
    }
}

```

---

## 4. **Common Operations**

| Method              | Meaning                         | Example               |
| ------------------- | ------------------------------- | --------------------- |
| `set(i)`            | Set bit `i` to 1                | `bs.set(2)`           |
| `clear(i)`          | Clear bit `i` (set to 0)        | `bs.clear(2)`         |
| `flip(i)`           | Toggle bit `i`                  | `bs.flip(3)`          |
| `get(i)`            | Returns boolean value of bit    | `bs.get(1)`           |
| `cardinality()`     | Number of set bits              | `bs.cardinality()`    |
| `and(other)`        | Bitwise AND                     | `bs.and(bs2)`         |
| `or(other)`         | Bitwise OR                      | `bs.or(bs2)`          |
| `xor(other)`        | Bitwise XOR                     | `bs.xor(bs2)`         |
| `intersects(other)` | True if they share a common bit | `bs1.intersects(bs2)` |
|                     |                                 |                       |
## Queries

|Method|Description|Example|
|---|---|---|
|`isEmpty()`|`true` if no bit is set.|`bs.isEmpty();`|
|`cardinality()`|Number of set bits.|`bs.cardinality();`|
|`length()`|Index of highest set bit + 1.|If `{3,7}` → `8`|
|`size()`|Capacity (multiple of 64).|`bs.size(); // 64,128,…`|
|`equals(Object obj)`|Compares 2 BitSets.|`bs1.equals(bs2);`|
## Cloning

| Method    | Description               | Example                              |
| --------- | ------------------------- | ------------------------------------ |
| `clone()` | Creates a copy of BitSet. | `BitSet copy = (BitSet) bs.clone();` |

---

## 5. **Example – Using BitSet for Languages**

Let’s map languages to bits.  
Say a user knows `{1, 3, 5}` → we can store this in a BitSet.

```java
int n = 5; // total languages
BitSet[] lang = new BitSet[3]; // 3 users

// user 0 knows 1, 3, 5
lang[0] = new BitSet(n);
lang[0].set(1);
lang[0].set(3);
lang[0].set(5);

// user 1 knows 2, 3
lang[1] = new BitSet(n);
lang[1].set(2);
lang[1].set(3);

// check if they share a language:
BitSet tmp = (BitSet) lang[0].clone();
tmp.and(lang[1]);
System.out.println(tmp.cardinality() > 0); // true (they share language 3)

```

---

## 6. **Advantages in your problem**

In your `minimumTeachings` solution:

- Instead of `HashSet<Integer>` for each user’s languages,  
    you can use `BitSet`.
    
- Checking **common languages** becomes **O(n/64)** (fast bitwise ops), not a loop.