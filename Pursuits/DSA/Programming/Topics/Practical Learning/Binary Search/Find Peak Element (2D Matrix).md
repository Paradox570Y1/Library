[1901. Find a Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/)
A **peak** element in a 2D grid is an element that is **strictly greater** than all of its **adjacent** neighbors to the left, right, top, and bottom.

Given a **0-indexed** `m x n` matrix `mat` where **no two adjacent cells are equal**, find **any** peak element `mat[i][j]` and return _the length 2 array_ `[i,j]`.

You may assume that the entire matrix is surrounded by an **outer perimeter** with the value `-1` in each cell.

You must write an algorithm that runs in `O(m log(n))` or `O(n log(m))` time.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/06/08/1.png)

**Input:** mat = [[1,4],[3,2]]
**Output:** [0,1]
**Explanation:** Both 3 and 4 are peak elements so [1,0] and [0,1] are both acceptable answers.

**Example 2:**

**![](https://assets.leetcode.com/uploads/2021/06/07/3.png)**

**Input:** mat = [[10,20,15],[21,30,14],[7,16,32]]
**Output:** [1,1]
**Explanation:** Both 30 and 32 are peak elements so [1,1] and [2,2] are both acceptable answers.

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `1 <= m, n <= 500`
- `1 <= mat[i][j] <= 105`
- No two adjacent cells are equal.

# Brute
TC => O(n\*m)
```java
class Solution {
    public int[] findPeakGrid(int[][] mat) {
        int n=mat[0].length,m=mat.length;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                int ele = mat[i][j];
                int right = -1,down=-1,top=-1,left=-1;
                if(j+1<n) right =mat[i][j+1];
                if(i+1<m) down = mat[i+1][j];
                if(i-1>=0) top = mat[i-1][j];
                if(j-1>=0) left = mat[i][j-1];
                if(ele>right && ele >down && ele >top && ele > left)return new int[]{i,j};
            }
        }
        return new int[]{-1,-1};
    }
}
```
# Better
TC = > O(n\*m)
```java
class Solution {
    public int[] findPeakGrid(int[][] mat) {
        int i=0,j=0;
        int n=mat[0].length,m=mat.length;
        while(i<m && j<n){
            int ele = mat[i][j];
            int right = -1,down = -1,top = -1,left = -1;
            if(j+1<n) right =mat[i][j+1];
            if(i+1<m) down = mat[i+1][j];
            if(i-1>=0) top = mat[i-1][j];
            if(j-1>=0) left = mat[i][j-1];
            if(ele>right && ele >down && ele >top && ele > left)return new int[]{i,j};
            else if(right>down){
                if(top>right){
                    if(left>top)j--; else i--;
                }
                else{
                    if(left>right)j--; else j++;
                }
            }
            else{
                if(down>top){
                    if(left>down)j--; else i++;
                } 
                else{
                    if(left>top)j--; else i--;
                }
            }
        }
        return new int[]{-1,-1};
    }
}
```

# Best
Using Binary Search TC => O(n\*log m)

```java
class Solution {
    public int[] findPeakGrid(int[][] mat) {
        int low = 0, high = mat[0].length-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int i=0,j=mid;
            for(int k=0;k<mat.length-1;k++){
                if(mat[i][mid]<mat[k+1][mid])i =k+1;
            }
            int left=-1,right=-1;
            if(j-1>=0) left = mat[i][j-1];
            if(j+1<mat[0].length) right = mat[i][j+1];
            if(mat[i][j]>left && mat[i][j]>right) return new int[]{i,j};
            else if(mat[i][j]<left)high =mid-1;
            else low = mid+1;
        }
        return new int[]{-1,-1};
    }
}
```