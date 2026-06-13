In JAVA

![[Pasted image 20250423204302.png]]

- We can even put comparator inside priority queue
```java
import java.util.*;

public class Main
{
    public static class Students{
        int marks;
        String name;
        
        Students(int marks, String name){
            this.marks = marks;
            this.name = name;
        }
        
        public String toString(){
            return name+"-"+marks;
        }
    }
    
    static class StCompare implements Comparator<Students>{
        public int compare(Students s1, Students s2){
            return s1.marks - s2.marks;
        }
    }
	public static void main(String[] args) {
// 		PriorityQueue<Students> pq = new PriorityQueue<>((a,b)->a.marks-b.marks);
        // StCompare obj = new StCompare();
        // PriorityQueue<Students> pq = new PriorityQueue<>(obj);
        PriorityQueue<Students> pq = new PriorityQueue<>(new Comparator<Students>(){public int compare(Students s1, Students s2){return s1.marks - s2.marks;}});
		
		pq.offer(new Students(10,"arjit"));
		pq.offer(new Students(30,"arun"));
		pq.offer(new Students(40,"aryan"));
		pq.offer(new Students(5,"bharat"));
		
		System.out.println(pq);
		System.out.println(pq.peek());
	}
}
```




In JS
```js
const array = [
    [3, 2, 1],
    [9, 8, 7],
    [5, 6, 4]
];

// Sorting rows lexicographically
array.sort((a, b) => {
    for (let i = 0; i < Math.min(a.length, b.length); i++) {
        if (a[i] !== b[i]) {
            return a[i] - b[i]; // Compare elements
        }
    }
    return a.length - b.length; // Shorter row comes first if all elements are equal
});

console.log(array);

```


In JAVA
```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[][] array = {
            {3, 2, 1},
            {9, 8, 7},
            {5, 6, 4}
        };

        // Sorting rows lexicographically
        Arrays.sort(array, (a, b) -> {
            // Compare arrays lexicographically
            for (int i = 0; i < Math.min(a.length, b.length); i++) {
                if (a[i] != b[i]) {
                    return Integer.compare(a[i], b[i]);
                }
            }
            return Integer.compare(a.length, b.length); // If all elements are equal, shorter row comes first
        });

        // Print sorted 2D array
        for (int[] row : array) {
            System.out.println(Arrays.toString(row));
        }
    }
}

```


In CPP

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<std::vector<int>> array = {
        {3, 2, 1},
        {9, 8, 7},
        {5, 6, 4}
    };

    // Sort rows lexicographically
    std::sort(array.begin(), array.end());

    // Print sorted 2D array
    for (const auto& row : array) {
        for (int elem : row) {
            std::cout << elem << " ";
        }
        std::cout << "\n";
    }

    return 0;
}

```