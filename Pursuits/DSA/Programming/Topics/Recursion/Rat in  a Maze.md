[Link](https://www.geeksforgeeks.org/problems/rat-in-a-maze-problem/1)
### Rat in a Maze Problem - I

Difficulty: **Medium**Accuracy: **35.75%**Submissions: **312K+**Points: **4**

Consider a rat placed at position (0, 0) in an **n x n** square matrix `mat`. The rat's goal is to reach the destination at position (n-1, n-1). The rat can move in four possible directions: **'U'(up)**, **'D'(down)**, **'L' (left)**, **'R' (right)**.

The matrix contains only two possible values:

- `0`: A blocked cell through which the rat **cannot** travel.
- `1`: A free cell that the rat **can** pass through.

**Note**: In a path, no cell can be visited more than one time. If the source cell is 0, the rat cannot move to any other cell. In case of no path, return an empty list.+  

The task is to find all possible paths the rat can take to reach the destination, starting from (0, 0) and ending at (n-1, n-1), under the condition that the rat cannot revisit any cell along the same path. Furthermore, the rat can only move to adjacent cells that are within the bounds of the matrix and not blocked.

**Examples:**

**Input**: mat[][] = [[1, 0, 0, 0], [1, 1, 0, 1], [1, 1, 0, 0], [0, 1, 1, 1]]
**Output:** ["DDRDRR", "DRDDRR"]
**Explanation**: The rat can reach the destination at (3, 3) from (0, 0) by two paths - DRDDRR and DDRDRR, when printed in sorted order we get DDRDRR DRDDRR.

**Input**: mat[][] = [[1, 0], [1, 0]]
**Output:** []
**Explanation**: No path exists and the destination cell is blocked.

**Input**: mat = [[1, 1, 1], [1, 0, 1], [1, 1, 1]]
**Output:** ["DDRR", "RRDD"]
**Explanation**: The rat has two possible paths to reach the destination: 1. "DDRR" 2. "RRDD", These are returned in lexicographically sorted order.

**Constraints:**  
2 ≤ mat.size() ≤ 5  
0 ≤ mat[i][j] ≤ 1


# Brute

**Time Complexity: O(4^(m\*n)),** because on every cell we need to try 4 different directions.

**Space Complexity:  O(m\*n),** Maximum Depth of the recursion tree(auxiliary space).

```java
class Solution {
    // Function to find all possible paths
    void generatePath(ArrayList<String> ans,String s,ArrayList<ArrayList<Integer>> mat,int i,int j,boolean[][] visited){
        int h =mat.size(),w = mat.get(0).size();
        
        if(i==h-1 && j == w-1){
            ans.add(s);
            return;
        }
        visited[i][j] = true;
        if(i+1<h && mat.get(i+1).get(j) == 1 && !visited[i+1][j]){
            generatePath(ans,s+"D",mat,i+1,j,visited);
        }
        if(j-1>=0 && mat.get(i).get(j-1) == 1 && !visited[i][j-1]){
            generatePath(ans,s+"L",mat,i,j-1,visited);
        }
        
        if(j+1<w && mat.get(i).get(j+1) == 1 && !visited[i][j+1]){
            generatePath(ans,s+"R",mat,i,j+1,visited);
        }
        if(i-1>=0 && mat.get(i-1).get(j) == 1 && !visited[i-1][j]){
            generatePath(ans,s+"U",mat,i-1,j,visited);
        }
        visited[i][j] = false;
    }
    public ArrayList<String> findPath(ArrayList<ArrayList<Integer>> mat) {
        // code here
        ArrayList<String> ans = new ArrayList<>();
        generatePath(ans,"",mat,0,0,new boolean[mat.size()][mat.get(0).size()]);
        return ans;
    }
}
```

Better time complexity and cleaner code using extra space
```java
class Solution {
    // Function to find all possible paths
    void generatePath(ArrayList<String> ans,String s,ArrayList<ArrayList<Integer>> mat,int i,int j,boolean[][] visited,int[] di,int[] dj){
        int h =mat.size(),w = mat.get(0).size();
        
        if(i==h-1 && j == w-1){
            ans.add(s);
            return;
        }
        String dir = "DLRU";
        for(int idx = 0;idx<4;idx++){
            int new_i = i+di[idx];
            int new_j = j+dj[idx];
            if(new_i>=0 && new_i<h && new_j>=0 && new_j<w && mat.get(new_i).get(new_j) == 1 && !visited[new_i][new_j]){
                visited[i][j] = true;
                generatePath(ans,s+dir.charAt(idx),mat,new_i,new_j,visited,di,dj);
                visited[i][j] = false;
            }
        }
    }
    public ArrayList<String> findPath(ArrayList<ArrayList<Integer>> mat) {
        // code here
        ArrayList<String> ans = new ArrayList<>();
        int di[]=  {1,0,0,-1};
        int dj[] = {0,-1,1,0};
        generatePath(ans,"",mat,0,0,new boolean[mat.size()][mat.get(0).size()],di,dj);
        return ans;
    }
}
```


better space complexity 
```java
class Solution {
    // Function to find all possible paths
    public ArrayList<String> findPath(ArrayList<ArrayList<Integer>> mat) {
        // code here
        ArrayList<String> ans = new ArrayList<>();
        if(mat.get(0).get(0)==0)return ans;
        helper(mat,0,0,mat.size(),ans,"");
        return ans;
    }
    void helper(ArrayList<ArrayList<Integer>> mat,int row,int col,int n,ArrayList<String> ans,String s){
        if(col==n-1 && row==n-1){
            ans.add(s);
            return;
        }
        if(row<0 || col<0 || row>=n || col>=n || mat.get(row).get(col)!=1)return;
        int temp = mat.get(row).get(col);
        mat.get(row).set(col,-1);
        
        if(row<n-1)
        helper(mat,row+1,col,n,ans,s+"D");
        if(col>0)
        helper(mat,row,col-1,n,ans,s+"L");
        if(col<n-1)
        helper(mat,row,col+1,n,ans,s+"R");
        if(row>0)
        helper(mat,row-1,col,n,ans,s+"U");
        mat.get(row).set(col,temp);
    }
}
```