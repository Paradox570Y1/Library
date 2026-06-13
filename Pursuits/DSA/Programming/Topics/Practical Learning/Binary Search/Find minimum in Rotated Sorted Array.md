[153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
Suppose an array of length `n` sorted in ascending order is **rotated** between `1` and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

- `[4,5,6,7,0,1,2]` if it was rotated `4` times.
- `[0,1,2,4,5,6,7]` if it was rotated `7` times.

Notice that **rotating** an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` of **unique** elements, return _the minimum element of this array_.

You must write an algorithm that runs in `O(log n) time`.

**Example 1:**

**Input:** nums = [3,4,5,1,2]
**Output:** 1
**Explanation:** The original array was [1,2,3,4,5] rotated 3 times.

**Example 2:**

**Input:** nums = [4,5,6,7,0,1,2]
**Output:** 0
**Explanation:** The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

**Example 3:**

**Input:** nums = [11,13,15,17]
**Output:** 11
**Explanation:** The original array was [11,13,15,17] and it was rotated 4 times. 

**Constraints:**

- `n == nums.length`
- `1 <= n <= 5000`
- `-5000 <= nums[i] <= 5000`
- All the integers of `nums` are **unique**.
- `nums` is sorted and rotated between `1` and `n` times.

>Compare with the last element, if the mid element is bigger than the last that means it belongs to left half of rotated sorted array so you will do low = mid+1 and vice versa.

# Brute
```cpp
#include <bits/stdc++.h>
using namespace std;

int findMin(vector<int>& arr) {
    int n = arr.size(); // size of the array.
    int mini = INT_MAX;
    for (int i = 0; i < n; i++) {
        // Always keep the minimum.
        mini = min(mini, arr[i]);
    }
    return mini;
}

int main()
{
    vector<int> arr = {4, 5, 6, 7, 0, 1, 2, 3};
    int ans = findMin(arr);
    cout << "The minimum element is: " << ans << "\n";
    return 0;
}
```

# Optimal 

```java
class Solution {
    public int findMin(int[] nums) {
        int n  = nums.length;
        int low=0,high = n-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid]>nums[n-1]) low=mid+1;
            else high = mid-1;
        }
        return nums[low];
    }
}
```
- After observation
```java
class Solution {
    public int findMin(int[] nums) {
        int n  = nums.length;
        int low=0,high = n-1;
        int ans=2147483647;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid]>nums[high]) low=mid+1;
            else high = mid-1;
            ans = Math.min(nums[mid],ans);
        }
        return ans;
    }
}
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMin = function(nums) {
    let i=0,j=nums.length-1;
    if(nums[i]<=nums[j]) return nums[i];
    var ans = 2147482647;
    while(i<=j){
        let mid = (i+j)>>1;
        if(nums[mid]>=nums[i]){
            ans = ans>nums[i]? nums[i]:ans;
            i  = mid+1;
        }
        else{
            ans = ans>nums[mid]? nums[mid]:ans;
            j = mid-1;
        }
    }
    return ans;
};
```

- Striver's
```cpp
#include <bits/stdc++.h>
using namespace std;

int findMin(vector<int>& arr) {
    int low = 0, high = arr.size() - 1;
    int ans = INT_MAX;
    while (low <= high) {
        int mid = (low + high) / 2;
        //search space is already sorted
        //then arr[low] will always be
        //the minimum in that search space:
        if (arr[low] <= arr[high]) {
            ans = min(ans, arr[low]);
            break;
        }

        //if left part is sorted:
        if (arr[low] <= arr[mid]) {
            // keep the minimum:
            ans = min(ans, arr[low]);

            // Eliminate left half:
            low = mid + 1;
        }
        else { //if right part is sorted:

            // keep the minimum:
            ans = min(ans, arr[mid]);

            // Eliminate right half:
            high = mid - 1;
        }
    }
    return ans;
}

int main()
{
    vector<int> arr = {4, 5, 6, 7, 0, 1, 2, 3};
    int ans = findMin(arr);
    cout << "The minimum element is: " << ans << "\n";
    return 0;
}
```

- My first approach
```java
class Solution {
    public int findMin(int[] nums) {
        int n  = nums.length;
        int low=0,high = n-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(mid-1>=0 && mid+1<n){
                if(nums[mid]<nums[mid-1] && nums[mid]<nums[mid+1]) return nums[mid];
                else if(nums[mid]>nums[mid-1] && nums[mid]>nums[mid+1]) return nums[mid+1];
                else{
                    if(nums[mid]>nums[n-1]) low = mid+1;
                    else high = mid-1;
                }
            }
            else if(mid+1<n){
                return Math.min(nums[mid],nums[mid+1]);
            }
            else if(mid-1>0){
                return Math.min(nums[mid],nums[mid-1]);
            }
            else{
                return nums[mid];
            }

        }
        return -1;
    }
}
```

