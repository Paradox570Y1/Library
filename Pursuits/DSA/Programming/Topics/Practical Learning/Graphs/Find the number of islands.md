[Link](https://www.geeksforgeeks.org/problems/find-the-number-of-islands/1)

Given a grid of size **n*m** (n is the number of rows and m is the number of columns in the grid) consisting of **'W'**s (Water) and **'L'**s (Land). Find the **number of islands**.  
  
**Note:** An island is either surrounded by water or the boundary of a grid and is formed by connecting adjacent lands **horizontally** or **vertically** or **diagonally** i.e., in all **8** directions.

**Examples:**

**Input:** grid[][] =` [['L', 'L', 'W', 'W', 'W'], ['W', 'L', 'W', 'W', 'L'], ['L', 'W', 'W', 'L', 'L'], ['W', 'W', 'W', 'W', 'W'], ['L', 'W', 'L', 'L', 'W']]`
**Output:** 4
**Explanation:**
The image below shows all the 4 islands in the grid.  
![|350](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891756/Web/Other/blobid1_1743509451.jpg) 

**Input:** grid[][] = `[['W', 'L', 'L', 'L', 'W', 'W', 'W'], ['W', 'W', 'L', 'L', 'W', 'L', 'W']]`
**Output:** 2
**Expanation:**
The image below shows 2 islands in the grid.  
![|350](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891756/Web/Other/blobid2_1743509488.jpg) 

**Constraints:**  
1 ≤ n, m ≤ 500  
grid[i][j] = {'L', 'W'}


# Using DFS

```java
class Solution {
    private static int[][] directions = {{0, -1}, {-1, -1}, {-1, 0}, {-1, 1}, {0, 1}, {1, 1}, {1, 0}, {1, -1}};
    public int countIslands(char[][] grid) {
        // Code here
        char[][] mat = Arrays.stream(grid).map(char[]::clone).toArray(char[][]::new);
        int count = 0;
        for (int i = 0; i < mat.length; i++) {
            for (int j = 0; j < mat[0].length; j++) {
                if (mat[i][j] == 'L') {
                    dfs(mat, i, j);
                    count++;
                }
            }
        }
        return count;
    }
    
    private void dfs(char[][] mat, int i, int j) {
        if (i < 0 || j < 0 || i == mat.length || j == mat[0].length || mat[i][j] == 'W') {
            return;
        }
        mat[i][j] = 'W';
        
        for (int[] dir: directions) {
            dfs(mat, i + dir[0], j + dir[1]);
        }
    }
}
```


# Using BFS

```java
class Solution {
    private static int[][] directions = {{0, -1}, {-1, -1}, {-1, 0}, {-1, 1}, {0, 1}, {1, 1}, {1, 0}, {1, -1}};
    public int countIslands(char[][] grid) {
        // Code here
        char[][] mat = Arrays.stream(grid).map(char[]::clone).toArray(char[][]::new);
        int count = 0;
        for (int i = 0; i < grid.length; i++) {
             for(int j = 0; j < grid[0].length; j++) {
                if(mat[i][j] == 'L') {
                    bfs(mat, i, j);
                    count++;
                }
             }
        }
        return count;
    }
    
    private void bfs(char[][] mat, int i, int j) {
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{i, j});
        mat[i][j] = 'W';
        while (!queue.isEmpty()) {
            int[] cur = queue.poll();
            for(int[] dir: directions) {
                int x = dir[0] + cur[0];
                int y = dir[1] + cur[1];
                
                if(x >= 0 && y >= 0 && x < mat.length && y < mat[0].length && mat[i][j] == 'L') {
                    mat[x][y] = 'W';
                    queue.offer(new int[]{x, y});
                }
            }
        }
    }
}
```