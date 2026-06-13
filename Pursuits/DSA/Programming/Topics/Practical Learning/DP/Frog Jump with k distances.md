/[Link](https://takeuforward.org/plus/dsa/problems/frog-jump-with-k-distances)
Frog jump with K distances

A frog wants to climb a staircase with n steps. Given an integer array heights, where heights[i] contains the height of the ith step, and an integer k.

To jump from the ith step to the jth step, the frog requires **abs(heights[i] - heights[j])** energy, where abs() denotes the absolute difference. The frog can jump from the ith step to any step in the range [i + 1, i + k], provided it exists. Return the **minimum** amount of energy required by the frog to go from the 0th step to the (n-1)th step.

Examples:

**Input**: heights = [10, 5, 20, 0, 15], k = 2

**Output**: 15

**Explanation**:

0th step -> 2nd step, cost = abs(10 - 20) = 10

2nd step -> 4th step, cost = abs(20 - 15) = 5

Total cost = 10 + 5 = 15.

**Input**: heights = [15, 4, 1, 14, 15], k = 3

**Output**: 2

**Explanation**:

0th step -> 3rd step, cost = abs(15 - 14) = 1

3rd step -> 4th step, cost = abs(14 - 15) = 1

Total cost = 1 + 1 = 2.


# Using Memoization

```java
class Solution {
    private int helper(int[] heights,int k,int i,int[] memo){
        if(i==0)return 0;
        if(memo[i]!=-1)return memo[i];
        int ans = Integer.MAX_VALUE;
        for(int j=1;j<=k;j++){
            if(i-j<0)break;
            ans = Math.min(helper(heights,k,i-j,memo)+Math.abs(heights[i]-heights[i-j]),ans);
        }
        memo[i] = ans;
        return ans;
    }
    public int frogJump(int[] heights, int k) {
        int n = heights.length;
        int memo[] = new int[n];
        Arrays.fill(memo,-1);
        return helper(heights,k,n-1,memo);
    }
}
```


# Using Tabulation

```java
class Solution {
    public int frogJump(int[] heights, int k) {
        int n = heights.length;
        int dp[] = new int[n];
        dp[0] = 0;
        for(int i=1;i<n;i++){
            int minJmp=Integer.MAX_VALUE;
            for(int j=1;j<=k && i-j>=0;j++){
                int jump = Math.abs(heights[i]-heights[i-j])+dp[i-j];
                minJmp = Math.min(minJmp,jump);
            }
            dp[i] = minJmp;
        }
        return dp[n-1];
    }
}
```

OR

![[Pasted image 20250721103926.png|300]]

After optimizing space
we can make Space complexity upto O(k) but it will be better only if k< n

```java
class Solution {
    public int frogJump(int[] heights, int k) {
        int n = heights.length;
        int dp[] = new int[k+1];
        dp[0] = 0;
        for(int i=1;i<n;i++){
            int minJmp=Integer.MAX_VALUE;
            for(int j=1;j<=k && i-j>=0;j++){
                int prev=(i-j)%(k+1);
                int jump = Math.abs(heights[i]-heights[i-j])+dp[prev];
                minJmp = Math.min(minJmp,jump);
            }
            dp[i%(k+1)] = minJmp;
        }
        return dp[(n-1)%(k+1)];
    }
}
```


OR

```java
class Solution {
    public int frogJump(int[] heights, int k) {
        int n = heights.length;
        int dp[] = new int[k];
        dp[0] = 0;
        for(int i=1;i<n;i++){
            int minJmp=Integer.MAX_VALUE;
            for(int j=1;j<=k && i-j>=0;j++){
                int prev=(i-j)%k;
                int jump = Math.abs(heights[i]-heights[i-j])+dp[prev];
                minJmp = Math.min(minJmp,jump);
            }
            dp[i%k] = minJmp;
        }
        return dp[(n-1)%k];
    }
}
```