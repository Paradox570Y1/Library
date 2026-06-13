# What is SCC ?
- It stands for `Strongly Connected Components`.
- SCC are only valid for directed graphs.
- When every pair of vertex is reachable by each other within a component then that is called SCC.

![[Pasted image 20250923124036.png|300]]

**Q. Types of Question asked?**
- Figure out number of SCC.
- Print the SCC.

# Thought Process
- Below is the way SSC are connected
	- ![[Pasted image 20250923124343.png|300]]
- What if we reverse connections between SSC.
	![[Pasted image 20250923124418.png|300]]
	- So now what we observed is if we visit all nodes in each components using DFS and arrive back on the starting node then that's a SCC.
- Since we don't know which edge to reverse so why not reverse all of them.
- But there is one more problem that  super starting point can be in any component like in above figure if that is in SCC4 after reversal then it's gonna visit all the components and we will not be able to define the boundary of each SSC.
- So to address above issue we are going to use starting time and finishing time concept.


# Steps to solve the problem
- Sort all the edges according to finishing time.
- Reverse the graph.
- Do a DFS.




[Link](https://www.geeksforgeeks.org/problems/strongly-connected-components-kosarajus-algo/1)

### Strongly Connected

Difficulty: **Medium**Accuracy: **50.61%**Submissions: **120K+**Points: **4**Average Time: **20m**

Given an adjacency list, **adj** of **D****irected Graph**, Find the number of strongly connected components in the graph.  
 

**Examples :**

**Input:** adj[][] = `[[2, 3], [0], [1], [4], []]`
![|300](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/700394/Web/Other/89b7c4e7-e03c-402f-b445-3e8815299af6_1685086635.png)
**Output:** 3
**Explanation**: We can clearly see that there are 3 Strongly Connected Components in the Graph.
![|300](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/700394/Web/Other/9f4ccc7f-8ad8-4f81-908a-01f27090ba5e_1685086635.png) 

**Input:** adj[][] = `[[1], [2], [0]]`
![](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/700394/Web/Other/8b9b3908-a800-4ffa-acaf-26cb760eac8e_1685086635.png)
**Output:** 1
**Explanation**: All of the nodes are connected to each other. So, there's only one SCC.  

**Input:** adj[][] = `[[1], []]`
**Output:** 2

**Constraints:**  
2<=adj.size()<=106  
0<=edges<=adj.size()-1


# Kosaraju Algorithm
TC -> O(2\*(V+E))
```java
class Solution {
    // Function to find number of strongly connected components in the graph.
    public int kosaraju(ArrayList<ArrayList<Integer>> adj) {
        // code here
        int V = adj.size();
        boolean[] vis = new boolean[V];
        Stack<Integer> st = new Stack<>();
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                dfs(adj, st, i, vis);
            }
        }
        ArrayList<ArrayList<Integer>> revAdj = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            revAdj.add(new ArrayList<>());
        }
        for (int u = 0; u < V; u++) {
            for (int v : adj.get(u)) {
                revAdj.get(v).add(u);
            }
        }
        int count = 0;
        vis = new boolean[V];
        while(!st.isEmpty()) {
            int node = st.pop();
            if(!vis[node]) {
                ssc(revAdj, node, vis);
                count++;
            }
        }
        return count;
    }
    private void dfs(ArrayList<ArrayList<Integer>> adj, Stack<Integer> st, int node, boolean[] vis) {
        vis[node] = true;
        for (int child : adj.get(node)) {
            if (!vis[child]) {
                dfs(adj, st, child, vis);
            }
        }
        st.push(node);
    }
    
    private void ssc(ArrayList<ArrayList<Integer>> adj, int node, boolean[] vis) {
        vis[node] = true;
        for (int child : adj.get(node)) {
            if (!vis[child]) {
                ssc(adj, child, vis);
            }
        }
    } 
}
```

OR





# Using Tarjan algorithm

```java
class Solution {
    // Function to find number of strongly connected components in the graph.
    private int timer;
    private int count;
    public int kosaraju(ArrayList<ArrayList<Integer>> adj) {
        // code here
        int V = adj.size();
        int[] disc = new int[V];
        int[] low = new int[V];
        Arrays.fill(disc, -1);
        Arrays.fill(low, -1);
        boolean[] inSt = new boolean[V];
        timer = 0;
        count = 0;
        for (int i = 0; i < V; i++) {
            if (disc[i] == -1) {
                tarjan(adj, i, disc, low, new Stack<>(), inSt);
            }
        }
        return count;
    }
    private void tarjan(ArrayList<ArrayList<Integer>> adj, int u, int[] disc, int[] low, Stack<Integer> st, boolean[] inSt) {
        disc[u] = low[u] = timer++;
        st.add(u);
        inSt[u] = true;
        for (int v : adj.get(u)) {
            if (disc[v] == -1) {
                tarjan(adj, v, disc, low, st, inSt);
                low[u] = Math.min(low[u], low[v]);
            } else if(inSt[v]) {
                low[u] = Math.min(low[u], disc[v]);
            }
        }
        
        if (disc[u] == low[u]) {
            while (true) {
                int v = st.pop();
                inSt[v] = false;
                if (v == u) break;
            }
            count++;
        }
    }
}
```

Theory with implementation of using Tarjan algo to get Strongly connected components

```java
// A recursive DFS based function used by getSCCs()
// u        -> The vertex to be visited next
// disc[]   -> Stores discovery times of visited vertices
// low[]    -> Earliest visited vertex that can be reached
//             from subtree rooted with current vertex
// st       -> Stack to store all active DFS vertices
// inSt[]   -> Boolean array to check whether a node is in stack
// timer    -> Global time counter for discovery times
// allSCCs  -> Stores all strongly connected components
function findSCC(u, adj, disc, low, inSt, st, timer, allSCCs) {

    // Initialize discovery time and low value
    timer.val++;
    disc[u] = low[u] = timer.val;

    // Push current vertex to stack and mark it as in stack
    st.push(u);
    inSt[u] = true;

    // Go through all vertices adjacent to this
    for (let v of adj[u]) {

        // If v is not visited yet, then recur for it
        // Case 1: Tree edge
        if (disc[v] === -1) {

            findSCC(v, adj, disc, low, inSt, st, timer, allSCCs);

            // Check if the subtree rooted with v has a
            // connection to one of the ancestors of u
            low[u] = Math.min(low[u], low[v]);
        }

        // Update low value of u only if v is still in stack
        // Case 2: Back edge (not cross edge)
        else if (inSt[v]) {
            low[u] = Math.min(low[u], disc[v]);
        }
    }

    // If u is head node of SCC, pop the stack and store the SCC
    if (low[u] === disc[u]) {

        let scc = [];

        // Pop all vertices from stack till u is found
        while (true) {

            let x = st.pop();
            inSt[x] = false;
            scc.push(x);

            if (x === u)
                break;
        }

        // Store one strongly connected component
        allSCCs.push(scc);
    }
}

function getSCCs(adj) {

    let n = adj.length;
    let disc = Array(n).fill(-1);
    let low = Array(n).fill(-1);
    let inSt = Array(n).fill(false);

    let st = [];
    let timer = { val: 0 };
    let allSCCs = [];

    // Call the recursive helper function to find SCCs
    // in DFS tree with vertex i
    for (let i = 0; i < n; i++) {

        if (disc[i] === -1) {
            findSCC(i, adj, disc, low, inSt, st, timer, allSCCs);
        }
    }

    return allSCCs;
}

// Driver Code
let adj = Array.from({ length: 6 }, () => []);

adj[0].push(1);
adj[1].push(2);
adj[2].push(0);
adj[2].push(3);
adj[3].push(4);
adj[4].push(3);
adj[4].push(5);

let sccs = getSCCs(adj);

console.log("Strongly Connected Components:");
for (let scc of sccs) {
    console.log(scc.join(" "));
}
```