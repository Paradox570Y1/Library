- It is also used to find the minimum spanning tree.
- In this we make use of Disjoint Set data structure.
- Two ways to implement it is union by size (number of nodes in tree) and union by rank(height of tree).
- The approaches offer same time complexity , union by rank maybe little more cache friendly as rank of tree will always be limited to log n. while number of nodes in size can count upto higher.
# Process
- Sort all edges according to weights.



# Implementation
TC-> O(E log E) + O(2 x 4 x α(V) x E)
Time complexity of Kruskal algorithm is O(E α(V)) ≈ O(E), excluding the sorting time complexity here


Final:
- **Time Complexity:** `O(E log E)`
- **Space Complexity:** `O(V + E)`
```java
class Solution {
    class DisjointSet{
        int[] parent, size;
        DisjointSet(int n) {
            parent = new int[n];
            size =new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
                size[i] = 1;
            }
        }
        
        public int findUParent(int node) {
            if (node == parent[node]) return node;
            return parent[node] = findUParent(parent[node]);
        }
        
        public void Union(int u, int v) {
            int up = findUParent(u);
            int vp = findUParent(v);
            
            if (size[up] < size[vp]) {
                parent[up] = vp;
                size[vp] += size[up];
            } else {
                parent[vp] = up;
                size[up] += size[vp];
            }
        }
    }
    public int spanningTree(int V, int[][] edges) {
        // code here
        Arrays.sort(edges, (a, b) -> a[2] - b[2]);
        DisjointSet ds = new DisjointSet(V);
        
        int sum = 0;
        
        for (int edge[] : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];
            if (ds.findUParent(u) != ds.findUParent(v)) {
                ds.Union(u, v);
                sum += w;
            }
        }
        return sum;
    }
}

```

OR

```java
class Solution {
    class DisjointSet {
        int[] parent, rank;

        DisjointSet(int n) {
            parent = new int[n];
            rank = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
                rank[i] = 0;   // rank starts from 0
            }
        }

        public int findUParent(int node) {
            if (node == parent[node]) return node;
            return parent[node] = findUParent(parent[node]); // path compression
        }

        public void Union(int u, int v) {
            int up = findUParent(u);
            int vp = findUParent(v);

            if (up == vp) return;

            // union by rank
            if (rank[up] < rank[vp]) {
                parent[up] = vp;
            } 
            else if (rank[up] > rank[vp]) {
                parent[vp] = up;
            } 
            else {
                // ranks equal
                parent[vp] = up;
                rank[up]++;   // rank increases ONLY here
            }
        }
    }

    public int spanningTree(int V, int[][] edges) {
        Arrays.sort(edges, (a, b) -> a[2] - b[2]);

        DisjointSet ds = new DisjointSet(V);
        int sum = 0;

        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int w = edge[2];

            if (ds.findUParent(u) != ds.findUParent(v)) {
                ds.Union(u, v);
                sum += w;
            }
        }
        return sum;
    }
}

```