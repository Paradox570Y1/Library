[70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

**Input:** n = 2
**Output:** 2
**Explanation:** There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

**Example 2:**

**Input:** n = 3
**Output:** 3
**Explanation:** There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

**Constraints:**

- `1 <= n <= 45`

# Brute

```java
class Solution {
    private int cnt=0;
    private void helper(int i){
        if(i<0)return;
        if(i==0){
            cnt++;
            return;
        }
        helper(i-1);
        helper(i-2);
    }
    public int climbStairs(int n) {
        helper(n);
        return cnt;
    }
}
```

OR

```java
class Solution {
    private int helper(int i,int cnt){
        if(i<=0){
            if(i==0)cnt++;
            return cnt;
        }
        return helper(i-1,cnt)+helper(i-2,cnt);
    }
    public int climbStairs(int n) {
        return helper(n,0);
    }
}
```

OR

```java
class Solution {
    private int helper(int i){
        if(i==0 || i==1)return 1;
        return helper(i-1)+helper(i-2);
    }
    public int climbStairs(int n) {
        return helper(n);
    }
}
```

# Using Memoization

```java
class Solution {
    private int helper(int i,int cnt,int[] memo){
        if(i<=0){
            if(i==0)cnt++;
            return cnt;
        }
        if(memo[i]!=0)return memo[i];
        return memo[i] = helper(i-1,cnt,memo) + helper(i-2,cnt,memo);
    }
    public int climbStairs(int n) {
        int memo[] = new int[n+1];
        return helper(n,0,memo);
    }
}
```

OR

```java
class Solution {
    private int helper(int i,int[] memo){
        if(i==0 || i==1)return 1;
        if(memo[i]!=0)return memo[i];
        return memo[i] = helper(i-1,memo)+helper(i-2,memo);
    }
    public int climbStairs(int n) {
        int memo[] = new int[n+1];
        return helper(n,memo);
    }
}
```
# Using Tabulation

```java
class Solution {
    public int climbStairs(int n) {
        int dp[] = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i=2;i<n+1;i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```

OR

After Optimizing space
```java
class Solution {
    public int climbStairs(int n) {
        int prev1=1;
        int prev2=1;
        for(int i=2;i<n+1;i++){
            int cur = prev1 + prev2;
            prev2 = prev1;
            prev1 = cur;
        }
        return prev1;
    }
}
```