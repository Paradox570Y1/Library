[51. N-Queens](https://leetcode.com/problems/n-queens/)

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4
**Output:** [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above

**Example 2:**

**Input:** n = 1
**Output:** [["Q"]]

**Constraints:**

- `1 <= n <= 9`

# Brute
**Time Complexity:** Exponential in nature since we are trying out all ways, to be precise its O(N! * N ).

**Space Complexity:** O(1 )
```java
class Solution {
    boolean check(List<String> board,int row,int col,int n){
        int i=row;
        int j=col;
        while(col>=0){
            if(board.get(row).charAt(col) == 'Q')return false;
            col--;
        }
        col = j;
        while(row>=0 && col>=0){
            if(board.get(row).charAt(col) == 'Q')return false;
            row--;col--;
        }
        row = i;
        col = j;
        while(row<n && col>=0){
            if(board.get(row).charAt(col) == 'Q')return false;
            row++;col--;
        }
        return true;
    }
    void generate(int n,int col,List<String> board,List<List<String>> ans){
        if(n==col){
            ans.add(new ArrayList<>(board));
            return;
        }
        
        for(int row=0;row<n;row++){
            if(check(board,row,col,n)){
                String s = board.get(row);
                board.set(row,s.substring(0,col)+"Q"+s.substring(col+1,n));
                generate(n,col+1,board,ans);
                board.set(row,s);
            }
        }
        return;
    }
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();
        List<String> board = new ArrayList<>();
        String s = ".".repeat(n);
        for(int i=0;i<n;i++){
            board.add(s);
        }
        generate(n,0,board,ans);
        return ans;
    }
}
```

# Better

```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();
        List<String> board = new ArrayList<>();
        String s = ".".repeat(n);
        for(int i=0;i<n;i++){
            board.add(s);
        }
        boolean flag[][] = new boolean[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                flag[i][j] = false;
            }
        }
        boolean upperD[] = new boolean[2*n-1];
        boolean lowerD[] = new boolean[2*n-1];
        boolean left[] = new boolean[n];
        helper(ans,board,n,0,upperD,lowerD,left,flag);
        return ans;
    }
    void helper(List<List<String>> ans,List<String> board,int n,int col,boolean []upperD,boolean []lowerD,boolean []left,boolean[][] flag){
        if(col==n){
            ans.add(new ArrayList<>(board));
            return;
        }
        for(int row=0;row<n;row++){
            if(left[row] || lowerD[row+col]|| upperD[n-1+col-row])continue;
            String temp = board.get(row);
            board.set(row,temp.substring(0,col)+"Q"+temp.substring(col+1,n));
            left[row] = lowerD[row+col] = upperD[n-1+col-row] = true;
            helper(ans,board,n,col+1,upperD,lowerD,left,flag);
            board.set(row,temp);
            left[row] = lowerD[row+col] = upperD[n-1+col-row] = false;
        }
    }
}
```

**Time Complexity:** Exponential in nature since we are trying out all ways, to be precise its O(N! * N).

**Space Complexity:** O(N)
```java
class Solution {
    void generate(int n,int col,List<String> board,List<List<String>> ans,boolean[] leftRow,boolean[] upperD,boolean[] lowerD){
        if(n==col){
            ans.add(new ArrayList<>(board));
            return;
        }
        
        for(int row=0;row<n;row++){
            if(leftRow[row] || upperD[n-1+(col-row)] || lowerD[col+row])continue;
            String s = board.get(row);
            board.set(row,s.substring(0,col)+"Q"+s.substring(col+1,n));
            leftRow[row] = true;
            upperD[n-1 + (col-row)] = true;
            lowerD[col+row] = true;
            generate(n,col+1,board,ans,leftRow,upperD,lowerD);
            leftRow[row] = false;
            upperD[n-1 + (col-row)] = false;
            lowerD[col+row] = false;
            board.set(row,s);
        }
        return;
    }
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();
        List<String> board = new ArrayList<>();
        String s = ".".repeat(n);
        for(int i=0;i<n;i++){
            board.add(s);
        }

        generate(n,0,board,ans,new boolean[n],new boolean[2*n-1],new boolean[2*n-1]);
        return ans;
    }
}
```


OR
##### Most better code
```java
class Solution {
    List<List<String>> ans;
    int n;
    boolean visited[][];
    String s;
    private boolean isVisited(int i,int j){
        for(int row = i;row>=0;row--){
            if(visited[row][j])return true;
        }
        int a=i,b=j;
        while(a>=0 && b>=0){
            if(visited[a][b])return true;
            a--;b--;
        }
        a=i;b=j;
        while(a>=0 && b<n){
            if(visited[a][b])return true;
            a--;b++;
        }
        return false;
    }
    private void generate(int i,List<String> li){
        if(i==n){
            ans.add(new ArrayList<>(li));
            return;
        }
        StringBuilder sb =new StringBuilder(s);
        for(int j=0;j<n;j++){
            if(!isVisited(i,j)){
                sb.setCharAt(j,'Q');
                li.add(sb.toString());
                visited[i][j] = true;
                generate(i+1,li);
                visited[i][j] = false;
                li.remove(li.size()-1);
                sb.setCharAt(j,'.');
            } 
        }
    }
    public List<List<String>> solveNQueens(int n) {
        ans = new ArrayList<>();
        visited = new boolean[n][n];
        this.n = n;
        s = new String(".".repeat(n));
        generate(0,new ArrayList<>());
        return ans;
    }
}
```
# Optimal


```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();
        char[][] board = new char[n][n];
        boolean flag[][] = new boolean[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                flag[i][j] = false;
                board[i][j] = '.';
            }
        }
        boolean upperD[] = new boolean[2*n-1];
        boolean lowerD[] = new boolean[2*n-1];
        boolean left[] = new boolean[n];
        helper(ans,board,n,0,upperD,lowerD,left,flag);
        return ans;
    }
    void helper(List<List<String>> ans,char[][] board,int n,int col,boolean []upperD,boolean []lowerD,boolean []left,boolean[][] flag){
        if(col==n){
            List<String> res = new ArrayList<>();
            for(int i=0;i<n;i++)res.add(new String(board[i]));
            ans.add(new ArrayList<>(res));
            return;
        }
        for(int row=0;row<n;row++){
            if(left[row] || lowerD[row+col]|| upperD[n-1+col-row])continue;
            board[row][col] = 'Q';
            left[row] = lowerD[row+col] = upperD[n-1+col-row] = true;
            helper(ans,board,n,col+1,upperD,lowerD,left,flag);
            board[row][col] = '.';
            left[row] = lowerD[row+col] = upperD[n-1+col-row] = false;
        }
    }
}
```

OR

```java
class Solution {
    List<List<String>> ans;
    int n;
    boolean visitedCol[];
    boolean leftDiag[];
    boolean rightDiag[];
    String s;
    private void generate(int i,List<String> li){
        if(i==n){
            ans.add(new ArrayList<>(li));
            return;
        }
        StringBuilder sb =new StringBuilder(s);
        for(int j=0;j<n;j++){
            if(visitedCol[j] || leftDiag[i+j] || rightDiag[n-1-i+j])continue;
            sb.setCharAt(j,'Q');
            li.add(sb.toString());
            visitedCol[j] = leftDiag[i+j] = rightDiag[n-1-i+j] = true;
            generate(i+1,li);
            visitedCol[j] = leftDiag[i+j] = rightDiag[n-1-i+j] = false;
            li.remove(li.size()-1);
            sb.setCharAt(j,'.');
        }
    }
    public List<List<String>> solveNQueens(int n) {
        ans = new ArrayList<>();
        this.n = n;
        visitedCol = new boolean[n];
        leftDiag = new boolean[2*n-1];
        rightDiag = new boolean[2*n-1];
        s = new String(".".repeat(n));
        generate(0,new ArrayList<>());
        return ans;
    }
}
```

OR

```java
class Solution {
    private boolean[] row, col, lDiag, rDiag;
    private void helper(int n, int i, List<List<String>> res, List<String> board) {
        if (i == n) {
            res.add(new ArrayList<>(board));
            return;
        }
        char[] s = new char[n];
        Arrays.fill(s, '.');
        for (int j = 0; j < n; j++) {
            if (row[i] || col[j] || lDiag[i+j] || rDiag[i-j+n-1]) continue;
            row[i] = col[j] = lDiag[i+j] = rDiag[i-j+n-1] = true;
            s[j] = 'Q';
            board.add(new String(s));
            helper(n, i+1, res, board);
            board.remove(board.size()-1);
            s[j] = '.';
            row[i] = col[j] = lDiag[i+j] = rDiag[i-j+n-1] = false;
        }
    }
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();
        row = new boolean[n];
        col = new boolean[n];
        lDiag = new boolean[2*n+1];
        rDiag = new boolean[2*n+1];
        helper(n, 0, res, new ArrayList<>());
        return res;
    }
}
```