# Breadth First Search

![[Pasted image 20250825111632.png|400]]
![[Pasted image 20250825111821.png|400]]


Given a **connected undirected graph** containing **V** vertices, represented by a 2-d adjacency list **`adj[][]`**, where each `adj[i]` represents the list of vertices connected to vertex `i`. Perform a **Breadth First Search (BFS)** traversal starting from vertex `0`, visiting vertices from left to right according to the given adjacency list, and return a list containing the BFS traversal of the graph.

**Note:** Do traverse in the **same order** as they are in the given **adjacency list**.

**Examples:**

**Input:** adj\[]\[] = `[[2, 3, 1], [0], [0, 4], [0], [2]]`  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700217/Web/Other/blobid0_1728648582.jpg)  
**Output:** [0, 2, 3, 1, 4]  
**Explanation:** Starting from 0, the BFS traversal will follow these steps:   
Visit 0 → Output: 0   
Visit 2 (first neighbor of 0) → Output: 0, 2   
Visit 3 (next neighbor of 0) → Output: 0, 2, 3   
Visit 1 (next neighbor of 0) → Output: 0, 2, 3,   
Visit 4 (neighbor of 2) → Final Output: 0, 2, 3, 1, 4

**Input:** adj\[]\[] = `[[1, 2], [0, 2], [0, 1, 3, 4], [2], [2]]`  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700217/Web/Other/blobid1_1728648604.jpg)  
**Output:** [0, 1, 2, 3, 4]  
**Explanation:** Starting from 0, the BFS traversal proceeds as follows:   
Visit 0 → Output: 0   
Visit 1 (the first neighbor of 0) → Output: 0, 1   
Visit 2 (the next neighbor of 0) → Output: 0, 1, 2   
Visit 3 (the first neighbor of 2 that hasn't been visited yet) → Output: 0, 1, 2, 3   
Visit 4 (the next neighbor of 2) → Final Output: 0, 1, 2, 3, 4

**Constraints:  
**1 ≤ V = adj.size() ≤ 104  
1 ≤ adj[i][j] ≤ 104


 TC -> O(V + E)
 SC -> O(V) + O(V)  for storing visited array
```java
class Solution {
    // Function to return Breadth First Search Traversal of given graph.
    public ArrayList<Integer> bfs(ArrayList<ArrayList<Integer>> adj) {
        // code here
        int n = adj.size();
        int vis[] = new int[n];
        Queue<Integer> queue = new LinkedList<>();
        vis[0] = 1;
        queue.offer(0);
        ArrayList<Integer> ans = new ArrayList<>();
        while(!queue.isEmpty()) {
            int node = queue.poll();
            ans.add(node);
            for (int cn: adj.get(node)) {
                if(vis[cn] == 0) 
                {
                    vis[cn] = 1;
                    queue.offer(cn);
                }
            }
        }
        return ans;
    }
}
```