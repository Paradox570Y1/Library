![[Pasted image 20250808211501.png]]
![[Pasted image 20250808213033.png]]

![[Pasted image 20250808213038.png]]

![[Pasted image 20250808213042.png]]



https://docs.google.com/document/d/1wT_s1v5J3yDw1KchwJbGtD5SdtUImHHOwcnSwbLV8C0/edit?tab=t.9drac2ft4ex7

#1
https://leetcode.com/problems/merge-sorted-array/submissions/1771633923/
#2
https://leetcode.com/problems/can-i-win/submissions/1771657318/
---


![[Pasted image 20250922202411.png]]

![[Pasted image 20250922202534.png]]


![[Pasted image 20250922202644.png]]![[Pasted image 20250922203451.png]]


https://docs.google.com/document/d/1gp1T4BL1uTsPF96dppUGsrzfoqhvF3kPq9teFBCdgtY/edit?tab=t.0



---
# LRU Caching

- Fault with caching
	- It provides faster access and used everywhere like CDN network, streaming services.
	- System Design also use caching and one popular one is Redis cache
	- It comes with a con that it introduce inconsistent behavior in the database.
	- Example: when you unfollow somebody but still you are able to see that persons profile for few seconds.
	- There are two categories in caching : hits & miss
		- A unique key is used to keep track if data is in cache or not.
	- Matrix for cache
		- If lakhs of request came then how many were hits and how many were miss. That gives a matrix.
			- This could be bad in case their are frequent data updates.
			- In case we are using dynamo DB then if hits were 99% then we need to make fewer calls to dynamo DB which reduces the cost of service as dynamo DB charges per call.
	- In caching if you have 100GB data then you can use 4 GB faster memory like ram to cache that data.

---

# Cache System
- LRU - Least Recently Used
- Map - K : V
- Maximum Capacity -> 10/ 10000/ 1000000...
- One of it's type is Client Side Cache.
- The problem with it that it  stale data might accumulate.
	- One way to prevent it is TTL using which we provide certain time limit to the existence of data.
- Consistency can be compromised with cache as user is the one to store the data.
- Two types of cache based on it's distribution:
	- In - memory cache
	- Distributed Cache
		- Imagine it like a service where common cache space is accessible by multiple machines.
![[Pasted image 20251104192107.png|400]]


> Look Up : Time Series question on leetcode 981


---

# Core Topic

# Graphs

implement all paths in acyclic graph
```java
import java.util.HashMap;
import java.util.Set;
import java.util.HashSet;
import java.util.List;
import java.util.ArrayList;

class Graph {
  private Map<Integer, Set<Integer>> edgeMap;

  Graph() {
    edgeMap = new HashMap<>();
  }

  void addEdge(int a, int b) {
    if (!edgeMap.containsKey(a)) {
      edgeMap.put(a, new HashSet<>());
    }
    edgeMap.computeIfAbsent(a, e -> new HashSet<>()).add(b);
    edgeMap.computeIfAbsent(b, e -> new HashSet<>()).add(a);
  }

  List<String> getAllPaths(int startNode) {
    Set<Integer> vis = new HashSet<>();
    vis.add(startNode);
    List<String> res = new ArrayList<>();
    dfs(vis, res, new StringBuilder(startNode), startNode);
    return res;
  }

  private void dfs(Set<Integer> vis,List<String> res, StringBuilder str, int node) {
    boolean lastNode = true;
    for (int child : edgeMap.get(node)) {
      if(!vis.contains(child)) {
        vis.add(child);
        str.append(child);
        dfs(vis, res, str, child);
        lastNode = false;
        str.setLength(str.length()-1);
      }
    }
    if(lastNode) res.add(str.toString());
  }

  public static void main(String[] args) {
    Graph g = new Graph();
    g.addEdge(1, 2);
    g.addEdge(2, 5);
    g.addEdge(2, 3);
    g.addEdge(3, 6);
    g.addEdge(3, 7);
    g.addEdge(3, 4);

    System.out.println(g.getAllPaths(1));
  }
}
```


# Dijkstra Algorithm

