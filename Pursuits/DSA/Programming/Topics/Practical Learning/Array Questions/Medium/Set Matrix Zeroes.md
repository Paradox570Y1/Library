[73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

**Input:** matrix = `[[1,1,1],[1,0,1],[1,1,1]]`
**Output:** `[[1,0,1],[0,0,0],[1,0,1]]`

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

**Input:** matrix = `[[0,1,2,0],[3,4,5,2],[1,3,1,5]]`
**Output:** `[[0,0,0,0],[0,4,5,0],[0,3,1,0]]`

**Constraints:**

- `m == matrix.length`
- `n == matrix[0].length`
- `1 <= m, n <= 200`
- `-231 <= matrix[i][j] <= 231 - 1`

# Brute
**Time Complexity:** O((N*M)*(N + M)) + O(N*M), where N = no. of rows in the matrix and M = no. of columns in the matrix.  
**Reason:** Firstly, we are traversing the matrix to find the cells with the value 0. It takes O(N*M). Now, whenever we find any such cell we mark that row and column with -1. This process takes O(N+M). So, combining this the whole process, finding and marking, takes O((N*M)*(N + M)).  
Another O(N*M) is taken to mark all the cells with -1 as 0 finally.

**Space Complexity:** O(1) as we are not using any extra space.

```cpp
#include <bits/stdc++.h>
using namespace std;

void markRow(vector<vector<int>> &matrix, int n, int m, int i) {
    // set all non-zero elements as -1 in the row i:
    for (int j = 0; j < m; j++) {
        if (matrix[i][j] != 0) {
            matrix[i][j] = -1;
        }
    }
}


void markCol(vector<vector<int>> &matrix, int n, int m, int j) {
    // set all non-zero elements as -1 in the col j:
    for (int i = 0; i < n; i++) {
        if (matrix[i][j] != 0) {
            matrix[i][j] = -1;
        }
    }
}

vector<vector<int>> zeroMatrix(vector<vector<int>> &matrix, int n, int m) {

    // Set -1 for rows and cols
    // that contains 0. Don't mark any 0 as -1:

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (matrix[i][j] == 0) {
                markRow(matrix, n, m, i);
                markCol(matrix, n, m, j);
            }
        }
    }

    // Finally, mark all -1 as 0:
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (matrix[i][j] == -1) {
                matrix[i][j] = 0;
            }
        }
    }

    return matrix;
}

int main()
{
    vector<vector<int>> matrix = {{1, 1, 1}, {1, 0, 1}, {1, 1, 1}};
    int n = matrix.size();
    int m = matrix[0].size();
    vector<vector<int>> ans = zeroMatrix(matrix, n, m);

    cout << "The Final matrix is: n";
    for (auto it : ans) {
        for (auto ele : it) {
            cout << ele << " ";
        }
        cout << "n";
    }
    return 0;
}
```
# Better
Complexity Analysis

**Time Complexity:** O(2*(N*M)), where N = no. of rows in the matrix and M = no. of columns in the matrix.  

**Space Complexity:** O(N) + O(M), where N = no. of rows in the matrix and M = no. of columns in the matrix.  
*Reason:* O(N) is for using the row array and O(M) is for using the col array.

```java
class Solution {
    public void setZeroes(int[][] matrix) {
     int m = matrix.length;
        int n = matrix[0].length;
        List<Integer> row = new ArrayList<>();
        List<Integer> col = new ArrayList<>();
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j] == 0){
                    row.add(i);
                    col.add(j);
                }
            }
        }

        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(row.contains(i)==true){
                    matrix[i][j] = 0;
                }
                if (col.contains(j) == true) {
                    matrix[i][j] = 0;
                }
            }
        }   
    }
}
```

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        int row[]=new int[m];
        int col[]=new int[n];
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j] == 0){
                    row[i]=1;
                    col[j]=1;
                }
            }
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j] != 0){
                    if(row[i]==1 || col[j]==1){
                        matrix[i][j] = 0;
                    }
                }
            }
        }
     
    }
}
```

# Best Approach 
### **Intuition:**

In the previous approach, the time complexity is minimal as the traversal of a matrix takes at least O(N*M)(_where N = row and M = column_). In this approach, we can just improve the space complexity. So, instead of using two extra matrices **row** and **col**, we will use the 1st row and 1st column of the given matrix to keep a track of the cells that need to be marked with 0. But here comes a problem. If we try to use the 1st row and 1st column to serve the purpose, the cell matrix[0][0] is taken twice. To solve this problem we will take an extra variable col0 initialized with 1. Now the entire 1st row of the matrix will serve the purpose of the **row array**. And the 1st column from (0,1) to (0,m-1) with the col0 variable will serve the purpose of the **col array**.

![](https://static.takeuforward.org/wp/uploads/2023/04/Screenshot-2023-04-04-001419.png)

If any cell in the 0th row contains 0, we will mark matrix[0][0] as 0 and if any cell in the 0th column contains 0, we will mark the **col0** variable as 0.

---
**Time Complexity:** O(2*(N*M)), where N = no. of rows in the matrix and M = no. of columns in the matrix.  

**Space Complexity:** O(1) as we are not using any extra space.

---

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        int init = -1;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j] == 0){
                    if(j!=0)
                    matrix[0][j] = 0;
                    else
                    init = 0;
                    matrix[i][0] = 0;
                }
            }
        }
        for(int i=m-1;i>=0;i--){
            for(int j=n-1;j>0;j--){
                if(matrix[i][j] !=0){
                    if(matrix[i][0]==0 || matrix[0][j]==0){
                        matrix[i][j] = 0;
                    }
                }
            }
        }
        for(int i=0;i<m;i++){
            if(init==0 || matrix[i][0]==0)
                matrix[i][0] = 0;
        }
     
    }
}
```
OR
```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int row = matrix.length;
        int col = matrix[0].length;
        boolean col_0 = false,row_0 = false;
        for(int i=0;i<row;i++){
            if(matrix[i][0] == 0) row_0 = true;
        }
        for(int i=0;i<col;i++){
            if(matrix[0][i] == 0) col_0 = true;
        }
        for(int i=1;i<row;i++){
            for(int j=1;j<col;j++){
                if(matrix[i][j]==0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        for(int i=1;i<row;i++){
            for(int j=1;j<col;j++){
                if(matrix[i][0] == 0 || matrix[0][j] == 0){
                    matrix[i][j] = 0;
                }
            }
        }
        if(row_0){
            for(int i=0;i<row;i++){
                matrix[i][0] = 0;
            }
        }
        if(col_0){
            for(int i=0;i<col;i++){
                matrix[0][i] = 0;
            }
        }
    }
	}
```

OR

```js
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var setZeroes = function(matrix) {
    var row = matrix.length;
    var col = matrix[0].length;
    var mark=1;
    for(let i=0;i<row;i++){
        for(let j=0;j<col;j++){
            if(matrix[i][j] == 0){
                if(j==0)mark=0;
                else matrix[0][j] = 0;
                matrix[i][0] = 0;
            }
        }
    }
    for(let i=1;i<row;i++){
        for(let j=1;j<col;j++){
            if(matrix[i][0] == 0 || matrix[0][j]==0){
                matrix[i][j] = 0;
            }
        }
    }
    if(matrix[0][0] == 0){
        for(let i=1;i<col;i++){
            matrix[0][i] = 0;
        }
    }
    if(mark==0){
        for(let i=0;i<row;i++){
            matrix[i][0] =0;
        }
    }
};
```