[Link](https://www.geeksforgeeks.org/problems/number-of-islands/1)

### Number Of Islands

Difficulty: **Medium**Accuracy: **60.65%**Submissions: **65K+**Points: **4**Average Time: **30m**

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


# Rohit Sir's code

```java
// User function Template for Java

class Solution {

    class DSU {
        int parent[];
        int size[];
        int N;

        DSU(int N) {
            this.N = N;
            this.parent = new int[N];
            this.size = new int[N];

            for (int i = 0; i < N; i++) {
                size[i] = 1;
                parent[i] = i;
            }
        }

        public int findParent(int node) {
            if (parent[node] == node) {
                return node;
            }
            int masterParent = findParent(parent[node]);
            parent[node] = masterParent; // compression
            return masterParent;
        }


        public boolean union(int node1, int node2) {
            int masterParentOfNode1 = findParent(node1);
            int masterParentOfNode2 = findParent(node2);

            if (masterParentOfNode1 == masterParentOfNode2) {
                return false;
            }

            if (size[masterParentOfNode1] >= size[masterParentOfNode2]) {
                size[masterParentOfNode1] += size[masterParentOfNode2];
                parent[masterParentOfNode2] = masterParentOfNode1;
            } else {
                size[masterParentOfNode2] += size[masterParentOfNode1];
                parent[masterParentOfNode1] = masterParentOfNode2;
            }
            
            return true;
        }


    }
    
    public boolean isValid(int i , int j, int matrix[][], int rows, int cols) {
        if (i < 0 || j < 0 || i >= rows || j >= cols || matrix[i][j] == 0) {
            return false;
        }
        
        return true;
    }

    public List<Integer> numOfIslands(int rows, int cols, int[][] operators) {
        
        int N = rows * cols;
        int numberOfIslands = 0;
        List<Integer> ans = new ArrayList<>();
        
        DSU dsu = new DSU(N);
        int matrix[][] = new int[rows][cols];
        int dirs[][] = new int[][] {{0,1} , {0, -1}, {1, 0}, {-1, 0}};
        
        for (int[] operator : operators) {
            int i = operator[0];
            int j = operator[1];
            
            if (matrix[i][j] == 1) {
                ans.add(numberOfIslands);
                continue;
            } else {
                matrix[i][j] = 1;
                numberOfIslands++;
            }
            
            int node1 = cols * i + j;
            
            for (int dir[] : dirs) {
                int neighbourI = i + dir[0];
                int neighbourJ = j + dir[1];
                
                if (isValid(neighbourI, neighbourJ, matrix, rows, cols)) {
                    int node2 = cols * neighbourI + neighbourJ;
                    
                    if (dsu.union(node1, node2)) {
                        numberOfIslands--;
                    }
                }
            }
            
            ans.add(numberOfIslands);
        }
        
        return ans;
    }
}
```


# Mine Code T-T

```java
// User function Template for Java

class Solution {
    class DSU{
        int[][][] parent;
        int[][] size;
        int N;
        DSU(int n, int m) {
            this.N = n*m;
            parent = new int[n][m][2];
            size = new int[n][m];
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    size[i][j] = 1;
                    parent[i][j][0] = i;
                    parent[i][j][1] = j;
                }
            }
        }
        
        private boolean cmp(int[] node1, int[] node2) {
            return (node1[0] == node2[0]) && (node1[1] == node2[1]);
        }
        
        public int[] findParent(int[] node) {
            int x = node[0];
            int y = node[1];
            if (cmp(parent[x][y], node)) return node;
            int[] masterParent = findParent(parent[x][y]);
            parent[x][y] = masterParent;
            return masterParent;
        }
        
        public boolean union(int[] node1, int[] node2) {
            int[] masterParent1 = findParent(node1);
            int[] masterParent2 = findParent(node2);
            if(cmp(masterParent1, masterParent2)) return false;
            if(size[masterParent1[0]][masterParent1[1]] >= size[masterParent2[0]][masterParent2[1]]) {
                size[masterParent1[0]][masterParent1[1]] += size[masterParent2[0]][masterParent2[1]];
                parent[masterParent2[0]][masterParent2[1]] = masterParent1;
            } else {
                size[masterParent2[0]][masterParent2[1]] += size[masterParent1[0]][masterParent1[1]];
                parent[masterParent1[0]][masterParent1[1]] = masterParent2;
            }
            return true;
        }
    }
    public List<Integer> numOfIslands(int rows, int cols, int[][] operators) {
        // Your code here
        DSU dsu = new DSU(rows, cols);
        int mat[][] = new int[rows][cols];
        int[][] dirs = {{0, 1}, {1, 0}, {-1, 0}, {0, -1}};
        int numberOfIslands = 0;
        List<Integer> list = new ArrayList<>();
        for (int node[] : operators) {
            int i = node[0];
            int j = node[1];
            if(mat[i][j] == 1) {
                list.add(numberOfIslands);
                continue;
            } else {
                mat[i][j] = 1;
                numberOfIslands++;
            }
            for (int[] dir : dirs) {
                int x = dir[0] + i;
                int y = dir[1] + j;
                if (x >= 0 && y >= 0 && x < rows && y < cols && mat[x][y] == 1) {
                    int neighbour[] = new int[]{x, y};
                    if(dsu.union(node, neighbour)) {
                        numberOfIslands--;
                    }
                }
            }
            list.add(numberOfIslands);
        }
        
        return list;
    }
}
```