![[Pasted image 20251124192735.png|400]]

![[Pasted image 20251124193139.png|400]]


![[Pasted image 20251124200901.png|400]]

![[Pasted image 20251124194035.png|400]]

Time Complexity of Dijkstra

![[Pasted image 20251125192517.png]]

![[Pasted image 20251125192550.png|200]]

![[Pasted image 20251125193609.png]]
![[Pasted image 20251125193627.png]]


# Floyd War shell Algorithm

![[Pasted image 20251208193349.png]]



Homework problems 
LeetCode 1334 — Find City With Smallest Number of Neighbors Within Threshold LeetCode 2642 — Design Graph With Shortest Path Calculator 
LeetCode 399 — Evaluate Division LeetCode 
1615 — Maximal Network Rank

# Disjoint Sets

![[Pasted image 20251209192344.png|300]]
![[Pasted image 20251209192524.png|400]]

![[Pasted image 20251209193209.png]]

![[Pasted image 20251209193601.png]]
This is called compression of path , while finding the parent it also makes the connection of other nodes direct to the parent. This is also the reason why the time complexity of this is very complex.(4 alpha)


Below code will not work as it misses a critical step of updating the parents of smaller kingdom to parents of bigger kingdom
![[Pasted image 20251209194522.png|300]]

![[Pasted image 20251209194940.png|300]]


[[684. Redundant Connection]]
[[Number Of Islands 2]]

Now lets talk about if a graph has both strongly connected component and not strongly connected component then how to find SCC

![[Pasted image 20251215191441.png|340]]

- SCC in a graph can be found using Kosaraju algorithm or Tarjan algorithm.
- Finding SCC helps in finding cycle.
- Even in google maps if there are SCC which means their is a cycle then that is made into a single component and a node is is used to lead to that sub graph. So, it is used to simply the node structure or decrease the density of a graph.
- It's a simplification of graph at the end of the day.
![[Pasted image 20251215191913.png|400]]

# Kosaraju Algorithm
It uses DFS
- Based on the finish time during DFS, we put nodes back in Stack.
- Reverse the graph
- DFS on stack order (gives you Strongly Connected Component)


```java
import java.util.*;

public class StronglyConnectedComponents {

    private int V;
    private List<Integer>[] graph;
    private List<Integer>[] reverseGraph;

    public StronglyConnectedComponents(int V) {
        this.V = V;
        graph = new ArrayList[V];
        reverseGraph = new ArrayList[V];

        for (int i = 0; i < V; i++) {
            graph[i] = new ArrayList<>();
            reverseGraph[i] = new ArrayList<>();
        }
    }

    // Add edge u -> v
    public void addEdge(int u, int v) {
        graph[u].add(v);
        reverseGraph[v].add(u); // reverse edge
    }

    // Step 1: DFS to fill stack by finish time
    private void fillOrder(int node, boolean[] visited, Stack<Integer> stack) {
        // Complete this.
	visited[node] = true;
	for (int child : graph[node]) {
	  if (!visited[child]) {
	    fillOrder(child, visited, stack);
	  }
	}
	stack.push(node);
    }

    // Step 2: DFS on reversed graph
    private void dfsOnReverse(int node, boolean[] visited, List<Integer> component) {
        // Complete this.
	visited[node] = true;
	component.add(node);
	for (int child : reverseGraph[node]) {
	  if (!visited[child]) {
	    dfsOnReverse(child, visited, component);
	  }
	}
    }

    // Main function to find SCCs
    public List<List<Integer>> getSCCs() {
        // Complete this.
	Stack<Integer> stack = new Stack<>();
	boolean[] visited = new boolean[V];
	for (int i = 0; i < V; i++) {
	  if (!visited[i]) {
	    fillOrder(i, visited, stack);
	  }
	}

	List<List<Integer>> scc = new ArrayList<>();
	visited = new boolean[V];
	while (!stack.isEmpty()) {
	  int node = stack.pop();
	  if (!visited[node]) {
	    List<Integer> component = new ArrayList<>();
	    dfsOnReverse(node, visited, component);
	    if (component.size() > 0) {
	      scc.add(new ArrayList<>(component));
	    }
	  }
	}

	return scc;
    }

    // Driver
    public static void main(String[] args) {
        StronglyConnectedComponents scc = new StronglyConnectedComponents(5);

        scc.addEdge(1, 0);
        scc.addEdge(0, 2);
        scc.addEdge(2, 1);
        scc.addEdge(0, 3);
        scc.addEdge(3, 4);

        List<List<Integer>> result = scc.getSCCs();

        System.out.println("Strongly Connected Components:");
        for (List<Integer> comp : result) {
            System.out.println(comp);
        }
    }
}

```


