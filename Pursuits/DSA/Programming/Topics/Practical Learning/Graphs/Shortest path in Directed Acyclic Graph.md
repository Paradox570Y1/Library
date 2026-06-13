[Link](https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph/1)

Given a Directed Acyclic Graph of V vertices from 0 to n-1 and a 2D Integer array(or vector) edges[ ][ ] of length E, where there is a directed edge from edge[i][0] to edge[i][1] with a distance of edge[i][2] for all i.

Find the **shortest** path from **src(0)** vertex to all the vertices and if it is impossible to reach any vertex, then return **-1** for that vertex.

**Examples :  
**

**Input:** V = 4, E = 2, edges = `[[0,1,2], [0,2,1]]`
**Output:** [0, 2, 1, -1]  
**Explanation:** Shortest path from 0 to 1 is 0->1 with edge weight 2. Shortest path from 0 to 2 is 0->2 with edge weight 1. There is no way we can reach 3, so it's -1 for 3.

**Input:** V = 6, E = 7, edges = `[[0,1,2], [0,4,1], [4,5,4], [4,2,2], [1,2,3], [2,3,6], [5,3,1]]`
**Output:** [0, 2, 3, 6, 1, 5]  
**Explanation:** Shortest path from 0 to 1 is 0->1 with edge weight 2. Shortest path from 0 to 2 is 0->4->2 with edge weight 1+2=3. Shortest path from 0 to 3 is 0->4->5->3 with edge weight 1+4+1=6. Shortest path from 0 to 4 is 0->4 with edge weight 1.Shortest path from 0 to 5 is 0->4->5 with edge weight 1+4=5.

**Constraint:  
**1 <= V <= 100  
1 <= E <= min((N*(N-1))/2,4000)  
0 <= edgesi,0, edgesi,1 < n  
0 <= edgei,2 <=105



# Using Queue-based Bellman–Ford relaxation
Works with Positive weights

```java
class Solution {
    public int[] shortestPath(int V, int E, int[][] edges) {
        // Code here
        ArrayList<ArrayList<int[]>> adjList = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            adjList.get(edge[0]).add(new int[]{edge[1], edge[2]});
        }
        
        int[] res = new int[V];
        Arrays.fill(res, (int)1e9);
        
        Queue<Integer> q = new LinkedList<>();
        q.offer(0);
        res[0] = 0;
        // O(V * E) worst case
        while (!q.isEmpty()) {
            int node = q.poll();
            for (int next[] : adjList.get(node)) {
                if (res[next[0]] > res[node] + next[1]) {
                    res[next[0]] = res[node] + next[1];
                    q.offer(next[0]);
                }
            }
        }
        
        for (int i = 0; i < V; i++) {
            if (res[i] == (int)1e9) {
                res[i] = -1;
            }
        }
        
        return res;
    }
}
```

OR

```java
// User function Template for Java
class Solution {

    public int[] shortestPath(int V, int E, int[][] edges) {
        // Code here
        @SuppressWarnings("unchecked")
        ArrayList<int[]>[] graph = new ArrayList[V];
        for (int v = 0; v < V; v++) {
            graph[v] = new ArrayList<>();
        }
        
        for (int[] edge : edges) {
            int u = edge[0], v = edge[1], w = edge[2];
            graph[u].add(new int[]{v, w});
        }
        
        int[] dist = new int[V];
        Arrays.fill(dist, (int)1e9);
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(0);
        dist[0] = 0;
        
        while (!queue.isEmpty()) {
            int u = queue.poll();
            for (int[] next : graph[u]) {
                int v = next[0];
                int w = next[1];
                if (dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                    queue.offer(v);
                }
            }
        }
        for (int i = 0; i < V; i++) {
            if (dist[i] == (int) 1e9) dist[i] = -1;
        }
        return dist;
    }
}
```
#### ✅ Above Approach (Queue-based, BFS-like relaxation)

This is very **similar** to the **Shortest Path Faster Algorithm (SPFA)**, a queue optimization of Bellman-Ford:

- You keep pushing nodes into the queue whenever a relaxation improves their distance.
- It works here because the graph is a DAG (no cycles), so you won’t get infinite updates

### Pros

- Easier to implement (no topo sort recursion or stack needed).
- Intuitive: keep relaxing until no shorter path is found.

### Cons

- **Complexity isn’t strictly O(V + E).**
    
    - Worst case (with lots of edges and frequent re-relaxations), a node can re-enter the queue multiple times.
    - This can degrade to **O(V * E)** in general graphs.
    - In DAGs it’s usually better, but still not guaranteed as cleanly as topo order.
        
- Less predictable performance compared to topo sort.

---



# Using DFS with relaxation of edges

- We can solve this by combining Topo sort with [[Relaxation of edges]].
- The intuition behind this approach is the fact that in Topo sort , order of elements proceed from parent to child , hence from source to destination we keep computing the nodes. 


TC ->  O(E + V) x 2
SC -> After generating `adjList` and `res` array , extra space taken is O(V) by stack

```java
// User function Template for Java
class Solution {

    public int[] shortestPath(int V, int E, int[][] edges) {
        // Code here
        ArrayList<ArrayList<int[]>> adjList = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            adjList.get(edge[0]).add(new int[]{edge[1], edge[2]});
        }
        
        int[] res = new int[V];
        Arrays.fill(res, (int)1e9);
        
        Stack<Integer> order = new Stack<>();
        boolean vis[] = new boolean[V];
        // O (E + V)
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                topoSort (adjList, i, order, vis);
            }
        }
        res[0] = 0;
        // O (E + V)
        while (!order.isEmpty()) {
            int node = order.pop();
            for (int next[] : adjList.get(node)) {
                if (res[node] + next[1] < res[next[0]]) {
                    res[next[0]] = res[node] + next[1];
                }
            }
        }
        for (int i = 0; i < V; i++) {
            if (res[i] == (int) 1e9) {
                res[i] = -1;
            }
        }
        return res;
    }
    private void topoSort (ArrayList<ArrayList<int[]>> adjList, int node, Stack<Integer> order, boolean[] vis) {
        vis[node] = true;
        
        for (int next[] : adjList.get(node)) {
            if (!vis[next[0]]) {
                topoSort(adjList, next[0], order, vis);
            }
        }
        order.push(node);
    }
}
```

## ✅ Why This Approach is Good

1. **Topological Sorting**
    
    - You correctly compute a topological order of vertices (`topoSort`).
    - This ensures that when you process a node, all edges leading into it have already been considered.
        
2. **Relaxation in Topological Order**
    
    - After getting the topo order, you pop nodes and **relax all outgoing edges**.
    - This works in `O(V + E)` time, which is optimal for DAG shortest paths.
        
3. **Initialization with Infinity**
    
    - You used `(int) 1e9` to represent infinity and then replaced unreachable nodes with `-1`.
    - That’s standard practice.
        
4. **Space Efficient**
    
    - Using adjacency list with `int[]{to, weight}` is clean and avoids extra classes.




## ⚖️ Verdict

- **Topological Sort Approach (your first code)** → ✅ **better and standard** for DAG shortest path.
    
- **Queue-based Approach (your second code)** → works fine but is essentially an SPFA variant. Not as cleanly optimal for DAGs, and can be worse in terms of performance in dense cases.