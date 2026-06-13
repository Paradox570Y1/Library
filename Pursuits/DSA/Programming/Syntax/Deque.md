```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        // Creating a Deque (ArrayDeque implementation)
        Deque<Integer> deque = new ArrayDeque<>();

        // Adding elements
        deque.addFirst(10);  // Adds 10 at the front
        deque.addLast(20);   // Adds 20 at the back
        deque.offerFirst(5); // Adds 5 at the front
        deque.offerLast(25); // Adds 25 at the back

        // Removing elements
        deque.removeFirst(); // Removes first element (5)
        deque.removeLast();  // Removes last element (25)
        deque.pollFirst();   // Removes and returns first element (10)
        deque.pollLast();    // Removes and returns last element (20)

        // Accessing elements
        deque.add(30);
        deque.add(40);
        System.out.println(deque.getFirst()); // Get first element
        System.out.println(deque.getLast());  // Get last element

        // Iterating over Deque
        for (int num : deque) {
            System.out.println(num);
        }
    }
}

```