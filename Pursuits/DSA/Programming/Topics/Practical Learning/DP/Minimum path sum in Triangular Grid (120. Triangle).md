[120. Triangle](https://leetcode.com/problems/triangle/)

Given a `triangle` array, return _the minimum path sum from top to bottom_.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

**Example 1:**

**Input:** triangle =` [[2],[3,4],[6,5,7],[4,1,8,3]]`
**Output:** 11
**Explanation:** The triangle looks like:
   2
  3 4
 6 5 7
4 1 8 3
The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).

**Example 2:**

**Input:** triangle = `[[-10]]`
**Output:** -10

**Constraints:**

- `1 <= triangle.length <= 200`
- `triangle[0].length == 1`
- `triangle[i].length == triangle[i - 1].length + 1`
- `-104 <= triangle[i][j] <= 104`


# Using Memoization
```java
class Solution {
    private int helper(List<List<Integer>> triangle,int i,int last,int[][] memo){
        if(i==triangle.size())return 0;
        if(memo[i][last]!=10001)return memo[i][last];
        int path1 = triangle.get(i).get(last) + helper(triangle,i+1,last,memo);
        int path2 = triangle.get(i).get(last) + helper(triangle,i+1,last+1,memo);
        return memo[i][last] = Math.min(path1,path2);
    }
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        int memo[][] = new int[n][];
        for(int i=0;i<n;i++){
            memo[i] = new int[i+1];
            Arrays.fill(memo[i],10001);
        }
        return helper(triangle,0,0,memo);
    }
}
```



# Using Tabulation

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        int dp[][] = new int[n][];
        for(int i=0;i<n;i++){
            dp[i] = new int[i+1];
            Arrays.fill(dp[i],20001);
        }
        dp[0][0] = triangle.get(0).get(0);
        for(int i=1;i<n;i++){
            for(int j=0;j<dp[i-1].length;j++){
                dp[i][j] = Math.min(dp[i][j],dp[i-1][j]+triangle.get(i).get(j));
                dp[i][j+1] = Math.min(dp[i][j+1],dp[i-1][j]+triangle.get(i).get(j+1));
            }
        }
        int ans=20001;
        for(int i=0;i<dp[n-1].length;i++){
            ans = Math.min(ans,dp[n-1][i]);
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        int dp[][] = new int[n][];
        for(int i=0;i<n;i++){
            dp[i] = new int[i+1];
        }
        for(int i=0;i<dp[n-1].length;i++){
            dp[n-1][i] = triangle.get(n-1).get(i);
        }
        for(int i=n-2;i>=0;i--){
            for(int j=i;j>=0;j--){
                dp[i][j] = triangle.get(i).get(j) + Math.min(dp[i+1][j],dp[i+1][j+1]);
            }
        }
        return dp[0][0];
    }
}
```


OR

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        for (int i = triangle.size()-2; i >= 0; i--) {
            for (int j = 0; j < triangle.get(i).size(); j++) {
                List<Integer> list = triangle.get(i);
                list.set(j, list.get(j) + Math.min(triangle.get(i+1).get(j), triangle.get(i+1).get(j+1)));
            }
        }
        return triangle.get(0).get(0);
    }
}
```




Striver's code

```java
static int minimumPathSum(int[][] triangle, int n) {
        int[] front = new int[n];
        int[] cur = new int[n]; 
        for (int j = 0; j < n; j++) {
            front[j] = triangle[n - 1][j];
        }
        for (int i = n - 2; i >= 0; i--) {
            for (int j = i; j >= 0; j--) {
                int down = triangle[i][j] + front[j];
                int diagonal = triangle[i][j] + front[j + 1];
                cur[j] = Math.min(down, diagonal);
            }
            front = cur.clone();
        }
        return front[0];
    }
```


OR  Bottom to Top

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int r = triangle.size();
        int c = triangle.get(r-1).size();
        int[] dp = new int[c];
        for(int i = 0; i < c; i++) {
            dp[i] = triangle.get(r-1).get(i);
        }
        for (int i = r-2; i>=0; i--) {
            for (int j = 0; j <= i; j++) {
                dp[j] = triangle.get(i).get(j) + Math.min(dp[j], dp[j+1]);
            }
            dp[i+1] += triangle.get(i).get(i);
        }
        return dp[0];
    }
}
```

OR Top to Bottom
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int r = triangle.size();
        int c = triangle.get(r-1).size();
        int[] dp = new int[c];
        int[] temp = new int[c];
        Arrays.fill(dp, (int)1e9);
        dp[0]= triangle.get(0).get(0);
        for (int i = 1; i < r; i++) {
            temp[0] = dp[0];
            dp[0] += triangle.get(i).get(0);
            for (int j = 1; j < i; j++) {
                temp[j] = dp[j];
                dp[j] = Math.min(temp[j-1], dp[j]) + triangle.get(i).get(j);
            }
            dp[i] = temp[i-1] + triangle.get(i).get(i);
        }
        int res = dp[0];
        for (int i = 0; i < c; i++) {
            res = Math.min(res, dp[i]);
        }
        return res;
    }
}
```

OR

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        int dp[] =  new int[n+1];
        for (int i = n-1; i>=0; i--) {
            List<Integer> row = triangle.get(i);
            for (int j = 0; j < row.size(); j++) {
                dp[j] = row.get(j) + Math.min(dp[j], dp[j+1]);
            }
        }
        return dp[0];
    }
}
```