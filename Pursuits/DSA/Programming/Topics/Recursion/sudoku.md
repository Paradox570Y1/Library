[37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver/)

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

1. Each of the digits `1-9` must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

The `'.'` character indicates empty cells.

**Example 1:**

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

**Input:** board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
**Output:** [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
**Explanation:** The input board is shown above and the only valid solution is shown below:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)

**Constraints:**

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit or `'.'`.
- It is **guaranteed** that the input board has only one solution.


# Better

```java
class Solution {
    boolean p1(int i,int j,int k,char[][] board){
        for(int l=0;l<board[0].length;l++){
            if(board[i][l]!='.' && k+'0' == board[i][l])return false;
        }
        return true;
    }
    boolean p2(int i,int j,int k,char[][] board){
        for(int l=0;l<board.length;l++){
            if(board[l][j]!='.' && k+'0' == board[l][j])return false;
        }
        return true;
    }
    boolean p3(int i,int j,int k,char[][] board){
        int sti = i-i%3;
        int stj = j-j%3;
        for(int m=sti;m<sti+3;m++){
            for(int n = stj;n<stj+3;n++){
                if(board[m][n] ==k+'0')return false;
            }
        }
        return true;
    }
    boolean possible(int i,int j,int k,char[][] board){
        return (p1(i,j,k,board) && p2(i,j,k,board) && p3(i,j,k,board));
    }
    boolean solve(char[][] board,int i,int j){
        //base
        if(i==board.length)return true;
        if(j==board[0].length)return solve(board,i+1,0); 
        //loop 1-9
        if(board[i][j]!= '.')return solve(board,i,j+1);

            for(int k=1;k<=9;k++){
                if(possible(i,j,k,board)){
                    board[i][j] = (char)(k+'0');
                    if(solve(board,i,j+1))return true;
                    board[i][j] = '.';
                }
            }
        return false;
    }
    public void solveSudoku(char[][] board) {
      solve(board,0,0);
    }
}
```


OR

```java
class Solution {
    int n;
    private boolean canFill(char[][] board,char num,int i,int j){
        int a=i,b=j;
        for(int pos=0;pos<n;pos++){
            if(board[i][pos]==num)return false;
            if(board[pos][j] == num)return false;
        }
        int len = n/3;
        int rowSt = i-(i%len);
        int colSt = j-(j%len);
        for(int row=rowSt;row<rowSt+len;row++){
            for(int col=colSt;col<colSt+len;col++){
                if(board[row][col] == num)return false;
            }
        }
        return true;
    }
    private boolean solve(char[][] board, int i,int j){
        if(i==n)return true;
        if(j==n)return solve(board,i+1,0);
        if(board[i][j] != '.')return solve(board,i,j+1);
        for(char num = '1';num<='9';num++){
            if(!canFill(board,num,i,j))continue;
            board[i][j] = num;
            if(solve(board,i,j+1))return true;
            board[i][j] = '.';
        }
        return false;
    }
    public void solveSudoku(char[][] board) {
        n = board.length;
        solve(board,0,0);
    }
}
```