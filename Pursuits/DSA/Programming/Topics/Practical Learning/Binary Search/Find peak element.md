[162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)

A peak element is an element that is strictly greater than its neighbors.

Given a **0-indexed** integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

**Example 1:**

**Input:** nums = [1,2,3,1]
**Output:** 2
**Explanation:** 3 is a peak element and your function should return the index number 2.

**Example 2:**

**Input:** nums = [1,2,1,3,5,6,4]
**Output:** 5
**Explanation:** Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.

**Constraints:**

- `1 <= nums.length <= 1000`
- `-231 <= nums[i] <= 231 - 1`
- `nums[i] != nums[i + 1]` for all valid `i`.


# Brute
```java
import java.util.*;

public class tUf {
    public static int findPeakElement(ArrayList<Integer> arr) {
        int n = arr.size(); // Size of array.

        for (int i = 0; i < n; i++) {
            // Checking for the peak:
            if ((i == 0 || arr.get(i - 1) < arr.get(i))
                    && (i == n - 1 || arr.get(i) > arr.get(i + 1))) {
                return i;
            }
        }
        // Dummy return statement
        return -1;
    }
}
```
# Optimal
```java
import java.util.*;
public class tUf {
    public static int findPeakElement(ArrayList<Integer> arr) {
        int n = arr.size(); // Size of array

        // Edge cases:
        if (n == 1) return 0;
        if (arr.get(0) > arr.get(1)) return 0;
        if (arr.get(n - 1) > arr.get(n - 2)) return n - 1;

        int low = 1, high = n - 2;
        while (low <= high) {
            int mid = (low + high) / 2;

            // If arr[mid] is the peak:
            if (arr.get(mid - 1) < arr.get(mid) && arr.get(mid) > arr.get(mid + 1))
                return mid;

            // If we are in the left:
            if (arr.get(mid) > arr.get(mid - 1)) low = mid + 1;

            // If we are in the right:
            // Or, arr[mid] is a common point:
            else high = mid - 1;
        }
        // Dummy return statement
        return -1;
    }
}
```

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int n =nums.length;
        int low=0,high=n-1;
        if(n==1) return 0;
        if(nums[low]>nums[low+1]) return low;
        if(nums[high]>nums[high-1])return high;
        low++;high--;
        while(low<=high){
            int  mid = low + (high-low)/2;
            if(nums[mid]>nums[mid-1] && nums[mid]>nums[mid+1]) return mid;
            else if(nums[mid+1]>=nums[mid-1])low=mid+1;
            else high=mid-1;
        }
        return -1;
    }
}
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findPeakElement = function(nums) {
    let n = nums.length;
    let low=0,high = n-1;
    if(n==1) return 0;
    if(nums[low]>nums[low+1])return low;
    if(nums[high]>nums[high-1])return high;
    low++;high--;
    while(low<=high){
        let mid = (low+high)>>1;
        if(nums[mid]>nums[mid-1] && nums[mid+1]<nums[mid])return mid;
        else if (nums[mid-1]<nums[mid])low = mid+1;
        else high =  mid-1;
    }
    return -1;
};
```