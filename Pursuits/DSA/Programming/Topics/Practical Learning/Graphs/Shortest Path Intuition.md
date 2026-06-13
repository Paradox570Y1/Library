Algorithms
- DAG shortest path (Topological sorting + relaxation of edges) works with negative edges
- SPFA (Queue based bellman ford relaxation) (this also works with -ve edges but not -ve cycles)
- Dijkstra algorithm (works with cycles but not with negative edge or negative cycle)
- Bellman ford Algorithm (works with -ve edges but not with -ve cycles but it can detect -ve cycle)

In undirected graph:
- Unit weights
	- we can make use of general BFS.
- Variable weights
	- In an undirected graph, a negative edge creates an immediate negative cycle (u → v → u), so queue-based **Bellman–Ford** relaxation will malfunction unless negative-cycle detection is used.
	- In this case we have to use [[Dijkstra Algorithm]] where we use Priority Queue to ensure relaxation of edges for smaller weights first and using pruning to prevent redundant computation on bigger weights.

In directed graph:
- Unit weights
	- we can make use of general BFS.
- Variable weights
	- For DAG we can use Queue based **Bellman-ford** relaxation
		- Does not work for -ve cycles which do not exist in DAG but works for -ve weights.
	- We can also use DFS  with relaxation of edges where we get **Topological order** using DFS and then use it for relaxation of edges using stack or any array.
	- We can also use **Dijkstra** Algorithm in directed graph.
	- Other ways include DFS + Pruning in which you have to do precomputation by sorting the edges in descending order and then perform relaxation of edges using DFS implemented iteratively to prevent Stack Overflow with pruning technique to optimize performance.

![[Pasted image 20260125231806.png]]

# Which algo to use for Directed graph with variable weights

## 🔹 Case 1: **Topological Sort + Relaxation**

- Works only when the graph is a **DAG (Directed Acyclic Graph)**.
    
- Idea:
    
    - Perform a **topological sort**.
        
    - Process vertices in topological order and relax their outgoing edges.
        
- **Complexity:** `O(V + E)` → very efficient.
    
- **Pros:**
    
    - Faster than Dijkstra.
        
    - Handles **negative weights** (as long as there are no cycles).
        
- **Cons:**
    
    - Only valid if the graph is a **DAG**. If there’s a cycle, this approach fails.
        

---

## 🔹 Case 2: **Dijkstra’s Algorithm**

- Works on any directed graph with **non-negative weights**.
    
- Idea: Greedily pick the vertex with the smallest tentative distance and relax edges.
    
- **Complexity:**
    
    - With adjacency list + min-heap → `O((V + E) log V)`.
        
- **Pros:**
    
    - General-purpose: works for **any graph** (with non-negative weights).
        
    - Doesn’t require DAG structure.
        
- **Cons:**
    
    - Slower than DAG-based DP approach.
        
    - Cannot handle negative weights.
        

---

## ✅ Which One to Choose?

- **Graph is a DAG (and maybe has negative weights but no cycle)** → Use **Topological Sort + Relaxation** (faster and simpler).
    
- **Graph has cycles or is not guaranteed to be acyclic but doesn't not have negative weights** → Use **Dijkstra** (safe, but slower).
    
- **Graph has negative weights & cycles possible** → You need **Bellman-Ford** (O(VE)).