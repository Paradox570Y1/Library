![[Pasted image 20250822212231.png|400]]
- Graph holds the relation between two entities or it holds some information about two entities
- Nodes
	-  They are represented with Circle.
	- They are also called Vertex.
	- They are often represented with a number but there is not particular order for their numbering
- Edge
	- They are represented with horizontal line.
		- Now it can be a directed edge or an undirected edge.
		- In case of undirected edge, it can also be referred to as bidirectional edge which means that edge can be in both the direction.


# Types of Graphs

- Undirected Graph
	- If there is an edge between vertex `u` and vertex `v` (`u—v`), you can traverse from `u` to `v` and also from `v` to `u`.
	- In other words, the connection is always **bidirectional**.
- Directed Graph or Directed Acyclic Graph (**DAG**)
	- It is a graph where all the edges are directed.
	- Each edge **has a direction**.
	- An edge from `u` to `v` (written as `u → v`) means you can move **only from `u` to `v`**, not the other way around unless there is a separate edge `v → u`.
	- So connections are **not automatically bidirectional** but they can be made bidirectional.
- Trees
	- Graph don't necessary means enclosed structure it could be **open structure** as well.
	- For anything to be graph , it needs nodes and edges.


# Terms related to Graph

- Cycle in a graph
	- There could be **multiple cycles** in a graph.
- Undirected cyclic graph
	- An **undirected cyclic graph** is an **undirected graph that contains at least one cycle**
- Directed cyclic graph
	- In this while finding a cycle one need to take care of direction as well.
	- If we start from a node and end at it via some path then it's called a directed cyclic graph.
	- Even having a bidirectional edge can convert an **acyclic** graph to a **cyclic** graph.
	![[Pasted image 20250822213201.png|200]]
	
- Path
	- It contains a lot of nodes and all of them are reachable.
	- Rules
		- While tracing the path one node **cannot appear twice**.
		- In a path there should be an edge between **adjacent nodes**.
		![[Pasted image 20250822213937.png|300]]
- Degrees in undirected Graph
	- Degree is number of edges attached to node in case of undirected graph.
	- Property of Degree:
		- Total degree of a graph  = 2 x Total no. of edges of a graph,   bcz every edge is connected to two vertices.
		![[Pasted image 20250822214455.png|400]]
- Degrees in directed graph
	- Degree is the number of edges that goes in and out of a node in case of directed graph. 
	-  Two sub category of degree:
		- In degree of node
			- It is number of incoming edges.
		- Out degree of node
			- It is number of outgoing edges.
			
		![[Pasted image 20250822214826.png|300]]
- Edge Weight
	- These  are weights assigned to edges.
	- If no weight is assigned then consider the weight to be 1.
	![[Pasted image 20250822214952.png|300]]


# How to store Graph

- You will be given two inputs n & m where n is number of nodes and m is number of edges.
- Then you will be given m (edges) lines of input of pair of numbers. Here each pair denotes adjacent vertices of an edge.
- In general n is always constant but m can be more than n as there could be multiple connections among the nodes.
- **Two ways** to store all the above data to form a graph:
	- Matrix Way
		- It is also called adjacency matrix.
		- Define a matrix of size n+1 like matrix\[n+1]\[n+1].
		- Space complexity is O(n²).
		![[Pasted image 20250822220254.png|400]]
	- List Way
		- In this we create an array of list (dynamic in nature).
		- In case of one based indexing of graph size of this list is n+1.
		- Space complexity is  O(2\*m) or O(2E) in case of undirected graph.
		- Space complexity is O(m) or O(E) in case of directed graph.
		![[Pasted image 20250822221452.png|400]]
- To store data in **weighted graph**
	- In case of Adjacency Matrix approach  instead of marking edge with 1 , mark it with the provided weight.
	- In case of Adjacency List approach instead of storing edge in list , tweak the data structure to store pairs (edge, weight).

#### In C++
###### To store undirected graph

Using **Adjacency Matrix** 
```cpp
#include <iostream>
using namespace std;

int main() {
    int n,m;
    cin >> n >> m;
    int adj[n+1][n+1];
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u][v] = 1; 
        adj[v][u] = 1; // remove this line for directed graph
    }
    return 0;
}
```

Using **Adjacency List**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n,m;
    cin >> n >> m;
    vector<int> adj[n+1];
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u); // remove this line for directed graph
    }
    return 0;
}
```



#### In Java

###### To store undirected graph

Using **Adjacency Matrix**
- Easier to use
- Occupy resources
- 
```java
import java.util.Scanner;

public class AdjMatrix {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); // number of vertices
        int m = sc.nextInt(); // number of edges
        
        int[][] adj = new int[n + 1][n + 1];

        for (int i = 0; i < m; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();

            adj[u][v] = 1;
            adj[v][u] = 1; // remove this line for directed graph
        }
        sc.close();
    }
}
```


Using **Adjacency List**
```java
import java.util.*;

