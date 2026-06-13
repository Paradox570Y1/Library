- It's a Multi-source Shortest Path algorithm
- This algorithm is not much intuitive as other ones.
- It is kind of brute force where all the combination of paths had been tried to get the shortest path.
- It's Time Complexity is O(N³)
- This doesn't work for negative cycle but works for negative weights.
- You can achieve similar feat with Dijkstra as long as there is no negative cycles and it's time complexity will still be better O (N x E log V).
# Intuition

![[Pasted image 20250911123907.png|200]]
- Go via every node or vertex
- Let's say we want to go from 0 to 1.
![[Pasted image 20250911124112.png|300]]
![[Pasted image 20250911124045.png|200]]
- During the process we are gonna store computation to use it later just like DP.


# For Directed Graph

![[Pasted image 20250911124423.png|300]]




# For Undirected Graph
- Consider edges as bi-directional edge in directed graph with same weight both ways for developing adjacency matrix.
![[Pasted image 20250911124443.png|120]]


# How to detect a negative cycle
![[Pasted image 20250912063527.png|300]]


---
[Link](https://www.geeksforgeeks.org/problems/implementing-floyd-warshall2042/1)

You are given an weighted **directed** graph, represented by an adjacency matrix, **dist\[]\[]** of size **n x n**, where **dist\[i]\[j]** represents the weight of the edge from **node i to node j**. If there is no direct edge, **dist\[i]\[j]** is set to a large value (i.e., **108**) to represent infinity.  
The graph may contain **negative edge weights**, but it does not contain any **negative weight cycles**.

Your task is to find the **shortest distance** between every pair of nodes **i** and **j** in the graph.

Note: Modify the distances for every pair **in place**.

**Examples :**

**Input:** dist[][] = `[[0, 4, 108, 5, 108], [108, 0, 1, 108, 6], [2, 108, 0, 3, 108], [108, 108, 1, 0, 2], [1, 108, 108, 4, 0]]  `
![|250](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893245/Web/Other/blobid0_1744701272.jpg)  
**Output:** `[[0, 4, 5, 5, 7], [3, 0, 1, 4, 6], [2, 6, 0, 3, 5], [3, 7, 1, 0, 2], [1, 5, 5, 4, 0]]`
![|250](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893245/Web/Other/blobid1_1744701370.jpg)  
**Explanation:** Each cell dist[i][j] in the output shows the shortest distance from node i to node j, computed by considering all possible intermediate nodes. 

**Input:** dist[][] = `[[0, -1, 2], [1, 0, 108], [3, 1, 0]]`
![|200](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893245/Web/Other/blobid2_1744701698.jpg)  
**Output:** `[[0, -1, 2], [1, 0, 3], [2, 1, 0]]`
![|200](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893245/Web/Other/blobid3_1744701713.jpg)  
**Explanation:** Each cell dist[i][j] in the output shows the shortest distance from node i to node j, computed by considering all possible intermediate nodes.  
From 2 to 0 shortest distance should be 2 by following path 2 -> 1 -> 0  
From 1 to 2 shortest distance should be 3 by following path 1 -> 0 -> 2

**Constraints:**  
1 ≤ dist.size() ≤ 100  
-1000 ≤ dist[i][j] ≤ 1000  
dist[i][j] can be **108** to represent infinity.



```java
// User function template for JAVA

class Solution {
    public void floydWarshall(int[][] dist) {
        // Code here
        int N = dist.length;
        
        for (int via = 0; via < N; via++) { 
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    if (dist[i][via] != (int) 1e8 && dist[via][j] != (int)1e8)
                    dist[i][j] = Math.min(dist[i][j], dist[i][via] + dist[via][j]);
                }
            }
        }
    }
}
```


In case we need to check -ve cycle

```java
// User function template for JAVA

class Solution {
    public void floydWarshall(int[][] dist) {
        int N = dist.length;
        int INF = (int) 1e9;

        // Core Floyd–Warshall
        for (int via = 0; via < N; via++) {
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {

                    // Important guard to avoid INF overflow
                    if (dist[i][via] < INF && dist[via][j] < INF) {
                        dist[i][j] = Math.min(
                            dist[i][j],
                            dist[i][via] + dist[via][j]
                        );
                    }
                }
            }
        }

        // Negative cycle detection
        for (int i = 0; i < N; i++) {
            if (dist[i][i] < 0) {
                // Negative cycle exists
                // Problem-specific handling can be done here
                // Example: mark all distances as -1
                // (depends on platform requirements)
                System.out.println("Negative cycle detected");
                return;
            }
        }
    }
}

```