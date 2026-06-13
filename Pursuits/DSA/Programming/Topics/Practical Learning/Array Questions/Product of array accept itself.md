[238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = [1,2,3,4]
**Output:** [24,12,8,6]

**Example 2:**

**Input:** nums = [-1,1,0,-3,3]
**Output:** [0,0,9,0,0]

**Constraints:**

- `2 <= nums.length <= 105`
- `-30 <= nums[i] <= 30`
- The input is generated such that `answer[i]` is **guaranteed** to fit in a **32-bit** integer.

**Follow up:** Can you solve the problem in `O(1)` extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)


# Brute
TC-> O(2N)
SC-> O(N)
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int cnt=0;
        int n = nums.length;
        int prefixProduct[] = new int[n];
        int ans[] = new int[n];
        int pro = 1;
        for(int i=0;i<n;i++){
            pro*=nums[i];
            prefixProduct[i] = pro;
        }
        ans[n-1] = prefixProduct[n-2];
        int endPro = nums[n-1];
        for(int i=n-2;i>0;i--){
            ans[i] = prefixProduct[i-1] * endPro;
            endPro*=nums[i];
        }
        ans[0] = endPro;
        return ans;
    }
}
```


# Optimal 
TC -> O(2N)
SC -> O(1)
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int cnt=0;
        int n = nums.length;
        int ans[] = new int[n];
        int pro = 1;
        for(int i=0;i<n;i++){
            pro*=nums[i];
            ans[i] = pro;
        }
        ans[n-1] = ans[n-2];
        int endPro = nums[n-1];
        for(int i=n-2;i>0;i--){
            ans[i] = ans[i-1] * endPro;
            endPro*=nums[i];
        }
        ans[0] = endPro;
        return ans;
    }
}
```