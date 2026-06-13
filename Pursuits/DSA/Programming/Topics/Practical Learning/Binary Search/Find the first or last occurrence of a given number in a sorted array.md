
[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [5,7,7,8,8,10], target = 8
**Output:** [3,4]

**Example 2:**

**Input:** nums = [5,7,7,8,8,10], target = 6
**Output:** [-1,-1]

**Example 3:**

**Input:** nums = [], target = 0
**Output:** [-1,-1]

**Constraints:**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `nums` is a non-decreasing array.
- `-109 <= target <= 109`

# Brute
- Just for last Occurrence
- 
```cpp
#include<bits/stdc++.h>
using namespace std;
int solve(int n, int key, vector < int > & v) {
  int res = -1;
  for (int i = n - 1; i >= 0; i--) {
    if (v[i] == key) {
      res = i;
      break;
    }
  }
  return res;
}

int main() {
  int n = 7;
  int key = 13;
  vector < int > v = {3,4,13,13,13,20,40};
   
  // returning the last occurrence index if the element is present otherwise -1
  cout << solve(n, key, v) << "\n";

  return 0;
}
```
# Optimal 1
>First Occurrence => lower bound         
>Last Occurrence => upper bound-1


- Using Upper bound and Lower bound
```java
class Solution {
    int lb(int[] nums,int target){
        int low = 0,high=nums.length-1;
        int ans=nums.length;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid] >= target){
                ans = mid;
                high = mid-1;
            }
            else low = mid+1;
        }
        return ans;
    }
    int ub(int[] nums,int target){
        int low=0,high=nums.length-1,ans=nums.length;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid]>target){
                ans = mid;
                high = mid-1;
            }
            else low = mid+1;
        }
        return ans;
    }
    public int[] searchRange(int[] nums, int target) {
        int lb = lb(nums,target);
        if(lb==nums.length || nums[lb]!=target) return new int[]{-1,-1};
        else return new int[]{lb,ub(nums,target)-1};
    }
}
```


OR

```java
class Solution {
    private int upperBound(int[] nums,int i,int j,int x){
        int ans = j+1;
        while(i<=j){
            int mid = (i+j)>>1;
            if(nums[mid] > x){
                ans = mid;
                j = mid-1;
            }
            else i = mid+1;
        }
        return ans;
    }
    private int lowerBound(int[] nums,int i,int j,int x){
        int ans = j+1;
        while(i<=j){
            int mid = (i+j)>>1;
            if(nums[mid] >= x){
                ans = mid;
                j = mid-1;
            }
            else i = mid+1;
        }
        return ans;
    }
    public int[] searchRange(int[] nums, int target) {
        int n = nums.length;
        int i=0,j=n-1;
        int st = lowerBound(nums,i,j,target);
        if(st==n || nums[st] !=target)return new int[]{-1,-1};
        return new int[]{st,upperBound(nums,i,j,target) -1};
    }
}
```
# Optimal 2
- Using intuitive way

#### Algo for finding first & last Occurrence
```java
int first(int[] arr,int i,int j,int target){
        int ans = -1;
        while(i<=j){
            int mid = (i+j)/2;
            if(arr[mid] == target){
                ans = mid;
                j = mid-1;
            }
            else if(arr[mid] > target) j = mid-1;
            else i = mid+1;
        }
        return ans;
    }
int last(int[] arr,int i,int j,int target){
        int ans = -1;
        while(i<=j){
            int mid = (i+j)/2;
            if(arr[mid] == target){
                ans = mid;
                i = mid+1;
            }
            else if(arr[mid] > target) j = mid-1;
            else i = mid+1;
        }
        return ans;
    }
```


Code:
```cpp
class Solution {
public:
    int first(vector<int>& nums,int target){
        int low=0,high=nums.size()-1,ans=-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid] == target){
                ans = mid;
                high = mid-1;
            }
            else if(nums[mid]>target) high = mid-1;
            else low = mid+1;
        }
        return ans;
    }
    int last(vector<int>& nums, int target){
        int low=0,high=nums.size()-1,ans=-1;
        while(low<=high){
            int mid = low + (high -low)/2;
            if(nums[mid]==target){
                ans = mid;
                low = mid+1;
            }
            else if(nums[mid]<target) low = mid+1;
            else high = mid-1;
        }
        return ans;
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        int firstt = first(nums,target);
        if(firstt == -1) return {-1,-1};
        return {firstt,last(nums,target)};
    }
};
```
