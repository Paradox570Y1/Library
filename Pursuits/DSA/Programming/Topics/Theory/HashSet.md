### What is a `HashSet`?

`HashSet` is a collection that implements the `Set` interface, backed by a hash table (actually a `HashMap` instance). It does not allow duplicate elements and provides constant-time performance for the basic operations (add, remove, contains, and size).

### Comparisons
### 1. HashSet

- No guarantees about the iteration order.
- Constant time performance for basic operations (add, remove, contains, size).

### 2. LinkedHashSet

- Maintains insertion order.
- Slightly slower than `HashSet` due to maintaining the linked list of entries.
- Useful when you need a predictable iteration order.

### 3. TreeSet

- Elements are sorted in natural order or by a specified comparator.
- Performance is guaranteed to be O(logn) for basic operations.
- Useful when you need a sorted set.
### Basic Operations

1. **Creating a `HashSet`**

```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        // Create a HashSet
        HashSet<String> set = new HashSet<>();
    }
}
```
2. **Adding Elements**
```java
set.add("apple");
set.add("banana");
set.add("orange");
```
3. **Removing Elements**
```java
set.remove("banana");
```

4. **Checking if an Element Exists**
```java
boolean containsApple = set.contains("apple"); // returns true if "apple" is in the set
```
5. **Iterating Over Elements**
```java
for (String fruit : set) {
    System.out.println(fruit);
}
```
6. **Getting the Size of the Set**
```java
int size = set.size(); // returns the number of elements in the set
```
7. **Clearing the Set**
```java
set.clear(); // removes all elements from the set
```
8. **Checking if the Set is Empty**
```java
boolean isEmpty = set.isEmpty(); // returns true if the set is empty
```
### Example Code

Here's a complete example that demonstrates these operations:
```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        // Create a HashSet
        HashSet<String> set = new HashSet<>();

        // Add elements to the HashSet
        set.add("apple");
        set.add("banana");
        set.add("orange");

        // Print the elements in the HashSet
        System.out.println("HashSet elements: " + set);

        // Check if an element exists in the HashSet
        if (set.contains("apple")) {
            System.out.println("HashSet contains apple");
        } else {
            System.out.println("HashSet does not contain apple");
        }

        // Remove an element from the HashSet
        set.remove("banana");
        System.out.println("HashSet elements after removing banana: " + set);

        // Get the size of the HashSet
        int size = set.size();
        System.out.println("Size of the HashSet: " + size);

        // Check if the HashSet is empty
        boolean isEmpty = set.isEmpty();
        System.out.println("Is the HashSet empty? " + isEmpty);

        // Clear the HashSet
        set.clear();
        System.out.println("HashSet elements after clearing: " + set);

        // Check if the HashSet is empty after clearing
        isEmpty = set.isEmpty();
        System.out.println("Is the HashSet empty after clearing? " + isEmpty);
    }
}
```
### Key Points

- `HashSet` does not allow duplicate elements.
- The order of elements in a `HashSet` is not guaranteed.
- `HashSet` provides constant-time performance for basic operations due to its underlying hash table implementation.
- Use `HashSet` when you need a collection to store unique elements and order does not matter.