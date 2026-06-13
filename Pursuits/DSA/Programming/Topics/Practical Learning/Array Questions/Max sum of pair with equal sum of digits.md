[2342. Max Sum of a Pair With Equal Sum of Digits](https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits/)

You are given a **0-indexed** array `nums` consisting of **positive** integers. You can choose two indices `i` and `j`, such that `i != j`, and the sum of digits of the number `nums[i]` is equal to that of `nums[j]`.

Return _the **maximum** value of_ `nums[i] + nums[j]` _that you can obtain over all possible indices_ `i` _and_ `j` _that satisfy the conditions._

**Example 1:**

**Input:** nums = [18,43,36,13,7]
**Output:** 54
**Explanation:** The pairs (i, j) that satisfy the conditions are:
- (0, 2), both numbers have a sum of digits equal to 9, and their sum is 18 + 36 = 54.
- (1, 4), both numbers have a sum of digits equal to 7, and their sum is 43 + 7 = 50.
So the maximum sum that we can obtain is 54.

**Example 2:**

**Input:** nums = [10,12,19,14]
**Output:** -1
**Explanation:** There are no two numbers that satisfy the conditions, so we return -1.

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`



```java
class Solution {
    private int sumDigit(int n){
        int ans=0;
        while(n>0){
            ans+=n%10;
            n/=10;
        }
        return ans;
    }
    public int maximumSum(int[] nums) {
        if(nums.length==1)return -1;
        HashMap<Integer,Integer> hm = new HashMap<>();
        hm.put(sumDigit(nums[0]),0);
        int maxi=-1;
        for(int i=1;i<nums.length;i++){
            int cur = sumDigit(nums[i]);
            if(hm.containsKey(cur)){
                int idx = hm.get(cur);
                if(maxi<nums[idx]+nums[i])maxi = nums[idx]+nums[i];
                if(nums[idx]<nums[i])hm.put(cur,i);
            }
            else hm.put(cur,i);
        }
        return maxi;
    }
}
```