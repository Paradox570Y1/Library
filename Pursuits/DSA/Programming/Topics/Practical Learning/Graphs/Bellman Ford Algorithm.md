- It's a single source Shortest Path Algorithm.
- If any path weight is less than zero then it's called negative cycle.
- Bellman Ford Algorithm helps you to detect negative cycles although it can't handle them but it can handle negative weights.

![[Pasted image 20250911111742.png|350]]

- This algorithm states that relax all edges N-1 times in Sequentially.

#### Why `N-1` iterations?

![[Pasted image 20250911120044.png|300]]
- In the worst case in each iteration we may only be able to relax 1 edge only. Since source edge is at distance 0 which is known. So, N-1 edges are left to be relaxed which can take upto N-1 iterations as per the worst case.

#### How to detect Negative Cycles?

- To detect them do 1 extra iteration which is Nth iteration.
- If `dist` array changes then that means some edge is further getting reduced due to some negative weight hence we can conclude that negative edge is discovered.


---
[Link](https://www.geeksforgeeks.org/problems/distance-from-the-source-bellman-ford-algorithm/1)
Given an weighted graph with **V** vertices numbered from 0 to V-1 and **E** edges, represented by a 2d array **edges[][]**, where **edges[i] = [u, v, w]** represents a direct edge from node **u** to **v** having **w** edge weight. You are also given a source vertex **src**.

Your task is to compute the **shortest distances** from the **source** to all other vertices. If a vertex is unreachable from the source, its distance should be marked as **108**. Additionally, if the graph contains a **negative weight cycle**, return **[-1]** to indicate that shortest paths cannot be reliably computed.

**Examples:**

**Input:** V = 5, edges\[]\[] = `[[1, 3, 2], [4, 3, -1], [2, 4, 1], [1, 2, 1], [0, 1, 5]]`, src = 0
![|200](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893096/Web/Other/blobid0_1744455175.jpg)
**Output:** [0, 5, 6, 6, 7]
**Explanation**: Shortest Paths:  
For 0 to 1 minimum distance will be 5. By following path 0 → 1
For 0 to 2 minimum distance will be 6. By following path 0 → 1  → 2
For 0 to 3 minimum distance will be 6. By following path 0 → 1  → 2 → 4 → 3 
For 0 to 4 minimum distance will be 7. By following path 0 → 1  → 2 → 4

**Input:** V = 4, edges\[]\[] =` [[0, 1, 4], [1, 2, -6], [2, 3, 5], [3, 1, -2]]`, src = 0
![|200](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893096/Web/Other/blobid1_1744455218.jpg)
**Output:** [-1]
**Explanation**: The graph contains a negative weight cycle formed by the path 1 → 2 → 3 → 1, where the total weight of the cycle is negative.

**Constraints:  
**1 ≤ V ≤ 100  
1 ≤ E = edges.size() ≤ V*(V-1)  
-1000 ≤ w ≤ 1000  
0 ≤ src < V



```java
class Solution {
    public int[] bellmanFord(int V, int[][] edges, int src) {
        // code here
        
        int dist[] = new int[V];
        Arrays.fill(dist, (int)1e8);
        dist[src] = 0;
        //TC -> V x E
        for (int i = 0; i < V-1; i++) {
            for (int edge[] : edges) {
                int u = edge[0];
                int v = edge[1];
                int w = edge[2];
                if (dist[u] != (int)1e8 && dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                }
            }
        }
        // For checking negative cycle
        for (int edge[] : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            if (dist[u] != (int)1e8 && dist[u] + w < dist[v]) {
               return new int[]{-1};
            }
        }
        return dist;
    }
}

```

OR

```java
class Solution {
    public int[] bellmanFord(int V, int[][] edges, int src) {
        // code here
        
        int dist[] = new int[V];
        Arrays.fill(dist, (int)1e8);
        dist[src] = 0;
        for (int i = 0; i < V; i++) {
            for (int edge[] : edges) {
                int u = edge[0];
                int v = edge[1];
                int w = edge[2];
                if (dist[u] != (int)1e8 && dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                    if (i == V-1) return new int[]{-1};
                }
            }
        }
        return dist;
    }
}

```

![[Pasted image 20251125195023.png]]

👉 So, you can remember:

- **Dijkstra → only non-negative edges**.
- **Bellman–Ford → can handle negative edges, detects cycles, but slower**.
- **Floyd–Warshall → all-pairs, works with negative edges, detects cycles**.