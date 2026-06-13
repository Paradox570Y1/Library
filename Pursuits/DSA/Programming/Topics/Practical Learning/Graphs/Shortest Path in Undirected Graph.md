# For unit weight graph level order traversal is enough
[Link](https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph-having-unit-distance/1)

You are given an adjacency list, **adj** of **Undirected Graph** having **unit weight** of the edges, find the shortest path from **src** to all the vertex and if it is **unreachable** to reach any vertex, then return **-1** for that vertex.

**Examples :**

**Input:** adj\[]\[] = `[[1, 3], [0, 2], [1, 6], [0, 4], [3, 5], [4, 6], [2, 5, 7, 8], [6, 8], [7, 6]]`, src=0
**Output:** `[0, 1, 2, 1, 2, 3, 3, 4, 4]  `
![|300](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/711976/Web/Other/blobid0_1745302423.jpg)

**Input:** adj\[]\[]= `[[3], [3], [], [0, 1]]`, src=3
**Output:**` [1, 1, -1, 0]  `
![|300](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/711976/Web/Other/blobid0_1747111194.webp)  

**Input:** adj\[]\[]= `[[], [], [], [4], [3], [], []]`, src=1
**Output:** `[-1, 0, -1, -1, -1, -1, -1] `

**Constraint:**  
1<=adj.size()<=104  
0<=edges<=adj.size()-1

# BFS

```java
class Solution {
    public int[] shortestPath(ArrayList<ArrayList<Integer>> adj, int src) {
        // code here
        Queue<Integer> q = new LinkedList<>();
        int res[] = new int[adj.size()];
        Arrays.fill(res, -1);
        boolean vis[] = new boolean[adj.size()];
        
        q.offer(src);
        res[src] = 0;
        vis[src] = true;
        while (!q.isEmpty()) {
            int node = q.poll();
            for (int next : adj.get(node)) {
                if (!vis[next]) {
                    vis[next] = true;
                    res[next] = res[node] + 1;
                    q.offer(next);
                }
            }
        }
        
        return res;
    }
}

```


After Optimizing little space by removing visited array

```java
class Solution {
    public int[] shortestPath(ArrayList<ArrayList<Integer>> adj, int src) {
        // code here
        Queue<Integer> q = new LinkedList<>();
        int res[] = new int[adj.size()];
        Arrays.fill(res, -1);
        
        q.offer(src);
        res[src] = 0;
        while (!q.isEmpty()) {
            int node = q.poll();
            for (int next : adj.get(node)) {
                if (res[next] == -1) {
                    res[next] = res[node] + 1;
                    q.offer(next);
                }
            }
        }
        
        return res;
    }
}

```



OR 
Striver's way
```java
class Solution {
    public int[] shortestPath(ArrayList<ArrayList<Integer>> adj, int src) {
        // code here
        int res[] = new int[adj.size()];
        Arrays.fill(res, (int)1e9);
        
        Queue<Integer> q = new LinkedList<>();
        q.offer(src);
        res[src] = 0;
        
        while (!q.isEmpty()) {
            int node = q.poll();
            
            for (int next : adj.get(node)) {
                if (res[next] > res[node] + 1) {
                    res[next] = res[node] + 1;
                    q.offer(next);
                }
            }
        }
        
        for (int i = 0; i < res.length; i++) {
            if (res[i] == (int) 1e9) {
                res[i] = -1;
            }
        }
        return res;
    }
}

```