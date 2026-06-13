# Sorting with values
In Ascending
```java
import java.util.*;

public class SortHashMapByValueWithoutLinkedList {
    public static void main(String[] args) {
        // Create a HashMap
        HashMap<String, Integer> map = new HashMap<>();
        map.put("Banana", 3);
        map.put("Apple", 5);
        map.put("Orange", 2);
        map.put("Grapes", 4);

        // Convert the map's entries to a list
        List<Map.Entry<String, Integer>> entries = new ArrayList<>(map.entrySet());

        // Sort the list by values
        entries.sort(Map.Entry.comparingByValue());

        // Print the sorted result directly
        System.out.println("Sorted by Values:");
        for (Map.Entry<String, Integer> entry : entries) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}

```

In descending 
```java
import java.util.*;

public class SortHashMapByValueDescending {
    public static void main(String[] args) {
        // Create a HashMap
        HashMap<String, Integer> map = new HashMap<>();
        map.put("Banana", 3);
        map.put("Apple", 5);
        map.put("Orange", 2);
        map.put("Grapes", 4);

        // Convert the map's entries to a list
        List<Map.Entry<String, Integer>> entries = new ArrayList<>(map.entrySet());

        // Sort the list by values in descending order
        entries.sort((entry1, entry2) -> entry2.getValue().compareTo(entry1.getValue()));

        // Print the sorted result directly
        System.out.println("Sorted by Values (Descending):");
        for (Map.Entry<String, Integer> entry : entries) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```