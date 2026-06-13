[Link](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

Given a Directed Graph with **V** vertices (Numbered from **0** to **V-1**) and **E** edges, check whether it contains any **cycle** or not.  
The graph is represented as a 2D vector **edges[][]**, where each entry **edges[i] = [u, v]** denotes an edge from verticex **u** to **v.**

**Examples:**

**Input:** V = 4, edges[][] = `[[0, 1], [0, 2], [1, 2], [2, 0], [2, 3]]`
![|350](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700218/Web/Other/blobid0_1744197297.jpg)
**Output:** true
**Explanation**: The diagram clearly shows a cycle 0 → 2 → 0

**Input:** V = 4, edges[][] = [[0, 1], [0, 2], [1, 2], [2, 3]
![|350](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700218/Web/Other/blobid1_1744197327.jpg)  
**Output:** false
**Explanation**: no cycle in the graph

**Constraints:**  
1 ≤ V, E ≤ 105  
u ≠ v


# Using DFS

```java
class Solution {
    public boolean isCyclic(int V, int[][] edges) {
        // code here
        boolean vis[] = new boolean[V];
        boolean visPath[] = new boolean[V];
        
        List<List<Integer>> adjList  = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] edge:edges) {
            adjList.get(edge[0]).add(edge[1]);
        }
        
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                if (isCyclic(adjList, i, vis, visPath)) return true;
            }
        }
        return false;
    }
    
    private boolean isCyclic(List<List<Integer>> adjList, int node, boolean[] vis, boolean[] visPath) {
        vis[node] = true;
        visPath[node] = true;
        for (int next:adjList.get(node)) {
            if (!vis[next] && isCyclic(adjList, next, vis, visPath)) return true;
            else if(visPath[next]) {
                return true;
            }
        }
        visPath[node] = false;
        return false;
    }
}
```


# Using BFS

```java
class Solution {
    public boolean isCyclic(int V, int[][] edges) {
        // code here
        int[] inorder = new int[V];
        
        List<List<Integer>> adjList = new ArrayList<>();
        
        for(int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] edge : edges) {
            adjList.get(edge[0]).add(edge[1]);
            inorder[edge[1]]++;
        }
        
        Queue<Integer> queue = new LinkedList<>();
        int count = 0;
        
        for (int i = 0; i < V; i++) {
            if (inorder[i] == 0) {
                queue.offer(i);
            }
        }
        
        while (!queue.isEmpty()) {
            int node = queue.poll();
            count++;
            for (int next: adjList.get(node)) {
                inorder[next]--;
                if (inorder[next] == 0) queue.offer(next);
            }
        }
        
        return (count != V);
    }
}
```