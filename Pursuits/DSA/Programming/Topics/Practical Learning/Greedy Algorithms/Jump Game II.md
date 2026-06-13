[45. Jump Game II](https://leetcode.com/problems/jump-game-ii/)

You are given a **0-indexed** array of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. In other words, if you are at `nums[i]`, you can jump to any `nums[i + j]` where:

- `0 <= j <= nums[i]` and
- `i + j < n`

Return _the minimum number of jumps to reach_ `nums[n - 1]`. The test cases are generated such that you can reach `nums[n - 1]`.

**Example 1:**

**Input:** nums = [2,3,1,1,4]
**Output:** 2
**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [2,3,0,1,4]
**Output:** 2

**Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 1000`
- It's guaranteed that you can reach `nums[n - 1]`.




# Using recursion

```java
class Solution {
    public int helper(int[] nums,int jump,int i){
        if(i==nums.length-1)return jump;
        int min = nums.length+1;
        for(int j=i+1;j<=i+nums[i] && j<nums.length;j++){
            min = Math.min(min,helper(nums,jump+1,j));
        }
        return min;
    }
    public int jump(int[] nums) {
        return helper(nums,0,0);
    }
}
```

OR

```java
class Solution {
    public int helper(int[] nums,int jump,int i){
        if(i>=nums.length-1)return jump;
        int min = nums.length+1;
        for(int j=1;j<=nums[i];j++){
            min = Math.min(min,helper(nums,jump+1,i+j));
        }
        return min;
    }
    public int jump(int[] nums) {
        return helper(nums,0,0);
    }
}
```
# Using Memoization
TC-> O(2\*N²)
SC-> O(N²)
```java
class Solution {
    public int helper(int[] nums,int jump,int i,int[][] memo){
        if(i>=nums.length-1)return jump;
        if(memo[i][jump]!=-1)return memo[i][jump];
        int min = nums.length+1;
        for(int j=1;j<=nums[i];j++){
            min = Math.min(min,helper(nums,jump+1,i+j,memo));
        }
        memo[i][jump] = min;
        return min;
    }
    public int jump(int[] nums) {
        int n = nums.length;
        int[][] memo = new int[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                memo[i][j] = -1;
            }
        }
        return helper(nums,0,0,memo);
    }
}
```

# Using tabulation
TC-> O(N²)
SC-> O(N)
```java
class Solution {
    public int jump(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        dp[n-1] = 0;
        for(int i=n-2;i>=0;i--){
            if(i+nums[i]>=n-1)dp[i] = 1;
            else if(nums[i]+i==i)dp[i] = n;
            else{
                int mini=n;
                for(int j=i+1;j<=i+nums[i];j++){
	                if(j>n-1)break;
                    mini = Math.min(mini,dp[j]);
                }
                dp[i] = mini+1;
            }
        }
        return dp[0];
    }
}
```


# Using Greedy
TC-> O(N)
```java
class Solution {
    public int jump(int[] nums) {
        int n = nums.length;
        if(n==1)return 0;
        int scope = nums[0];
        int max=0;
        int cnt=1;
        for(int i=1;i<n;i++){
            if(i<=scope){
                if(i==n-1)return cnt;
                max = Math.max(max,i+nums[i]);
                if(i==scope){
                    scope = max;
                    max=0;
                    cnt++;
                }
            }
        }
        return -1;
    }
}
```

TC-> O(N)
Better runtime
```java
class Solution {
    public int jump(int[] nums) {
        int n = nums.length;
        int left = 0, right = 0;
        int jump = 0, largest = 0;
        while(right<n-1){
            largest = 0;
            for(int i=left;i<=right;i++){
                largest = Math.max(largest,nums[i]+i);
            }
            left = right+1;
            right = largest;
            jump++;
        }
        return jump;
    }
}
```