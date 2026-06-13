[55. Jump Game](https://leetcode.com/problems/jump-game/)

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` _if you can reach the last index, or_ `false` _otherwise_.

**Example 1:**

**Input:** nums = [2,3,1,1,4]
**Output:** true
**Explanation:** Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [3,2,1,0,4]
**Output:** false
**Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

**Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 105`


# Using recursion
TLE
```java
class Solution {
    public boolean helper(int[] nums,int i){
        if(i==nums.length-1)return true;
        int steps = nums[i];
        for(int j=1;j<=steps;j++){
            if(helper(nums,j+i))return true;
        }
        return false;
    }
    public boolean canJump(int[] nums) {
        return helper(nums,0);
    }
}
```


# Using Memoization

```java
class Solution {
    public boolean helper(int[] nums,int i,Boolean[] memo){
        if(i==nums.length-1)return true;
        if(memo[i]!=null)return memo[i];
        int steps = nums[i];
        for(int j=1;j<=steps;j++){
            if(helper(nums,j+i,memo)){
                memo[i] = true;
                return true;
            }
        }
        memo[i] = false;
        return false;
    }
    public boolean canJump(int[] nums) {
        Boolean memo[] = new Boolean[nums.length];
        //by default null is stored
        return helper(nums,0,memo);
    }
}
```

```java
class Solution {
    public boolean helper(int[] nums,int i,int[] memo){
        if(i==nums.length-1)return true;
        if(memo[i]!=0)return memo[i]==1;
        int steps = nums[i];
        for(int j=1;j<=steps;j++){
            if(helper(nums,j+i,memo)){
                memo[i] = 1;
                return true;
            }
        }
        memo[i] = -1;
        return false;
    }
    public boolean canJump(int[] nums) {
        int memo[] = new int[nums.length];
        return helper(nums,0,memo);
    }
}
```


# Using Tabulation (Bottom Up DP)

Most optimal
```java
class Solution {
    public boolean canJump(int[] nums) {
        int n =nums.length;
        int reach = n-1;
        for(int i=n-2;i>=0;i--){
            if(i+nums[i]>=reach){
                reach = i;
            }
        }
        return reach==0;
    }
}
```


# Using greedy

```java
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int max = 0;
        for(int i=0;i<n;i++){
            if(i>max)return false;
            max = Math.max(max,i+nums[i]);
        }
        return true;
    }
}
```
Better than above greedy code
```java
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int max = 0;
        int i=0;
        for(;i<n && i<=max;i++){
            max = Math.max(max,i+nums[i]);
        }
        return i==n;
    }
}
```