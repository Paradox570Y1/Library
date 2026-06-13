- It helps in finding Minimum Spanning Tree.
- Greedy is the intuition behind Prim's Algo.
- It is similar to Dijkstra algorithm but visited array is used and marked while enqueuing.

We will be requiring following tools:
- Priority Queue
	- In case you want the MST graph then u use `{weight, node, parent}`
	- In case you just want the sum of weight of MST then `{weight, node}` is enough.
- Visited Array
- Sum variable to store the summation of weights.
- MST edges list to store result.


### Process
- We can start with any node and we will be storing  MST in form of edges.
- In Priority Queue we will be inserting data structured as `{weight, node, parent}` and sorted based on weight in ascending.
- For the initial node, take parent to be -1 and weight will be 0 also mark it as visited.
- Since first node's parent is -1, this means that it not an edge and hence cannot be added to MST but since it's weight is 0 so that doesn't affect result. 
- Now look up for neighbor nodes connected to the current node and add them to queue by taking current node as parent along with weight of the edge connecting them. But `do not` mark them visited.
- Now poll the least weight edge and add that edge to MST and also increase sum counter by the weight of edge and then mark this edge as visited.
- Continue this process
	![[Pasted image 20250912191159.png|400]]


---
[Minimum Spanning Tree](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)
Given a weighted, undirected, and connected graph with V vertices and E edges, your task is to find the sum of the weights of the edges in the Minimum Spanning Tree (MST) of the graph. The graph is provided as a list of edges, where each edge is represented as [u, v, w], indicating an edge between vertex u and vertex v with edge weight w.

**Input:** V = 3, E = 3, Edges = `[[0, 1, 5], [1, 2, 3], [0, 2, 1]]`
![|250](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700343/Web/Other/blobid1_1744376821.jpg)   
**Output:** 4
**Explanation**:
![|250](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700343/Web/Other/blobid2_1744376854.jpg)  
The Spanning Tree resulting in a weight
of 4 is shown above.

**Input:** V = 2, E = 1, Edges = `[[0 1 5]]`
  
 ![|250](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700343/Web/Other/blobid3_1744376890.jpg)  
  
**Output:** 5   
**Explanation**: Only one Spanning Tree is possible which has a weight of 5.  

**Constraints:  
**2 ≤ V ≤ 1000  
V-1 ≤ E ≤ (V*(V-1))/2  
1 ≤ w ≤ 1000  
The graph is connected and doesn't contain self-loops & multiple edges.


# Prim's Algo Implementation

TC -> E log E + E log E = 2E log E
```java
class Solution {
    public int spanningTree(int V, int[][] edges) {
        // code here
        List<List<int[]>> adjList = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        //O(E)
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            adjList.get(u).add(new int[]{v, w});
            adjList.get(v).add(new int[]{u, w});
        }
        
        boolean[] vis = new boolean[V];
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.offer(new int[]{0, 0});
        
        int sum = 0;
        //E log E
        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            int u = cur[0];
            int weight = cur[1];
            if (vis[u]) continue;
            sum += weight;
            vis[u] = true;
            // Amortized E log E
            for (int[] next : adjList.get(u)) {
                int v = next[0];
                int w = next[1];
                if (!vis[v]) {
                    pq.offer(new int[]{v, w});
                }
            }
        }
        return sum;
    }
}

```


OR
In case you want to find parents as well then use 3 parameters along with result array to store edges.
```java
class Solution {
    public int spanningTree(int V, int[][] edges) {
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
        
        boolean[] vis = new boolean[V];
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.offer(new int[]{0, 0, -1});
        
        int sum = 0;
        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            int u = cur[0];
            int weight = cur[1];
            int parent = cur[2];
            if (!vis[u]) {//works but use if(vis[u]) continue for better runtime
                sum += weight;
                vis[u] = true;
            }
            for (int[] next : adjList.get(u)) {
                int v = next[0];
                int w = next[1];
                if (!vis[v]) {
                    pq.offer(new int[]{v, w, u});
                }
            }
        }
        return sum;
    }
}

```

