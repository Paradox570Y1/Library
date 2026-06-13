[Link](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1)

Difficulty: **Medium**Accuracy: **30.13%**Submissions: **631K+**Points: **4**Average Time: **20m**

Given an **undirected graph** with **V** vertices and **E** edges, represented as a 2D vector **edges[][]**, where each entry **edges[i] = [u, v]** denotes an edge between vertices **u** and **v**, determine whether the graph contains a **cycle** or not. The graph can have multiple component.![](file:///C:/Users/Mukul%20kumar/Desktop/GFG_PIC.JPG)

**Examples:**

**Input:** V = 4, E = 4, edges[][] = `[[0, 1], [0, 2], [1, 2], [2, 3]]`
**Output:** true
**Explanation:** 
![|200](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891735/Web/Other/blobid1_1743510240.jpg)   
1 -> 2 -> 0 -> 1 is a cycle.

**Input:** V = 4, E = 3, edges[][] = `[[0, 1], [1, 2], [2, 3]]`
**Output:** false
**Explanation:** 
![|200](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891735/Web/Other/blobid2_1743510254.jpg)   
No cycle in the graph.

**Constraints:  
**1 ≤ V ≤ 105  
1 ≤ E = edges.size() ≤ 105


> NOTE: Instead of returning true if you increment the count then the final count divide by 2 will give you the number of cycles.

- In Undirected graph if  a node points to already visited node which is not it's parent then there is a cycle in graph.
# Using BFS
![[Pasted image 20250827002838.png|300]]
```java
class Solution {
    class Node{
        int prev;
        int val;
        Node(int val, int prev) {
            this.val = val;
            this.prev = prev;
        }
    }
    public boolean isCycle(int V, int[][] edges) {
        // Code here
        boolean vis[] = new boolean[V];
        ArrayList<ArrayList<Integer>> matrix = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            matrix.add(new ArrayList<>());
        }
        for (int i = 0; i < edges.length; i++) {
            matrix.get(edges[i][0]).add(edges[i][1]);
            matrix.get(edges[i][1]).add(edges[i][0]);
        }
        for (int i = 0; i < V; i++) {
            if(!vis[i]) {
                if(detectCycle(matrix, i, vis)) return true;
            }
        }
        return false;
    }
    private boolean detectCycle(ArrayList<ArrayList<Integer>> adj, int node, boolean[] vis) {
        Queue<Node> queue = new LinkedList<>();
        queue.offer(new Node(node, -1));
        vis[node] = true;
        while(!queue.isEmpty()) {
            Node cur = queue.poll();
            for (int i = 0; i < adj.get(cur.val).size(); i++) {
                int val = adj.get(cur.val).get(i);
                if (!vis[val]) {
                    vis[val] = true;
                    queue.offer(new Node(val, cur.val));
                }
                else if(val != cur.prev) {
                    return true;
                }
            }
        }
        return false;
    }
}
```


# Using DFS
![[Pasted image 20250827004113.png|300]]
```java
class Solution {
    public boolean isCycle(int V, int[][] edges) {
        // Code here
        boolean vis[] = new boolean[V];
        ArrayList<ArrayList<Integer>> matrix = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            matrix.add(new ArrayList<>());
        }
        for (int i = 0; i < edges.length; i++) {
            matrix.get(edges[i][0]).add(edges[i][1]);
            matrix.get(edges[i][1]).add(edges[i][0]);
        }
        for (int i = 0; i < V; i++) {
            if(!vis[i]) {
                if(detectCycle(matrix, i, -1, vis)) return true;
            }
        }
        return false;
    }
    private boolean detectCycle(ArrayList<ArrayList<Integer>> adj, int cur, int parent, boolean[] vis) {
       vis[cur] = true;
       for (int i = 0; i < adj.get(cur).size(); i++) {
           int val = adj.get(cur).get(i);
           if (!vis[val]) {
               vis[val] = true;
               if(detectCycle(adj, val, cur, vis)) {
                   return true;
               }
           }
           else if(val != parent) {
               return true;
           }
       }
       return false;
    }
}
```

![[Pasted image 20250827003937.png|400]]
