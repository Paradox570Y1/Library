In Java, a **Heap** is usually implemented using the **PriorityQueue** class, which is part of the `java.util` package. The **PriorityQueue** class provides a **Min-Heap** by default, but you can implement a **Max-Heap** using a custom comparator.

![[Pasted image 20250302115616.png]]

![[Pasted image 20250302115648.png]]

> NOTE
> we can even define the capacity of the Priority Queue


```java
import java.util.*;

public class tUf {
    public static class Pair {
        double first;
        int second;

        Pair(double first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    public static double minimiseMaxDistance(int[] arr, int k) {
        int n = arr.length; // size of array.
        int[] howMany = new int[n - 1];
        PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> Double.compare(b.first, a.first));

        // insert the first n-1 elements into pq
        // with respective distance values:
        for (int i = 0; i < n - 1; i++) {
            pq.add(new Pair(arr[i + 1] - arr[i], i));
        }

        // Pick and place k gas stations:
        for (int gasStations = 1; gasStations <= k; gasStations++) {
            // Find the maximum section
            // and insert the gas station:
            Pair tp = pq.poll();
            int secInd = tp.second;

            // insert the current gas station:
            howMany[secInd]++;

            double inidiff = arr[secInd + 1] - arr[secInd];
            double newSecLen = inidiff / (double) (howMany[secInd] + 1);
            pq.add(new Pair(newSecLen, secInd));
        }

        return pq.peek().first;
    }
}
```


- [[poll method]]
```java
PriorityQueue<Pair> pq = new PriorityQueue<>((a,b)-> Double.compare(b.first,a.first));
// here b.first is written before a.first so it will natural sort queue in descending order, but if it was opposite then it will sort in descending order.
```


```cpp
class Solution {
  public:
    double findSmallestMaxDist(vector<int> &stations, int k) {
        // Code here
        int n = stations.size();
    
        priority_queue<pair<double,int>> pq;
        for(int i=0;i<n-1;i++){
            pq.push({stations[i+1]-stations[i],i});
        }
        vector<int> count(n-1,1);
        for(int j=1;j<=k;j++){
            int ind = pq.top().second;
            pq.pop();
            count[ind]++;
            double original = stations[ind+1]-stations[ind];
            double new_diff = original/count[ind];
            pq.push({new_diff,ind});
        }
        return pq.top().first;
    }
};
```

## **Basic Syntax of PriorityQueue in Java**

### **1. Import the PriorityQueue class**


`import java.util.PriorityQueue;`

### **2. Creating a Min-Heap (Default)**

`PriorityQueue<Integer> pq = new PriorityQueue<>();`

- This creates a **Min-Heap** where the smallest element is always at the front.

### **3. Creating a Max-Heap (Using Comparator)**


```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
//or
//below method is much better
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
```

- This creates a **Max-Heap** by reversing the natural order.

---

## **Common Operations**

### **1. Add elements**


`pq.add(10); pq.add(5); pq.add(20); pq.add(15);`

- Inserts elements into the priority queue.

### **2. Get the top element (peek)**

`System.out.println(pq.peek());  // Output: 5 (smallest element in Min-Heap)`

- Retrieves, but does **not remove**, the top element.

### **3. Remove the top element**


`System.out.println(pq.poll());  // Output: 5 (removes smallest element) 
`System.out.println(pq.poll());  // Output: 10`

- Retrieves and **removes** the top element.

### **4. Check size**

`System.out.println(pq.size());`  

- Returns the number of elements in the priority queue.

### **5. Check if the queue is empty**

`System.out.println(pq.isEmpty());`  

- Returns `true` if the priority queue is empty.

### **6. Iterate over elements**

`for (int num : pq) {     System.out.print(num + " "); }`

- **Note:** The elements might **not** be printed in sorted order because they are stored as a heap, not a sorted list.
