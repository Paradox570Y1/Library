- Nodes on which removal, graph breaks into multiple components is called articulation point.
- Now instead of looking for edge which breaks the graph, we are looking for Vertex which breaks the graph.



It Uses:
- Time of insertion : The step at which you are reaching a node while DFS.
- Lowest time of insertion : It will compare the `lowest time of insertion` of all adjacent node apart from parent and visited nodes.
	- If node is not parent and is visited then take `lowest time of insertion`.
	- This is slightly different than bridge.
	- Why take `Time of insertion` instead of `lowest Time of insertion` of adjacent Node in visited nodes?
		- This is because if there is articulation point then on removing it we cannot reach nodes via that articulation point in another component.

![[Pasted image 20250923115839.png|250]]

### Important points
- Starting point can be articulation only when it has multiple children.
- An articulation point can be taken multiple times during traversal after returning from multiple components.


[Link](https://www.geeksforgeeks.org/problems/articulation-point-1/1)
### Articulation Point - I

Difficulty: **Hard**Accuracy: **39.26%**Submissions: **85K+**Points: **8**Average Time: **20m**

Given an undirected connected graph with **V** vertices and adjacency list **adj**. You are required to find all the vertices removing which (and edges through it) disconnects the graph into 2 or more components and return it in sorted manner.  
**Note:** Indexing is zero-based i.e nodes numbering from (0 to V-1). There might be loops present in the graph.

**Example 1:**

**Input:**
![](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/708502/Web/Other/a27f9040-9783-4386-92f9-b8684c75db07_1685087852.png)
**Output:**{1,4}
**Explanation:** Removing the vertex 1 will
discconect the graph as-
![](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/708502/Web/Other/7e12629a-ba31-411e-b6ac-ccf5a8baa6a3_1685087852.png)
Removing the vertex 4 will disconnect the
graph as-
![](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/708502/Web/Other/fb781bda-91d6-4920-96a8-c976412c3ada_1685087852.png)

**Your Task:**  
You don't need to read or print anything. Your task is to complete the function **articulationPoints****()** which takes V and adj as input parameters and returns a list containing all the vertices removing which turn the graph into two or more disconnected components in sorted order. If there are no such vertices then returns a list containing -1.  
 

**Expected Time Complexity:** O(V + E)  
**Expected Auxiliary Space:** O(V)  
 

**Constraints:**  
1 ≤ V ≤ 105

TC -> O (V + 2E) same as DFS 
```java
class Solution {
    // Function to return Breadth First Traversal of given graph.
    private int timer;
    public ArrayList<Integer> articulationPoints(int V,
                                                 ArrayList<ArrayList<Integer>> adj) {
        // Code here
        boolean ap[] = new boolean[V];
        timer = 0;
        boolean[] vis = new boolean[V];
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                dfs(adj, 0, -1, vis, new int[V], new int[V], ap);
            }
        }
        ArrayList<Integer> ans = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            if (ap[i]) ans.add(i);
        }
        if (ans.size() == 0) ans.add(-1);
        return ans;
    }
    private void dfs(ArrayList<ArrayList<Integer>> adj, int child, int parent, boolean[] vis, int time[], int[] low, boolean[] ap) {
        vis[child] = true;
        time[child] = low[child] = timer;
        timer++;
        int nodes = 0;
        for (int adjNode : adj.get(child)) {
            if(adjNode == parent) continue;
            if (!vis[adjNode]) {
                dfs(adj, adjNode, child, vis, time, low, ap);
                low[child] = Math.min(low[adjNode], low[child]);
                if (low[adjNode] >= time[child] && parent != -1) {
                    ap[child] = true;
                }
                nodes++;
            } else {
                low[child] = Math.min(low[child], time[adjNode]);
            }
        }
        if (nodes > 1 && parent == -1) {
            ap[child]  = true;
        }
    }
}
```

OR

```java
class Solution {
    // Function to return Breadth First Traversal of given graph.
    private int timer;
    public ArrayList<Integer> articulationPoints(int V, ArrayList<ArrayList<Integer>> adj) {
        // Code here
        int[] disc = new int[V];
        int[] low = new int[V];
        timer = 0;
        Arrays.fill(disc, -1);
        Arrays.fill(low, -1);
        TreeSet<Integer> res = new TreeSet<>();
        scc(adj, 0, -1, disc, low, res);
        if (res.size() == 0) return new ArrayList<>(List.of(-1));
        return new ArrayList<>(res);
    }
    private void scc(ArrayList<ArrayList<Integer>> adj, int u, int p, int[] disc, int[] low, TreeSet<Integer> res) {
        disc[u] = low[u] = timer++;
        int children = 0;
        for (int v : adj.get(u)) {
            if (disc[v] == -1) {
                children++;
                scc(adj, v, u, disc, low, res);
                low[u] = Math.min(low[u], low[v]);
                if (p != -1 && low[v] >= disc[u]) res.add(u); // >= bcz v cannot visit ancenstor of u but it's fine if it can visit u itself as removal of u still degenrate the graph
            } else if (v != p) {
                low[u] = Math.min(low[u], disc[v]);
            }
            if (p == -1 && children > 1) res.add(u);
        }
    }
}
```

OR

```java
class Solution {
    // Function to return Breadth First Traversal of given graph.
    private int timer;
    public ArrayList<Integer> articulationPoints(int V, ArrayList<ArrayList<Integer>> adj) {
        // Code here
        int[] disc = new int[V];
        int[] low = new int[V];
        timer = 0;
        Arrays.fill(disc, -1);
        Arrays.fill(low, -1);
        boolean[] res = new boolean[V];
        scc(adj, 0, -1, disc, low, res);
        ArrayList<Integer> ans = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            if (res[i]) ans.add(i);
        }
        if (ans.size() == 0) return new ArrayList<>(List.of(-1));
        return ans;
    }
    private void scc(ArrayList<ArrayList<Integer>> adj, int u, int p, int[] disc, int[] low, boolean[] res) {
        disc[u] = low[u] = timer++;
        int children = 0;
        for (int v : adj.get(u)) {
            if (disc[v] == -1) {
                children++;
                scc(adj, v, u, disc, low, res);
                low[u] = Math.min(low[u], low[v]);
                if (p != -1 && low[v] >= disc[u]) res[u] = true;
            } else if (v != p) {
                low[u] = Math.min(low[u], disc[v]);
            }
            if (p == -1 && children > 1) res[u] = true;
        }
    }
}
```

OR

```java
class Solution {
    // Function to return Breadth First Traversal of given graph.
    private int timer;
    public ArrayList<Integer> articulationPoints(int V,
                                                 ArrayList<ArrayList<Integer>> adj) {
        // Code here
        int[] disc = new int[V];
        Arrays.fill(disc, -1);
        int[] low = new int[V];
        ArrayList<Integer> res = new ArrayList<>();
        boolean[] pos = new boolean[V];
        timer = 0;
        for (int i = 0; i < V; i++) {
            if (disc[i] == -1) {
                helper(adj, i, disc, low, -1, pos);
            }
        }
        for (int i = 0; i < V; i++) {
            if (pos[i]) res.add(i);
        }
        if (res.size() == 0) res.add(-1);
        return res;
    }
    
    private void helper(ArrayList<ArrayList<Integer>> adj, int u, int[] disc, int[] low, int p, boolean[] pos) {
        disc[u] = low[u] = timer++;
        int child = 0;
        for (int v : adj.get(u)) {
            if (p == v) continue;
            if (disc[v] == -1) {
                helper(adj, v, disc, low, u, pos);
                low[u] = Math.min(low[u], low[v]);
                if (disc[u] <= low[v] && p != -1) pos[u] = true;
                child++;
            } else {
                low[u] = Math.min(low[u], disc[v]);
            }
        }
        if (p == -1 && child > 1) {
            pos[u] = true;
        }
    }
}
```