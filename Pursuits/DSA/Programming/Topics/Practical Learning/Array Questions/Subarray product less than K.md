[713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)

Given an array of integers `nums` and an integer `k`, return _the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than_ `k`.

**Example 1:**

**Input:** nums = [10,5,2,6], k = 100
**Output:** 8
**Explanation:** The 8 subarrays that have product less than 100 are:
[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.

**Example 2:**

**Input:** nums = [1,2,3], k = 0
**Output:** 0

**Constraints:**

- `1 <= nums.length <= 3 * 104`
- `1 <= nums[i] <= 1000`
- `0 <= k <= 106`

```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        int pro=1;
        int cnt=0;
        int j=0;
        int  n= nums.length;
        for(int i=0;i<n;i++){
            pro*=nums[i];
            while(pro>=k && j<nums.length && pro!=1){
                pro/=nums[j];
                j++;
            }
            if(pro<k)cnt += i-j+1;
        }
        return cnt;
    }
}
```