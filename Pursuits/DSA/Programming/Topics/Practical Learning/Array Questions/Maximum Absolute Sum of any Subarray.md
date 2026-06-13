[1749. Maximum Absolute Sum of Any Subarray](https://leetcode.com/problems/maximum-absolute-sum-of-any-subarray/)

You are given an integer array `nums`. The **absolute sum** of a subarray `[numsl, numsl+1, ..., numsr-1, numsr]` is `abs(numsl + numsl+1 + ... + numsr-1 + numsr)`.

Return _the **maximum** absolute sum of any **(possibly empty)** subarray of_ `nums`.

Note that `abs(x)` is defined as follows:

- If `x` is a negative integer, then `abs(x) = -x`.
- If `x` is a non-negative integer, then `abs(x) = x`.

**Example 1:**

**Input:** nums = [1,-3,2,3,-4]
**Output:** 5
**Explanation:** The subarray [2,3] has absolute sum = abs(2+3) = abs(5) = 5.

**Example 2:**

**Input:** nums = [2,-5,1,-4,3,-2]
**Output:** 8
**Explanation:** The subarray [-5,1,-4] has absolute sum = abs(-5+1-4) = abs(-8) = 8.

**Constraints:**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`


# Brute

```java
class Solution {
    public int maxAbsoluteSum(int[] nums) {
        int sum=0;
        int maxi =0;
        int mini=0;
        int sub=0;
        for(int i=0;i<nums.length;i++){
            sum=Math.max(sum+nums[i],nums[i]);
            maxi= Math.max(maxi,sum);
            sub=Math.min(sub+nums[i],nums[i]);
            mini = Math.min(sub,mini);
        }
        return Math.max(Math.abs(mini),maxi);
    }
}
```

# Better

```java
class Solution {
    public int maxAbsoluteSum(int[] nums) {
        int s1=0;
        int maxi =0;
        int mini=0;
        int s2=0;
        for(int i=0;i<nums.length;i++){
            s1+=nums[i];
            s2+=nums[i];
            if(s1<0)s1=0;
            if(s2>0)s2=0;
            if(maxi<s1)maxi = s1;
            if(mini>s2)mini = s2;
        }
        return Math.max(Math.abs(mini),maxi);
    }
}
```


# Optimal

```java
class Solution {
    public int maxAbsoluteSum(int[] nums) {
        int sum=nums[0];
        int maxi =0;
        int mini=0;
        if(maxi<nums[0])maxi = nums[0];
        if(mini>nums[0])mini = nums[0];
        for(int i=1;i<nums.length;i++){
            sum+=nums[i];
            if(maxi<sum)maxi = sum;
            if(mini>sum)mini = sum;
        }
        System.out.println(maxi);
        System.out.println(mini);
        return Math.abs(maxi-mini);
    }
}
```