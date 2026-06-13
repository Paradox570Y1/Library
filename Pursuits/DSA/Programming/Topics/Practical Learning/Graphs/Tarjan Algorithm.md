Bridges in Graph
- Bridge means an edges which connects 2 components and on removing it graph gets broken into 2 components.
- We will be using some logic on DFS to implement bridge in Graph.
- Our goal is to find edges which form a bridge.


It Uses:
- Time of insertion : The step at which you are reaching a node while DFS.
- Lowest time of insertion : It will compare the lowest time of insertion of all adjacent node apart from parent.
![[Pasted image 20250919230638.png|200]]

[1192. Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network/)

There are `n` servers numbered from `0` to `n - 1` connected by undirected server-to-server `connections` forming a network where `connections[i] = [ai, bi]` represents a connection between servers `ai` and `bi`. Any server can reach other servers directly or indirectly through the network.

A _critical connection_ is a connection that, if removed, will make some servers unable to reach some other server.

Return all critical connections in the network in any order.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/09/03/1537_ex1_2.png)

**Input:** n = 4, connections = `[[0,1],[1,2],[2,0],[1,3]]`
**Output:** `[[1,3]]`
**Explanation:** `[[3,1]]` is also accepted.

**Example 2:**

**Input:** n = 2, connections = `[[0,1]]`
**Output:** `[[0,1]]`

**Constraints:**

- `2 <= n <= 105`
- `n - 1 <= connections.length <= 105`
- `0 <= ai, bi <= n - 1`
- `ai != bi`
- There are no repeated connections.


# Using Tarjan Algorithm

```java
class Solution {
    private int timer;
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adjList.add(new ArrayList<>());
        }
        for (List<Integer> connection : connections) {
            int u = connection.get(0);
            int v = connection.get(1);
            adjList.get(u).add(v);
            adjList.get(v).add(u);
        }
        boolean[] vis = new boolean[n];
        int[] disc = new int[n];
        int[] low = new int[n];
        this.timer = 1;
        List<List<Integer>> bridges = new ArrayList<>();
        dfs(adjList, 0, -1, bridges, disc, low, vis);
        return bridges;
    }
    private void dfs(List<List<Integer>> adjList,int child, int parent, List<List<Integer>> bridges, int[] disc, int[] low, boolean[] vis) {
        vis[child] = true;
        low[child] = disc[child] = timer;
        timer++;
        for (int node : adjList.get(child)) {
            if (node == parent) continue;
            if (!vis[node]) {
                dfs(adjList, node, child, bridges, disc, low, vis);
                low[child] = Math.min(low[child], low[node]);
                if (disc[child] < low[node]) bridges.add(Arrays.asList(child, node));
            } else {
                low[child] = Math.min(low[child], low[node]);
            }
        }
    }
}
```

OR
Same code after taking common elements inside dfs
```java
class Solution {
    private int timer;
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adjList.add(new ArrayList<>());
        }
        for (List<Integer> connection : connections) {
            int u = connection.get(0);
            int v = connection.get(1);
            adjList.get(u).add(v);
            adjList.get(v).add(u);
        }
        boolean[] vis = new boolean[n];
        int[] disc = new int[n];
        int[] low = new int[n];
        this.timer = 1;
        List<List<Integer>> bridges = new ArrayList<>();
        dfs(adjList, 0, -1, bridges, disc, low, vis);
        return bridges;
    }
    private void dfs(List<List<Integer>> adjList,int child, int parent, List<List<Integer>> bridges, int[] disc, int[] low, boolean[] vis) {
        vis[child] = true;
        low[child] = disc[child] = timer;
        timer++;
        for (int node : adjList.get(child)) {
            if (node == parent) continue;
            if (!vis[node]) {
                dfs(adjList, node, child, bridges, disc, low, vis);
                if (disc[child] < low[node]) bridges.add(Arrays.asList(child, node));
            }
            low[child] = Math.min(low[child], low[node]);
        }
    }
}
```

OR

```java
class Solution {
    private int timer;
    private List<List<Integer>> res;
    private void buildGraph(List<Integer>[] graph, int n, List<List<Integer>> connections) {
        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<>();
        }

        for (List<Integer> connection : connections) {
            int u = connection.get(0), v = connection.get(1);
            graph[u].add(v);
            graph[v].add(u);
        }
    }
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        
        List<Integer>[] graph = new ArrayList[n];
        buildGraph(graph, n, connections);
        
        int[] disc = new int[n];
        Arrays.fill(disc, -1);
        int[] low = new int[n];
        timer = 0;
        res = new ArrayList<>();
        helper(graph, low, disc, 0, -1);
        return res;
    }

    private void helper(List<Integer>[] graph, int[] low, int[] disc, int u, int p) {
        disc[u] = low[u] = timer++;
        for (int v : graph[u]) {
            if (v == p) continue;
            if (disc[v] == -1) {
                helper(graph, low, disc, v, u);
                low[u] = Math.min(low[u], low[v]);
                if (disc[u] < low[v]) res.add(new ArrayList<>(Arrays.asList(u, v)));
            } else {
                low[u] = Math.min(low[v], low[u]);
            }
        }
    }
}
```

OR

```java
class Solution {
    private int timer;
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < n; i++) adjList.add(new ArrayList<>());

        for (List<Integer> connection : connections) {
            int u = connection.get(0), v = connection.get(1);
            adjList.get(u).add(v);
            adjList.get(v).add(u);
        }

        List<List<Integer>> res = new ArrayList<>();
        int[] disc = new int[n];
        int[] low = new int[n];
        Arrays.fill(disc, -1);
        Arrays.fill(low, -1);
        timer = 0;
        findSCC(adjList, 0, disc, low, res, -1);
        return res;
    }
    private void findSCC(List<List<Integer>> adjList, int u, int[] disc, int[] low, List<List<Integer>> res, int p) {
        disc[u] = low[u] = timer++;
        for (int v : adjList.get(u)) {
            if (disc[v] == -1) {
                findSCC(adjList, v, disc, low, res, u);
                low[u] = Math.min(low[u], low[v]);
                if (disc[u] < low[v]) res.add(new ArrayList<>(List.of(u, v)));
            } else if (v != p){
                low[u] = Math.min(disc[v], low[u]);
            }
        }
    }
}
```


**Giving Memory Limit Exceeded on using Adjacency Matrix**

```java
class Solution {
    private int timer;
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        boolean[][] adjMat = new boolean[n][n];

        for (List<Integer> connection : connections) {
            int u = connection.get(0);
            int v = connection.get(1);
            adjMat[u][v] = true;
            adjMat[v][u] = true;
        }
        boolean[] vis = new boolean[n];
        int[] disc = new int[n];
        int[] low = new int[n];
        this.timer = 1;
        List<List<Integer>> bridges = new ArrayList<>();
        dfs(adjMat, 0, -1, bridges, disc, low, vis);
        return bridges;
    }
    private void dfs(boolean[][] adjMat,int child, int parent, List<List<Integer>> bridges, int[] disc, int[] low, boolean[] vis) {
        vis[child] = true;
        low[child] = disc[child] = timer;
        timer++;
        for (int node = 0; node < adjMat.length; node++) {
            if(!adjMat[child][node]) continue;
            if (node == parent) continue;
            if (!vis[node]) {
                dfs(adjMat, node, child, bridges, disc, low, vis);
                low[child] = Math.min(low[child], low[node]);
                if (disc[child] < low[node]) bridges.add(Arrays.asList(child, node));
            } else {
                low[child] = Math.min(low[child], low[node]);
            }
        }
    }
}
```