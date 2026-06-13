[52. N-Queens II](https://leetcode.com/problems/n-queens-ii/)

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _the number of distinct solutions to the **n-queens puzzle**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4
**Output:** 2
**Explanation:** There are two distinct solutions to the 4-queens puzzle as shown.

**Example 2:**

**Input:** n = 1
**Output:** 1

**Constraints:**

- `1 <= n <= 9`


# Brute
50%
```java
class Solution {
    public int totalNQueens(int n) {
        boolean[][]  board = new boolean[n][n];
        return helper(board,0,n);
    }
    int helper(boolean[][] board,int col,int n){
        if(col==n){
            return 1;
        }
        int cnt=0;
        for(int row=0;row<n;row++){
            if(check(board,row,col,n)){
                board[row][col] = true;
                cnt+=helper(board,col+1,n);
                board[row][col] = false;
            }
        }
        return cnt;
    }
    boolean check(boolean[][] board,int row,int col,int n){
        for(int i=0;i<col;i++){
            if(board[row][i])return false;
        }
        int i=row,j=col;
        while(i>=0 && j>=0){
            if(board[i][j])return false;
            i--;j--;
        }
        i=row;j=col;
        while(i<n && j>=0){
            if(board[i][j])return false;
            i++;j--;
        }
        return true;
    }
}
```


# Better
77%

```java
class Solution {
    public int totalNQueens(int n) {
        boolean[][]  board = new boolean[n][n];
        boolean[] checkRow = new boolean[n];
        boolean[] upperD = new boolean[2*n-1];
        boolean[] lowerD = new boolean[2*n-1];
        return helper(board,0,n,checkRow,upperD,lowerD);
    }
    int helper(boolean[][] board,int col,int n,boolean[] checkRow,boolean[] upperD,boolean[] lowerD){
        if(col==n){
            return 1;
        }
        int cnt=0;
        for(int row=0;row<n;row++){
            if(checkRow[row] || upperD[n-1-col+row] || lowerD[row+col])continue;
            board[row][col] = true;
            checkRow[row] = upperD[n-1-col+row] = lowerD[row+col] = true;
            cnt+=helper(board,col+1,n,checkRow,upperD,lowerD);
            checkRow[row] = upperD[n-1-col+row] = lowerD[row+col] = false;
            board[row][col] = false;
        }
        return cnt;
    }
}
```


# Optimal

TC =  O(N!)
SC = O(1)
```java
class Solution {
    public int totalNQueens(int n) {
        return helper(0,0,0,0,n);
    }
    int helper(int row,int col,int diag,int antiD,int n){
        int cnt=0;
        if(row==n)return 1;
        int possiblePos = ((1<<n)-1) & ~(col | diag | antiD);
        while(possiblePos!=0){
            int pos = possiblePos & -possiblePos;
            possiblePos = possiblePos & possiblePos-1;
            cnt+= helper(row+1,col|pos,(diag|pos)<<1,(antiD|pos)>>1,n);
        }
        return cnt;
    }
}
```