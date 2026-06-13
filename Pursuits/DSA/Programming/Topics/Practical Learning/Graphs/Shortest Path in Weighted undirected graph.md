[Link](https://www.geeksforgeeks.org/problems/shortest-path-in-weighted-undirected-graph/1)

You are given a weighted undirected graph having **n** vertices numbered from **1 to n** and **m** edges along with their weights. Find the **shortest** **weight** **path** between the vertex 1 and the vertex **n**,  if there exists a path, and return a list of integers whose first element is the **weight** of the path, and the rest consist of the nodes on that path. If no path exists, then return a list containing a single element **-1**.

The input list of edges is as follows - **{a, b, w}**, denoting there is an edge between **a** and **b**, and **w** is the weight of that edge.

**_Note:_** The driver code here will first check if the weight of the path returned is **equal** to the **sum** of the weights along the nodes on that path, if **equal** it will output the weight of the path, else **-2**. In case the list contains only a single element (**-1**) it will simply output **-1**. 

**Examples :**

**Input:** n = 5, m= 6, edges = `[[1, 2, 2], [2, 5, 5], [2, 3, 4], [1, 4, 1], [4, 3, 3], [3, 5, 1]]`
**Output:** 5
**Explanation:** Shortest path from 1 to n is by the path 1 4 3 5 whose weight is 5. 

**Input:** n = 2, m= 1, edges = `[[1, 2, 2]]`
**Output:** 2
**Explanation:** Shortest path from 1 to 2 is by the path 1 2 whose weight is 2. 

**Input:** n = 2, m= 0, edges = \[ ]
**Output:** -1
**Explanation:** Since there are no edges, so no answer is possible.

**Expected Time Complexity:** O(m* log(n))  
**Expected Space Complexity:** O(n+m)

**Constraint:**  
2 <= n <= 106  
0 <= m <= 106  
1 <= a, b <= n  
1 <= w <= 105



# Using Priority Queue for Dijkstra's Algo

- In this question we want the order in which we should visit node to get the smallest distance.

```java
class Solution {
    public List<Integer> shortestPath(int n, int m, int edges[][]) {
        //  Code Here.
        List<List<int[]>> adjList = new ArrayList<>();
        
        for (int i = 0; i <= n; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            adjList.get(u).add(new int[]{v, w});
            adjList.get(v).add(new int[]{u, w});
        }
        
        PriorityQueue<int[]> minHeap = new PriorityQueue<>(new Comparator<int[]>() {
            public int compare(int[] a, int b[]) {
                if (a[0] != b[0]) return Integer.compare(a[0], b[0]);
                return Integer.compare(a[1], b[1]);
            }
        });
        
        int dist[] = new int[n+1];
        int parent[] = new int[n+1];
        
        for (int i = 0; i <= n; i++) {
            dist[i] = (int) 1e9;
            parent[i] = i;
        }
        
        minHeap.offer(new int[]{0, 1});
        dist[1] = 0;
        
        while (!minHeap.isEmpty()) {
            int[] node = minHeap.poll();
            int u = node[1];
            int du = node[0];
            for (int[] next : adjList.get(u)) {
                int v = next[0];
                int dv = next[1];
                if (du + dv < dist[v]) {
                    dist[v] = du + dv;
                    parent[v] = u;
                    minHeap.offer(new int[]{du + dv, v});
                }
            }
        }
        
        for (int i = 0; i <= n; i++) {
            if (dist[i] == (int) 1e9) {
                dist[i] = -1;
            }
        }
       
        
        List<Integer> path = new ArrayList<>();
        int node = n;
        while (parent[node] != node) {
            path.add(node);
            node = parent[node];
        }
        path.add(1);
        Collections.reverse(path);
        
        List<Integer> result = new ArrayList<>();
        result.add(dist[n]);
        result.addAll(path);
        return result;
    }
}
```


OR

```java
class Solution {
    class Pair implements Comparable<Pair> {
        int v;
        int dist;
        Pair(int v, int w) {
            this.v = v;
            this.dist = w;
        }
        @Override
        public int compareTo(Pair other) {
            if (this.dist != other.dist) return Integer.compare(this.dist, other.dist);
            return Integer.compare(this.v, other.v);
        }
    }
    public List<Integer> shortestPath(int n, int m, int edges[][]) {
        //  Code Here.
        List<List<Pair>> graph = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            graph.get(u).add(new Pair(v, w));
            graph.get(v).add(new Pair(u, w));
        }
        
        PriorityQueue<Pair> pq = new PriorityQueue<>();
        int[] dist = new int[n+1];
        int[] parent = new int[n+1];
        Arrays.fill(dist, (int)1e9);
        dist[1] = 0;
        pq.offer(new Pair(1, 0));
        
        while (!pq.isEmpty()) {
            Pair node = pq.poll();
            int u = node.v;
            int du = node.dist;
            if (du > dist[u]) continue;
            for (Pair next : graph.get(u)) {
                int v = next.v;
                int w = next.dist;
                if (du + w < dist[v]) {
                    dist[v] = du + w;
                    parent[v] = u;
                    pq.offer(new Pair(v, dist[v]));
                }
            }
        }
        for (int v = 1; v <= n; v++) {
            if (dist[v] == (int) 1e9) dist[v] = -1;
        }
        if (dist[n] == -1) return new ArrayList<>(List.of(-1));
        int i = n;
        List<Integer> res = new ArrayList<>();
        res.add(dist[n]);
        res.add(n);
        while (parent[i] != 0) {
            res.add(parent[i]);
            i = parent[i];
        }
        return res;
    }
}
```


For some reason path from 1 to n or n to 1 both works fine in result.