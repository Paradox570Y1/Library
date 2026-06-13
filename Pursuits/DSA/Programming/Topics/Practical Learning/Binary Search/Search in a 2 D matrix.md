[74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)
You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` _if_ `target` _is in_ `matrix` _or_ `false` _otherwise_.

You must write a solution in `O(log(m * n))` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
**Output:** false

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- `-104 <= matrix[i][j], target <= 104`



# Optimal
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int n = matrix.length,m=matrix[0].length;
        int low =0,high = n*m-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int ele = matrix[mid/m][mid%m];
            if(ele == target)return true;
            else if(ele>target)high = mid-1;
            else low = mid+1;
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;
        int low = 0,high = (m*n)-1;
        while(low<=high){
            int mid = (low+high)>>1;
            int row = mid/n, col = mid%n;
            if(matrix[row][col] == target)return true;
            else if(matrix[row][col]<target) low = mid+1;
            else high = mid -1;
        }
        return false;
    }
}
```