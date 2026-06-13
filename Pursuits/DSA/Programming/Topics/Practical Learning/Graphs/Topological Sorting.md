- Topological Ordering refers to any linear ordering of vertices such there is an edge between u & v where u always appears before v in that ordering.
- It only exists on DAG (Directed Acyclic Graph).
- There could be many number of such ordering for a single graph.
![[Pasted image 20250905181304.png|300]]


# Why only in DAG?

- In Undirected graph if u → v then v → u due to which it becomes impossible to place u before v as it can exist after it too. Hence this exist only in Directed Graph.
	- Same is the case when there is cycle in Directed Graph, If a -> b , b -> c , c -> a , then `c` can't exist before and after `a` at the same time. So it should be Acyclic. 


# Using DFS

- To print the Sequence
```java
class Solution {
    public static ArrayList<Integer> topoSort(int V, int[][] edges) {
        
        boolean vis[] = new boolean[V];
        List<List<Integer>> adjList = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int edge[] : edges) {
            adjList.get(edge[0]).add(edge[1]);
        }
        
        Stack<Integer> res = new Stack<>();
        
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                dfs(adjList, i, vis, res);
            }
        }
        
        ArrayList<Integer> ans = new ArrayList<>();
        while (!res.isEmpty()) {
            ans.add(res.pop());
        }
        return ans;
    }
    
    private static void dfs(List<List<Integer>> adjList, int node, boolean[] vis, Stack<Integer> res) {
        vis[node] = true;
        for (int next : adjList.get(node)) {
            if (!vis[next]) {
                dfs(adjList, next, vis, res);
            }
        }
        res.add(node);
    }
}
```

Condition to Check if Topological sort of graph is possible or not using dfs:
- If there is any cycle in dfs than no topological order exists. So using path and vis arrays check for cycles simultaneously.
Following is the implementation to check if cycle exists or not.
[[Directed Graph Cycle]]


# Using BFS (Kahn's Algorithm)


```java
class Solution {
    public static ArrayList<Integer> topoSort(int V, int[][] edges) {
        // code here
        int[] inorder = new int[V];
        
        List<List<Integer>> adjList = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] edge : edges) {
            adjList.get(edge[0]).add(edge[1]);
            inorder[edge[1]]++;
        }
        
        Queue<Integer> queue = new LinkedList<>();
        ArrayList<Integer> res = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            if (inorder[i] == 0) {
                queue.offer(i);
            }
        }
        
        while (!queue.isEmpty()) {
            int node = queue.poll();
            res.add(node);
            
            for (int next: adjList.get(node)) {
                inorder[next]--;
                if (inorder[next] == 0) queue.offer(next);
            }
        }
        
        return res;
    }
}
```

Condition to Check if Topological sort of graph is possible or not using Kahn's algo:
- If Sequence length is less than the number of vertices then it means topo order of that graph doesn't exist.




# Which one to prefer

### **1. Using DFS (Depth First Search)**

- Idea: Perform a DFS, and when a node finishes (i.e., all its neighbors are visited), push it onto a stack.
    
- At the end, popping from the stack gives a valid topological order.
    
- **Complexity:** `O(V + E)`
    
- **Pros:**
    
    - Simple recursive implementation.
    - Naturally leverages the "postorder" property of DFS.
- **Cons:**
    
    - Recursion may cause stack overflow for very large graphs.
    - Harder to detect cycles unless handled carefully.

---

### **2. Using BFS (Kahn’s Algorithm)**

- Idea: Count in-degrees of all nodes. Put all nodes with in-degree `0` in a queue. Repeatedly pop from the queue, reduce the in-degree of neighbors, and push them into the queue when their in-degree becomes `0`.
    
- The order of removal gives the topological order.
    
- **Complexity:** `O(V + E)`
    
- **Pros:**
    
    - Iterative, avoids recursion depth issues.
        
    - Naturally detects cycles: if processed nodes < `V`, graph has a cycle.
        
- **Cons:**
    
    - Needs extra space for in-degree array and queue.
        

---

### ✅ **Preferred Choice in Practice**

- **Kahn’s Algorithm (BFS)** is often preferred in competitive programming & production because it:
    
    - Explicitly detects cycles,
        
    - Is iterative and safer for large inputs.
        
- **DFS** is also widely used, especially in teaching and recursive codebases. It's elegant and often faster to write.
    

---

👉 Rule of Thumb:

- If you need **cycle detection explicitly** → Use **BFS (Kahn’s)**.
    
- If recursion depth is not a concern and you want a **quick implementation** → Use **DFS**.