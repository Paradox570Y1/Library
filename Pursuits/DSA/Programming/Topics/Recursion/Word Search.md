[79. Word Search](https://leetcode.com/problems/word-search/)

Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
**Output:** true

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
**Output:** false

**Constraints:**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.







# Brute (Using DFS)
TC-> **O(mxnx4^k)**,
SC-> **O(K + mxn)**
```java
class Solution {
    boolean check(char[][] board,String word,int i,int j,int idx,boolean[][] visited){
         if(word.length() == idx)return true;
         if(i<0 || i>=board.length || j<0 || j>=board[0].length || word.charAt(idx) != board[i][j] || visited[i][j])return false;
         visited[i][j] = true;
         boolean found = check(board,word,i+1,j,idx+1,visited) || 
            check(board,word,i-1,j,idx+1,visited) || 
            check(board,word,i,j+1,idx+1,visited) || 
            check(board,word,i,j-1,idx+1,visited); 
         visited[i][j] = false;
        return found;
    }
    public boolean exist(char[][] board, String word) {
        int row = board.length;
        int col = board[0].length;
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(board[i][j]==word.charAt(0) && check(board,word,i,j,0,new boolean[row][col])) return true;
            }
        }
        return false;
    }
}
```

OR

```java
class Solution {
    char[][] board;
    boolean[][] visited;
    String word;
    int n;
    private boolean generate(int i,int j,int k){
        if(k == n)return true;
        if(i==board.length || j==board[0].length || i<0 || j<0 || visited[i][j] || word.charAt(k)!=board[i][j])return false;
        visited[i][j] = true;
        if(
            generate(i+1,j,k+1) ||
            generate(i-1,j,k+1) ||
            generate(i,j+1,k+1) ||
            generate(i,j-1,k+1)
        )return true;
        visited[i][j] = false;
        return false;
    }
    public boolean exist(char[][] board, String word) {
        this.board = board;
        this.word = word;
        int a = board.length;
        int b = board[0].length;
        n=word.length();
        for(int i=0;i<a;i++){
            for(int j=0;j<b;j++){
                visited = new boolean[a][b];
                if(generate(i,j,0))return true;
            }
        }
        return false;
    }
}
```

OR

```java
class Solution {
    char[][] board;
    boolean[][] visited;
    String word;
    int n;
    private boolean generate(int i,int j,int k){
        if(k == n)return true;
        if(i==board.length || j==board[0].length || i<0 || j<0 || visited[i][j] || word.charAt(k)!=board[i][j])return false;
        visited[i][j] = true;
        if(
            generate(i+1,j,k+1) ||
            generate(i-1,j,k+1) ||
            generate(i,j+1,k+1) ||
            generate(i,j-1,k+1)
        )return true;
        visited[i][j] = false;
        return false;
    }
    public boolean exist(char[][] board, String word) {
        this.board = board;
        this.word = word;
        int a = board.length;
        int b = board[0].length;
        n=word.length();
        for(int i=0;i<a;i++){
            for(int j=0;j<b;j++){
                visited = new boolean[a][b];
                if(word.charAt(0) == board[i][j] && generate(i,j,0))return true;
            }
        }
        return false;
    }
}
```
# Optimal 
You can optimize the space
TC-> **O(mxnx4^k)**,
SC-> **O(K)**
```java
class Solution {
    boolean check(char[][] board,String word,int i,int j,int idx){
         if(word.length() == idx)return true;
         if(i<0 || i>=board.length || j<0 || j>=board[0].length || word.charAt(idx) != board[i][j] || board[i][j]==' ')return false;
         char ch = board[i][j];
         board[i][j] = ' ';
         boolean found = check(board,word,i+1,j,idx+1) || 
            check(board,word,i-1,j,idx+1) || 
            check(board,word,i,j+1,idx+1) || 
            check(board,word,i,j-1,idx+1); 
         board[i][j] = ch;
        return found;
    }
    public boolean exist(char[][] board, String word) {
        int row = board.length;
        int col = board[0].length;
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(board[i][j]==word.charAt(0) && check(board,word,i,j,0)) return true;
            }
        }
        return false;
    }
}
```

OR

```java
class Solution {
     public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0 || word == null || word.length() == 0) {
            return false;
        }
        
        int rows = board.length;
        int cols = board[0].length;
        
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (board[i][j] == word.charAt(0) && dfs(board, i, j, word, 0)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    private boolean dfs(char[][] board, int i, int j, String word, int index) {
        if (index == word.length()) {
            return true;
        }
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word.charAt(index)) {
            return false;
        }
        
        // Mark the cell as visited by temporarily changing its value
        char temp = board[i][j];
        board[i][j] = '#';
        
        // Explore all four possible directions
        boolean found = dfs(board, i + 1, j, word, index + 1) ||
                       dfs(board, i - 1, j, word, index + 1) ||
                       dfs(board, i, j + 1, word, index + 1) ||
                       dfs(board, i, j - 1, word, index + 1);
        
        // Restore the cell's original value
        board[i][j] = temp;
        return found;
    }
}
```