[410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)
Given an integer array `nums` and an integer `k`, split `nums` into `k` non-empty subarrays such that the largest sum of any subarray is **minimized**.

Return _the minimized largest sum of the split_.

A **subarray** is a contiguous part of the array.

**Example 1:**

**Input:** nums = [7,2,5,10,8], k = 2
**Output:** 18
**Explanation:** There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8], where the largest sum among the two subarrays is only 18.

**Example 2:**

**Input:** nums = [1,2,3,4,5], k = 2
**Output:** 9
**Explanation:** There are four ways to split nums into two subarrays.
The best way is to split it into [1,2,3] and [4,5], where the largest sum among the two subarrays is only 9.

**Constraints:**

- `1 <= nums.length <= 1000`
- `0 <= nums[i] <= 106`
- `1 <= k <= min(50, nums.length)`


# Brute
```java



import java.util.*;

public class tUf {
    public static int countPartitions(int[] a, int maxSum) {
        int n = a.length; //size of array.
        int partitions = 1;
        long subarraySum = 0;
        for (int i = 0; i < n; i++) {
            if (subarraySum + a[i] <= maxSum) {
                //insert element to current subarray
                subarraySum += a[i];
            } else {
                //insert element to next subarray
                partitions++;
                subarraySum = a[i];
            }
        }
        return partitions;
    }

    public static int largestSubarraySumMinimized(int[] a, int k) {
        int low = a[0];
        int high = 0;
        //find maximum and summation:
        for (int i = 0; i < a.length; i++) {
            low = Math.max(low, a[i]);
            high += a[i];
        }

        for (int maxSum = low; maxSum <= high; maxSum++) {
            if (countPartitions(a, maxSum) == k)
                return maxSum;
        }
        return low;
    }
}
```

# Optimal
```cpp
class Solution {
public:
    int func(vector<int>& nums, int size){
        int cnt=1,sum=0;
        for(int i=0;i<nums.size();i++){
            if(sum+nums[i]<=size) sum += nums[i];
            else{
                cnt++;
                sum = nums[i];
            }
        }
        return cnt;
    }
    int splitArray(vector<int>& nums, int k) {
        int low= *max_element(nums.begin(),nums.end());
        int high = accumulate(nums.begin(),nums.end(),0);
        if(nums.size()<k) return -1;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(func(nums,mid)>k) low = mid+1;
            else high = mid-1;
        }
        return low;
    }
};

```

```cpp
class Solution {
public:
    int func(vector<int>& nums, int size){
        int cnt=1,sum=0;
        for(int i=0;i<nums.size();i++){
            if(sum+nums[i]<=size) sum += nums[i];
            else{
                cnt++;
                sum = nums[i];
            }
        }
        return cnt;
    }
    int splitArray(vector<int>& nums, int k) {
        int low=INT_MIN,high=0;
        for(int i=0;i<nums.size();i++){
            low = max(low,nums[i]);
            high += nums[i];
        }
        if(nums.size()<k) return -1;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(func(nums,mid)<=k) high = mid-1;
            else low = mid+1;
        }
        return low;
    }
};
```