# Segment Trees
- Used to find answers on range.

#### Prefix Sum

![[Pasted image 20260105191212.png|200]]
- Here if we want sum of numbers from 2-4 range then we will subtract prefix sum at 1 from prefix sum at 3.

- Segment tree is expansion of trees which are stored as array.
- So size of seg trees are generally taken 4 times.

![[Pasted image 20260105192401.png|300]]

![[Pasted image 20260105192802.png|400]]

- In segment tree index number represents for which range it is valid.
![[Pasted image 20260105194326.png|300]]

- first condition exits if queried range is before or after our tree range.
- if seg tree range of some idx is completely in range of query where query range can be bigger as well but still we return the sum at that idx bcz that part lies in the queried range although may not be complete.
![[Pasted image 20260105195308.png|300]]

So, we are breaking down the range and return sum for valid ranges and 0 for non valid ranges and adding up all to get that range sum. This take O(log n) time to find the range sum. On comparison with prefix method just take O(1) to get the range sum.
# Advantage of segment tree
- In case you want to find a range when data is dynamically getting updated then segment trees is better as in normal prefix way if value at index changes then it take O(n) time to update rest of the values in prefix array but in case of seg tree it will take O(log n) to update rest of seg tree.

[[303. Range Sum Query - Immutable]]

Home Work
![[Pasted image 20260105203327.png|100]]

[[2080. Range Frequency Queries]]

# Spring boot

- We need something to expose APIs.
- XML based modelling - SOAP (API request and response structure)
- Backend API is essential to fetch data from database, even to data from  external backend of some other services as well
- You need to make your backend server as well to allow curl commands.
- Spring Framework has documentation about how to create own server , do XML based modelling , setup dependencies etc.

- So to prevent these hassle , Spring boot came into picture.
- It will provide you backend server which will self manage configuration, dependencies, tomcat etc.
- It executes all SOLID Principles that we have-> inversion of control, open close etc.

![[Pasted image 20260209191735.png|200]]
- It uses concept of beans - each class object is made globally and these objects are meant to be used again and again. **Everything that interacts in Spring Boot are beans**.
- Creation will be handled by itself when application startups.
- Here `Autowired`is annotation used to signify that you don't need to create a new engine , in memory there are objects of engine which already exist , use them directly.
- It kind of reuses already existing objects.
- Dependency injection means that if while creating a class it needs dependencies like other classes then using annotation it will automatically inject the dependencies from the memory.
![[Pasted image 20260209191755.png|200]]
![[Pasted image 20260209193240.png|300]]
![[Pasted image 20260209193511.png|300]]
- here why need multiple objects of C (controller layer), S (service layer), R (repository layer) if they are doing the same thing of reading data from Database, instead we can make some beans of C, S, R which will used for all the requests instead of creating a new one.


#Layers

1. Controller layer - Stores routing info
2. Service layer - Application logic exist here
3. Repository layer - It is used to extract data from DB, IMD (In-Memory Database), map etc. (DOW)
4. Database layer - data exists here


Main method has annotation `@StartApplication` which starts the spring boot , then it creates DAG dependency graph based on topological order of dependencies of beans also identifies cyclic dependencies as well. Then initializes the beans accordingly. Then start executing application layer by layer.

There are many package manager that can be used in spring boot but most used is Maven.
![[Pasted image 20260209200841.png]]


### How does multi layered implementation  works
If there are multiple implementations of the same class then use `@Qualifiers`which kind of tags each implementation of that class then we perform dependency injection on.