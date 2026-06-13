
- It's used for finding shortest path even if there are cycles in graph but there should be no negative cycle.
- It's a single source Shortest Path Algorithm.
There are primarily two ways to ways to implement Dijkstra's Algorithm:
- Using Priority Queue
- Using Set (fastest way)

There is a third way as well although not used much:
- Using Queue (takes more time than above ways).

[Problem Link](https://www.geeksforgeeks.org/problems/implementing-dijkstra-set-1-adjacency-matrix/0)

Given an undirected, weighted graph with **V** vertices numbered from 0 to V-1 and **E** edges, represented by 2d array **edges[][]**, where edges[i]=[u, v, w] represents the **edge** between the nodes u and v having w **edge weight**.  
You have to find the **shortest distance** of all the vertices from the source vertex **src**, and return an array of integers where the **ith** element denotes the shortest distance between **ith** node and source vertex **src**.

**Note:** The Graph is connected and doesn't contain any negative weight edge.

**Examples:**

**Input:** V = 3, edges\[]\[] = `[[0, 1, 1], [1, 2, 3], [0, 2, 6]]`, src = 2
**Output:** [4, 3, 0]
**Explanation**:
![|300](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/892538/Web/Other/blobid0_1744201836.jpg)
Shortest Paths:
For 2 to 0 minimum distance will be 4. By following path 2 -> 1 -> 0
For 2 to 1 minimum distance will be 3. By following path 2 -> 1
For 2 to 2 minimum distance will be 0. By following path 2 -> 2  

**Input:** V = 5, edges\[]\[] = `[[0, 1, 4], [0, 2, 8], [1, 4, 6], [2, 3, 2], [3, 4, 10]]`, src = 0
**Output:** [0, 4, 8, 10, 10]
**Explanation**:   
![|300](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/892538/Web/Other/blobid1_1744202046.jpg) Shortest Paths:   
For 0 to 1 minimum distance will be 4. By following path 0 -> 1
For 0 to 2 minimum distance will be 8. By following path 0 -> 2
For 0 to 3 minimum distance will be 10. By following path 0 -> 2 -> 3 
For 0 to 4 minimum distance will be 10. By following path 0 -> 1 -> 4

**Constraints:**  
1 ≤ V ≤ 105

1 ≤ E = edges.size() ≤ 105  
0 ≤ edges[i][j] ≤ 104

0 ≤ src < V


>**Note:** The Graph is connected and doesn't contain any negative weight edge.
# Using Priority Queue

**Time:** `O((V + E) log V)`
![[Pasted image 20250907123356.png|400]]

**Space:** `O(V + E)`
```java
class Solution {
    public int[] dijkstra(int V, int[][] edges, int src) {
        // code here
        List<List<int[]>> adjList = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            adjList.get(u).add(new int[]{v, w});
            adjList.get(v).add(new int[]{u, w});
        }
        
        int dist[] = new int[V];
        for (int i = 0; i < V; i++) {
            dist[i] = (int) 1e9;
        }
        PriorityQueue<int[]> minHeap = new PriorityQueue<>(new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                if (a[0] != b[0]) return a[0] - b[0];
                return a[1] - b[1];
            }
        });
        
        minHeap.offer(new int[]{0, src});
        dist[src] = 0;
        
        while (!minHeap.isEmpty()) {
            int[] node = minHeap.poll();
            int u = node[1];
            int du = node[0];
            if (du > dist[u]) continue; //Optional but improve TC
            // skip outdated entries ✅ which striver did by set
            for (int[] next : adjList.get(u)) {
                int v = next[0];
                int dv = next[1];
                if (du + dv < dist[v]) {
                    dist[v] = du + dv;
                    minHeap.offer(new int[]{dist[v], v});
                }
            }
        }
        
        return dist;
    }
}
```


###### Dijkstra Algorithm doesn't work for negative weights 
- It causes infinite loop.
![[Pasted image 20250907123114.png|300]]


![[Pasted image 20250907123104.png]]






# Using Set

## Why Set
![[Pasted image 20250907124022.png|350]]
- In above case when we visit node 5 again and calculates it's new distance to be 8 but earlier it wasn't infinity but 10. So we get to know that this node is already in our set, since Iteration with 10 value is not required as new value 8 exists , so we can remove that value from set and save little time in iteration.
- But removing an object from set takes O(log V) time, which  means it will be better only if O(log V) is better than visiting children of the removed node which happens in Priority Queue, and this can be possible as if there can be very few or no child of that node.

```java
import java.util.*;

class Solution {
    public int[] dijkstra(int V, int[][] edges, int src) {
        // Build adjacency list
        List<List<int[]>> adjList = new ArrayList<>();
        for (int i = 0; i < V; i++) adjList.add(new ArrayList<>());
        
        for (int[] edge : edges) {
            int u = edge[0], v = edge[1], w = edge[2];
            adjList.get(u).add(new int[]{v, w});
            adjList.get(v).add(new int[]{u, w});
        }

        int[] dist = new int[V];
        Arrays.fill(dist, (int)1e9);
        dist[src] = 0;

        TreeSet<int[]> st = new TreeSet<>((a, b) -> {
            if (a[0] != b[0]) return Integer.compare(a[0], b[0]);
            return Integer.compare(a[1], b[1]);
        });

        st.add(new int[]{0, src});

        while (!st.isEmpty()) {
            int[] node = st.pollFirst();
            int du = node[0], u = node[1];

            for (int[] next : adjList.get(u)) {
                int v = next[0], w = next[1];
                if (du + w < dist[v]) {
                    if (dist[v] != (int)1e9) {
                        st.remove(new int[]{dist[v], v});
                    }
                    dist[v] = du + w;
                    st.add(new int[]{dist[v], v});
                }
            }
        }
        return dist;
    }
}
```

OR
Using Class
```java
class Solution{
    class Pair implements Comparable<Pair>{
        int node;
        int dist;
        Pair(int dist, int node) {
            this.node = node;
            this.dist = dist;
        }
        
        @Override
        public int compareTo(Pair other) {
            if (this.dist != other.dist) return Integer.compare(this.dist, other.dist);
            return Integer.compare(this.node, other.node);
        }
    }
    public int[] dijkstra(int V, int[][] edges, int src) {
        // code here
        List<List<int[]>> adjList = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            adjList.get(u).add(new int[]{v, w});
            adjList.get(v).add(new int[]{u, w});
        }
        
        int dist[] = new int[V];
        for (int i = 0; i < V; i++) {
            dist[i] = (int) 1e9;
        }
        
        TreeSet<Pair> st = new TreeSet<>();
        
        st.add(new Pair(0, src));
        dist[src] = 0;
        
        while (!st.isEmpty()) {
            Pair cur = st.pollFirst();
            int u = cur.node;
            int du = cur.dist;
            for (int[] next : adjList.get(u)) {
                int v = next[0];
                int dv = next[1];
                if (du + dv < dist[v]) {
                    if (dist[v] != (int) 1e9) {
                        st.remove(new Pair(dist[v], v));
                    }
                    dist[v] = du + dv;
                    st.add(new Pair(du + dv, v));
                }
            }
        }
        return dist;
    }
}
```

### 1. **Priority Queue (Min-Heap) with Pruning**

- Typically implemented using **`PriorityQueue<int[]>`** (or a custom class with `Comparator`).
    
- You push `(dist, node)` pairs into the heap.
    
- When you pop a node, if its `dist` is **greater than the recorded best distance**, you prune (skip).
    
- **Complexity**:
    
    - Push/Pop = `O(log V)`
        
    - For all edges = `O((V+E) log V)` (tight bound).
        
- **Pros**:
    
    - Standard and widely accepted implementation.
        
    - Clear, concise, easy to understand.
        
    - Works well for dense and sparse graphs.
        
    - Heap operations are fast in Java.
        
- **Cons**:
    
    - Multiple duplicate entries for the same node may exist in the heap until pruned.
        

---

### 2. **Set (like `TreeSet`) with Pruning**

- Uses an **ordered set** keyed by distance.
    
- Nodes are stored only once, and when distance improves, you remove the old entry and insert the new one.
    
- **Complexity**:
    
    - Insert/Delete in `TreeSet` = `O(log V)`
        
    - Still `O((V+E) log V)`.
        
- **Pros**:
    
    - Each node has at most one entry in the set.
        
    - Avoids extra duplicates (compared to PriorityQueue).
        
- **Cons**:
    
    - Removing arbitrary elements (`set.remove(node)`) requires storing references or searching → `O(log V)`, but with higher overhead.
        
    - `TreeSet` relies on **`compareTo`/`Comparator`**, which makes it slower in practice.
        
    - More boilerplate code, less intuitive.
        
    - Can break if comparator doesn’t handle ties well (common bug).
        

---

### 🚀 **Which is better in Java?**

- **PriorityQueue with pruning** is **preferred in practice**.
    
    - Faster due to lower overhead than `TreeSet`.
        
    - More common in competitive programming, interviews, and real projects.
        
    - Easier to implement and less error-prone.
        
- **TreeSet approach** is mostly theoretical or useful when you _must_ avoid duplicates strictly.
    

---

✅ **Recommendation**:  
Use **`PriorityQueue` with pruning** unless you have a very specific reason to enforce unique entries (and are okay with extra coding overhead).




# Using BFS

TC -> O(E \* V)
```java
class Solution {
    public int[] dijkstra(int V, int[][] edges, int src) {
        // code here
        List<List<int[]>> adjList = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            adjList.get(u).add(new int[]{v, w});
            adjList.get(v).add(new int[]{u, w});
        }
        
        int dist[] = new int[V];
        for (int i = 0; i < V; i++) {
            dist[i] = (int) 1e9;
        }
        Queue<Integer> q = new LinkedList();
        
        q.offer(src);
        dist[src] = 0;
        
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int[] next : adjList.get(u)) {
                int v = next[0];
                int dv = next[1];
                if (dist[u] + dv < dist[v]) {
                    dist[v] = dist[u] + dv;
                    q.offer(v);
                }
            }
        }
        
        return dist;
    }
}
```


### ✅ Why it sometimes works?

- You’re relaxing edges just like in **Bellman-Ford** but in a BFS manner.
- For **unweighted graphs (all edges = 1)** this is exactly **BFS shortest path** → `O(V + E)`.
- For **weighted graphs (positive weights)**, it can still give correct results because you repeatedly relax until all shortest paths are settled.

