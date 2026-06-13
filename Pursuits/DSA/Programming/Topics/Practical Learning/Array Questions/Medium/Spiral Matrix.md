[Link](https://leetcode.com/problems/spiral-matrix/description/)
Given an `m x n` `matrix`, return _all elements of the_ `matrix` _in spiral order_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

**Input:** matrix = `[[1,2,3],[4,5,6],[7,8,9]]`
**Output:** [1,2,3,6,9,8,7,4,5]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

**Input:** matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
**Output:** [1,2,3,4,8,12,11,10,9,5,6,7]

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

# Optimal only
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int  n = matrix.length;
        int m = matrix[0].length;
        List<Integer> ans = new ArrayList<>();
        int left=0,top=0,right=m-1,bottom=n-1;


        while(left<=right && top <= bottom){
            for(int i=left;i<=right;i++){
                ans.add(matrix[top][i]);
            }
            top++;
            for(int i=top;i<=bottom;i++){
                ans.add(matrix[i][right]);
            }
            right--;
            //in case of single line array
            if(top<=bottom){
                for(int i=right;i>=left;i--){
                ans.add(matrix[bottom][i]);
            }
            bottom--;
            }
            //for last turn in spiral matrix
            if(left<=right){
                for(int i=bottom;i>=top;i--){
                ans.add(matrix[i][left]);
            }
            left++;
            }
            
        }
        return ans;
    }
}
```
**Time Complexity: O(m x n)** { Since all the elements are being traversed once and there are total n x m elements ( m elements in each row and total n rows) so the time complexity will be O(n x m)}.

**Space Complexity: O(n)** { Extra Space used for storing traversal in the ans array }.


# Other way

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> li = new ArrayList<>();
        int r[] = {0,1,0,-1};
        int c[] = {1,0,-1,0};
        int row = matrix.length;
        int col = matrix[0].length;
        int i=0,j=0,k=0;
        int nexti,nextj;
        int n = row*col;
        while(n-->0){
            li.add(matrix[i][j]);
            matrix[i][j]=101;
            nexti= r[k]+i;
            nextj = c[k]+j;
            if(nextj==col || nexti==row || nextj<0 || matrix[nexti][nextj]==101){
                k = (k+1)%4;
                nexti = i + r[k];
                nextj = j + c[k];
            }
            i = nexti;
            j = nextj;
            
        }
        return li;
    }
}
```


OR

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        int n = matrix.length, m = matrix[0].length;
        int top = 0, bottom = n-1;
        int left = 0, right = m-1;
        int i = 0, j = 0;
        int ic = 1, jc = 1;
        while (left <= right && top <=bottom) {
            res.add(matrix[i][j]);
            if (ic == jc){
                j += jc;
                if(left <= j && j <= right) continue;
                j -= jc;
                i += ic;
                if(jc == 1) top++;
                else bottom--;
                jc *= -1;
            }
            else {
                i += ic;
                if (top <= i && i <= bottom) continue;
                i -= ic;
                j += jc;
                if(ic == 1) right--;
                else left++;
                ic *= -1;
            }
        }
        return res;
    }
}
```