public class AdjList {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); // number of vertices
        int m = sc.nextInt(); // number of edges

        // adjacency list (1-based indexing)
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            adj.add(new ArrayList<>()); 
        }

        for (int i = 0; i < m; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();

            adj.get(u).add(v);
            adj.get(v).add(u); // remove this line for directed graph
        }
        sc.close();
    }
}
```



# What are Connected Component

- A graph can be disconnected as well based on the list of connected edges provided while creation of the graph.
- These disconnected portions of graph is called components.

![[Pasted image 20250822224548.png|400]]




# Insights about Traversals

- In case of components while you complete the traversal of one component you can't reach out to other components as they are not connected with the one you traversed.
- So for such scenarios we need to keep track of visited nodes and for that we are  always going to use visited array.
- To use visited array you will run a loop from 1 to n (number of nodes) and if any node is not visited you will call the traversal algorithm from that node.
	![[Pasted image 20250822225506.png|400]]


### Memoization in Graph Traversal

In classic problems like calculating Fibonacci numbers, **memoization** means storing the result of a function call so you don't have to compute it again.

In graph or grid traversal algorithms (like DFS and BFS), the concept is functionally the same, but we usually call it keeping a **"visited" set**. The goal is to avoid re-processing a node (or cell) that we have already seen. Without this, your algorithm could get stuck in an infinite loop or do an enormous amount of redundant work.

This visited array handles two things:
- It handles the cycles in a graph
- It handles multiple components in a graph.



# BFS vs DFS

### At a Glance: Comparison Table

| Feature                | Breadth-First Search (BFS)                                            | Depth-First Search (DFS)                                                       |
| ---------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **Traversal Strategy** | **Level-by-level**. Visits all neighbors before moving to next level. | **Goes deep**. Explores as far as possible along a branch before backtracking. |
| **Data Structure**     | **Queue** (FIFO: First-In, First-Out)                                 | **Stack** (LIFO: Last-In, First-Out). This is implicit in recursion.           |
| **Time Complexity**    | **O(V + E)**                                                          | **O(V + E)**                                                                   |
| **Space Complexity**   | **O(V)**                                                              | **O(V)** (but see important note below)                                        |
| **Optimal for...**     | **Finding the shortest path** (in unweighted graphs).                 | **Exploring all nodes**, checking for cycles, topological sorting.             |
| **Implementation**     | **Always iterative** (using a queue).                                 | **Iterative** (using a stack) or **Recursive** (using recursive stack)         |

### Summary: Which One to Choose?

| Choose BFS if...                                                       | Choose DFS if...                                                           |
| ---------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| You need the **shortest path** (in unweighted graphs).                 | You need to **visit every node** and memory is a concern for wide graphs.  |
| The graph is **very deep** but not too wide (e.g., a long chain).      | The graph is **very wide** (a DFS stack will be smaller than a BFS queue). |
| You are exploring a graph level-by-level (e.g., "friends of friends"). | You need to do **cycle detection** or **topological sorting**.             |

# Which has better space complexity

Of course. This is an excellent and very common interview question. The answer is nuanced.

**The short answer is: It depends on the structure of the graph. DFS _often_ has better practical space complexity, but its worst-case is the same as BFS: O(V).**

Here’s the detailed breakdown that you should use in an interview.

---

### The Core Difference: Strategy Dictates Space

The space complexity is determined by the data structure used to track the "frontier" of nodes to be explored.

- **BFS uses a Queue.** Its space is determined by the **width** of the graph.
    
- **DFS uses a Stack.** Its space is determined by the **depth** of the graph.
    

This leads to different best-case and worst-case scenarios.

### Analysis of Space Complexity

| Algorithm | Worst-Case Space Complexity | Reason for Worst-Case                                                                                                            | Best-Case Scenario                                                             |
| --------- | --------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **BFS**   | **O(V)**                    | A densely connected, wide graph (e.g., a "star" graph). The queue must hold an entire level, which could be nearly all vertices. | **O(1)** for an infinite chain, but typically **O(width)** for a "nice" graph. |
| **DFS**   | **O(V)**                    | A deep, narrow graph (e.g., a linked list). The stack must hold the entire path from the root to the deepest node.               | **O(depth)** for a balanced graph. Often much smaller than BFS's queue.        |

### Key Insight and Practical Advice

**In practice, for many real-world problems like web crawling or exploring large networks, DFS has a significant space advantage.**

- **Why?** Most real-world graphs (like the internet, social networks, or dependency trees) are **very wide but not very deep**.
    
- **BFS** would struggle because its queue would need to store a massive number of nodes from the same level, quickly consuming gigabytes of memory.
    
- **DFS** would excel because it only needs to store the path it's currently exploring. Even in a graph with billions of nodes, the _depth_ of the path might only be 10 or 20 clicks. This uses dramatically less memory.
    

**Conversely, you would never use DFS on a very deep graph (like a long linked list) if you could use BFS, as BFS's queue would remain tiny.**

### How to Answer in an Interview

Structure your answer like this:

1. **State the official complexity:** "Both BFS and DFS have a worst-case space complexity of **O(V)**, as in the worst case, both their underlying data structures might need to store all vertices."
    
2. **Explain the difference:** "However, the _reason_ for this complexity is different and has major practical implications:
    
    - **BFS** uses a queue. Its memory usage is tied to the **breadth** of the graph. Its worst case is a very wide, shallow graph (like a star network).
        
    - **DFS** uses a stack (either explicit or the call stack). Its memory usage is tied to the **depth** of the graph. Its worst case is a very deep, narrow graph (like a linked list)."
        
3. **Give the practical conclusion:** "Therefore, for problems involving wide, bushy graphs—which are very common—**DFS is usually the better choice for space efficiency**. For problems involving finding the shortest path or traversing deep graphs, BFS might be more efficient."
    
4. **Use an example:** "For instance, if I were building a web crawler, the internet is immensely wide. Using BFS would cause the queue to grow uncontrollably. Using DFS would be far more memory-efficient as it only stores the chain of links leading to the current page."