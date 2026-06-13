[33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return _the index of_ `target` _if it is in_ `nums`_, or_ `-1` _if it is not in_ `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [4,5,6,7,0,1,2], target = 0
**Output:** 4

**Example 2:**

**Input:** nums = [4,5,6,7,0,1,2], target = 3
**Output:** -1

**Example 3:**

**Input:** nums = [1], target = 0
**Output:** -1

**Constraints:**

- `1 <= nums.length <= 5000`
- `-104 <= nums[i] <= 104`
- All values of `nums` are **unique**.
- `nums` is an ascending array that is possibly rotated.
- `-104 <= target <= 104`


# Brute
**Time Complexity:** O(N), N = size of the given array.**Reason:** We have to iterate through the entire array to check if the target is present in the array.

**Space Complexity:** O(1)**Reason:** We have not used any extra data structures, this makes space complexity, even in the worst case as O(1).


# Optimal 
**Time Complexity:** O(logN), N = size of the given array.**Reason:** We are using binary search to search the target.

**Space Complexity:** O(1)**Reason:** We have not used any extra data structures, this makes space complexity, even in the worst case as O(1).

```java
class Solution {
    public int search(int[] nums, int target) {
        int i=0,j=nums.length-1;
        while(i<=j){
            int mid = i + (j-i)/2;
            if(nums[mid] == target) return mid;
            else if(nums[mid]>=nums[i]){
                if(target<nums[mid] && target>=nums[i]){
                    j = mid-1;
                }
                else{
                    i = mid+1;
                }
            }
            else if(target<=nums[j] && target > nums[mid]) i = mid+1;
            else j = mid-1;
        }
        return -1;
    }
}
```

```java
class Solution {
    public int search(int[] nums, int target) {
        int i=0,j=nums.length-1;
        while(i<=j){
            int mid = i + (j-i)/2;
            if(nums[mid] == target) return mid;
            else if(nums[mid]>=nums[i]){
                if(target<nums[mid] && target>=nums[i]){
                    j = mid-1;
                }
                else{
                    i = mid+1;
                }
            }
            else {
                if(target<=nums[j] && target>nums[mid]){
                    i = mid+1;
                }
                else{
                    j=mid-1;
                }
            }
        }
        return -1;
    }
}
```

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int n=nums.size();
        int low=0,high=n-1;
        int pivot=-1;
        while(low<=high){
            int mid= low + (high-low)/2;
            if(mid-1<0 && mid+1 >= n){
                pivot = mid;
                break;
            }
            else if(mid-1<0){
                if(nums[mid+1]>nums[mid]){
                    pivot = mid+1;break;
                }
                else{
                    pivot = mid;break;
                }
            }
            else if(mid+1>=n){
                if(nums[mid-1]>nums[mid]){
                    pivot = mid-1;break;
                }
                else{
                    pivot = mid;break;
                }
            }
            else if(nums[mid]>nums[mid-1] && nums[mid]>nums[mid+1]){
                pivot = mid; break;
            }
            else if(nums[mid]>nums[mid-1] && nums[mid]<nums[0]){
                high = mid-1;
            }
            else if(nums[mid]>nums[mid-1]){
                low = mid+1;
            }
            else if(nums[mid]<nums[mid-1]){
                high = mid-1;
            }
        }
        pivot++;
        
        pivot %=n;
        low=pivot;
        high=n-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid]==target){
                return mid;
            }
            else if(nums[mid]>target) high = mid-1;
            else low = mid+1;
        }
        high=pivot-1;
        if(high<0)return -1;
        low=0;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid]==target){
                return mid;
            }
            else if(nums[mid]>target) high = mid-1;
            else low = mid+1;
        }
        return -1;
    }
};
```