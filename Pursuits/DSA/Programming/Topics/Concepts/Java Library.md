- To find max() 
- **Collections.max()**:
    
    - For lists and other collections, use `Collections.max()`.
```java
import java.util.Collections;
import java.util.ArrayList;
import java.util.List;

public class MaxExample {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        list.add(5);
        list.add(3);
        list.add(8);
        list.add(2);
        list.add(1);
        int max = Collections.max(list);
        System.out.println(max);
    }
}
```
 **Arrays.stream()**:
    For arrays, you can use streams.
```java
import java.util.Arrays;

public class MaxExample {
    public static void main(String[] args) {
        int[] array = {5, 3, 8, 2, 1};
        int max = Arrays.stream(array).max().getAsInt();
        System.out.println(max);
    }
}

```


# To accumulate the sum

To add all elements of a collection in Java, you can use the **`Stream` API** introduced in Java 8 or a library function like `Collections.addAll()`. Below are examples:

### 1. **Using Stream API with `reduce` (for custom summation):**

This works for numerical collections like a `List<Integer>`.


```java
import java.util.Arrays; 
import java.util.List;  
public class Main {     
	public static void main(String[] args) {         
		List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);          
		// Summing all elements using Stream API         
		int sum = numbers.stream().mapToInt(Integer::intValue).sum();               System.out.println("Sum of elements: " + sum);     
	} 
}
```

### 2. **Using `Collections.addAll` (to add all elements to a collection):**

This is not for summing but adding elements to a collection from another collection or array.


```java
import java.util.ArrayList; 
import java.util.Collections; 
import java.util.List;  
public class Main {     
	public static void main(String[] args) {         
		List<Integer> list = new ArrayList<>(); 
		Collections.addAll(list, 1, 2, 3, 4, 5);
		System.out.println("Elements added to the list: " + list);     
	} 
}
```

### 3. **Using `IntStream.of` (for summing elements in an array):**

java

Copy code

```java
import java.util.stream.IntStream;  
public class Main {     
	public static void main(String[] args) {         
		int[] numbers = {1, 2, 3, 4, 5};         
		 // Summing array elements         
		int sum = IntStream.of(numbers).sum();            
		System.out.println("Sum of elements: " + sum);    
	} 
}
```

### Choose Based on Your Use Case:

- **For summing numeric elements:** Use the **Stream API** (`sum` or `reduce`).
- **To add elements to a collection:** Use `Collections.addAll()`.