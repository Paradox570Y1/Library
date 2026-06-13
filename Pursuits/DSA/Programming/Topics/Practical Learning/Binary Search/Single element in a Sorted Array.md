[540. Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/)

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return _the single element that appears only once_.

Your solution must run in `O(log n)` time and `O(1)` space.

**Example 1:**

**Input:** nums = [1,1,2,3,3,4,4,8,8]
**Output:** 2

**Example 2:**

**Input:** nums = [3,3,7,7,10,11,11]
**Output:** 10

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 105`


# Better
```java
import java.util.*;

public class tUf {
    public static int singleNonDuplicate(ArrayList<Integer> arr) {
        int n = arr.size(); //size of the array.
        int ans = 0;
        // XOR all the elements:
        for (int i = 0; i < n; i++) {
            ans = ans ^ arr.get(i);
        }
        return ans;
    }
```
# Optimal


```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int n=nums.length;
        int low =0,high=n-1;
        while(low<high){
            int mid = low + (high-low)/2;
            if(nums[mid+1]>nums[mid]){
                if(mid%2==1) low=mid+1;
                else high = mid;
            }
            else{
                if(mid%2==0) low=mid;
                else high=mid-1;
            }
        }
        return nums[low];
    }
}
```

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int n=nums.length;
        int low =0,high=n-1;
        while(low<high){
            int mid = low + (high-low)/2;
            if(nums[mid+1]>nums[mid]){
                if((n-1 - mid-1)%2==0) low=mid+1;
                else high = mid;
            }
            else{
                if((n-1 - mid)%2==1) high = mid-1;
                else low = mid;
            }
        }
        return nums[low];
    }
}
```
![[Pasted image 20240925233949.png|400]]

```cpp
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int n = nums.size();
        if(n==1)return nums[0];
        if(nums[0]!=nums[1]) return nums[0];
        if(nums[n-1]!= nums[n-2]) return nums[n-1];
        int low = 1,high=n-2;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid]!=nums[mid-1] && nums[mid]!=nums[mid+1]) return nums[mid];
            else if((mid%2==1 && nums[mid]==nums[mid-1]) || (mid%2==0 && nums[mid]==nums[mid+1])) low=mid+1;
            else high = mid-1;
        }
        return -1;
    }
};
```

OR

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int n = nums.length;
        int low = 0,high = n-1;
        while(low<=high){
            int mid = (low+high)/2;
            if(mid>0 && nums[mid-1]==nums[mid]){
                if(mid%2==1) low = mid+1;
                else high = mid-1;
            }
            else{
                if(mid%2==0)low = mid+1;
                else high = mid-1;
            }
        }
        return nums[high];
    }
}
```
