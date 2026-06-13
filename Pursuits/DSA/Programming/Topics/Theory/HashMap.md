A HashMap in Java is a part of the `java.util` package and is used to store key-value pairs. It works on the principle of hashing, which allows for fast retrieval, insertion, and deletion of values based on their keys. Here's a basic guide to understanding and using a HashMap in Java:

### 1. Importing the HashMap Class

To use HashMap, you need to import it from the `java.util` package.

```java
import java.util.HashMap;
```

### 2. Creating a HashMap

You can create a HashMap by specifying the types for the keys and values.


```java
HashMap<Integer, String> map = new HashMap<>();
```

### 3. Adding Elements

You can add key-value pairs to the HashMap using the `put` method.

```java
map.put(1, "One"); map.put(2, "Two"); map.put(3, "Three");
```

### 4. Accessing Elements

You can retrieve a value from the HashMap using the `get` method by providing the key.


```java
String value = map.get(1); // Returns "One"
```

### 5. Removing Elements

You can remove a key-value pair from the HashMap using the `remove` method by providing the key.


```java
map.remove(2); // Removes the key-value pair where the key is 2
```

### 6. Iterating Over a HashMap

You can iterate over the keys, values, or entries (key-value pairs) of the HashMap.
#### Iterating over keys:

```java
for (Integer key : map.keySet()) {     
	System.out.println(key); 
}
```

#### Iterating over values:

```java
for (String value : map.values()) {     
	System.out.println(value);
}
```

#### Iterating over entries:
```java
for (HashMap.Entry<Integer, String> entry : map.entrySet()) {        System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue()); }
```

#### How to get key and value without iterating
```java
HashMap<Integer,Integer> store = new HashMap<>();
//store something
List<HashMap.Entry<Integer,Integer>> ent = new ArrayList<>(store.entrySet());
HashMap.Entry<Integer,Integer> e = ent.get(0);
System.out.println(e.getKey()+ " " + e.getValue());
```
### 7. Common Methods

- **size()**: Returns the number of key-value pairs in the map.
- **isEmpty()**: Checks if the map is empty.
- **containsKey(Object key)**: Checks if the map contains the specified key.
- **containsValue(Object value)**: Checks if the map contains the specified value.

### Example Program

Here is a complete example program that demonstrates the basic operations of a HashMap:

```java
import java.util.HashMap;
public class HashMapExample {
    public static void main(String[] args) {
        // Creating a HashMap
        HashMap<Integer, String> map = new HashMap<>();

        // Adding elements
        map.put(1, "One");
        map.put(2, "Two");
        map.put(3, "Three");

        // Accessing elements
        System.out.println("Value for key 1: " + map.get(1));

        // Removing an element
        map.remove(2);

        // Iterating over keys
        System.out.println("Keys:");
        for (Integer key : map.keySet()) {
            System.out.println(key);
        }

        // Iterating over values
        System.out.println("Values:");
        for (String value : map.values()) {
            System.out.println(value);
        }

        // Iterating over entries
        System.out.println("Entries:");
        for (HashMap.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }
    }
}
```
