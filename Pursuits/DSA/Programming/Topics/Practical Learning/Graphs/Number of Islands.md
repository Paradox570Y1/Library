[Link](https://www.geeksforgeeks.org/problems/number-of-islands/1)
### Number Of Islands

Difficulty: **Medium**Accuracy: **60.65%**Submissions: **62K+**Points: **4**Average Time: **30m**

You are given a **n,m** which means the row and column of the 2D matrix and an array of  size k denoting the number of operations. Matrix elements is 0 if there is water or 1 if there is land. Originally, the 2D matrix is all 0 which means there is no land in the matrix. The array has k operator(s) and each operator has two integer A[i][0], A[i][1] means that you can change the cell matrix[A[i][0]][A[i][1]] from sea to island. Return how many island are there in the matrix after each operation.You need to return an array of size **k**.  
**Note :** An island means group of 1s such that they share a common side.

**Example 1:**

**Input:** n = 4
m = 5
k = 4
A = {{1,1},{0,1},{3,3},{3,4}}

**Output:** 1 1 2 2
**Explanation:**
0.  00000
    00000
    00000
    00000
1.  00000
    01000
    00000
    00000
2.  01000
    01000
    00000
    00000
3.  01000
    01000
    00000
    00010
4.  01000
    01000
    00000
    00011

**Example 2:**

**Input:** n = 4
m = 5
k = 4
A = {{0,0},{1,1},{2,2},{3,3}}

**Output:** 1 2 3 4
**Explanation:**
0.  00000
    00000
    00000
    00000
1.  10000
    00000
    00000
    00000
2.  10000
    01000
    00000
    00000
3.  10000
    01000
    00100
    00000
4.  10000
    01000
    00100
    00010

**Your Task:**  
You don't need to read or print anything. Your task is to complete the function numOfIslands() which takes an integer n denoting no. of rows in the matrix, an integer m denoting the number of columns in the matrix and a 2D array of size k denoting  the number of operators.

**Expected Time Complexity:** O(m * n)  
**Expected Auxiliary Space:** O(m * n)

**Constraints:**

1 <= n,m <= 100  
1 <= k <= 1000

---
- Since we have to make connections dynamically, compatible algorithm is DSU(Disjoint Set Union).



# Using DSU

```java
// User function Template for Java

class Solution {
    class DisjointSet{
        int[] parent, size;
        DisjointSet(int n) {
            parent = new int[n];
            size = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
                size[i] = 1;
            }
        }
        
        public int findUParent(int node) {
            if (node == parent[node]) return node;
            return parent[node] = findUParent(parent[node]);
        }
        
        public void union(int u, int v) {
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
    public List<Integer> numOfIslands(int rows, int cols, int[][] operators) {
        // Your code here
        DisjointSet ds = new DisjointSet(rows * cols);
        List<Integer> ans = new ArrayList<>();
        boolean land[][] = new boolean[rows][cols];
        int count = 0;
        int[][] directions = {{0, -1}, {0, 1}, {-1, 0}, {1, 0}};
        
        for (int[] op : operators) {
            int row = op[0];
            int col = op[1];
            if (land[row][col]) {
                ans.add(count);
                continue;
            }
            land[row][col] = true;
            count++;
            for (int[] dir : directions) {
                int adjr = row + dir[0];
                int adjc = col + dir[1];
                if (isValid(adjr, adjc, rows, cols) && land[adjr][adjc]) {
                    int curNode = row * cols + col;
                    int adjNode = adjr * cols + adjc;
                    if(ds.findUParent(curNode) != ds.findUParent(adjNode)) {
                        count--;
                        ds.union(curNode, adjNode);
                    }
                }
            }
            ans.add(count);
        }
        return ans;
    }
    private boolean isValid(int adjr, int adjc, int rows, int cols) {
        return adjr >= 0 && adjr < rows && adjc >= 0 && adjc < cols;
    }
}
```


OR

```java
// User function Template for Java

class Solution {
    private int[] parent, size;
    private static int[][] dirs = {{-1, 0}, {0, -1}, {1, 0}, {0, 1}};
    private int cols;
    private int getNode(int i, int j) {
        return i * cols + j;
    }
    private int find(int node) {
        if (parent[node] == node) return node;
        return parent[node] = find(parent[node]);
    }
    private void union(int u, int v) {
        int pu = find(u);
        int pv = find(v);
        if (size[pu] < size[pv]) {
            parent[pu] = pv;
            size[pv] += size[pu];
        } else {
            parent[pv] = pu;
            size[pu] += size[pv];
        }
    }
    public List<Integer> numOfIslands(int rows, int cols, int[][] operators) {
        // Your code here
        this.cols = cols;
        int V = rows*cols;
        parent = new int[V];
        size = new int[V];
        for (int i = 0; i < V; i++) {
            parent[i] = i;
        }
        List<Integer> res = new ArrayList<>();
        int count = 0;
        for (int[] operator : operators) {
            int i = operator[0], j = operator[1];
            int u = getNode(i, j);
            if (size[u] == 0) {
                size[u] = 1;
                count++;
            }
            for (int[] dir : dirs) {
                int x = dir[0] + i;
                int y = dir[1] + j;
                if (x >= 0 && y >= 0 && x < rows && y < cols) {
                    int v = getNode(x, y);
                    if (size[v] > 0 && find(u) != find(v)) {
                        union(u, v);
                        count--;
                    }
                }
            }
            res.add(count);
        }
        
        
        return res;
    }
}
```