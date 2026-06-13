[Link](https://www.geeksforgeeks.org/problems/number-of-occurrence2259/1)
Given a sorted array **Arr** of size **N** and a number **X**, you need to find the number of occurrences of **X** in **Arr**.

**Example 1:**

**Input:**
N = 7, X = 2
Arr[] = {1, 1, 2, 2, 2, 2, 3}
**Output:** 4
**Explanation:** x = 2 occurs 4 times in the given array so the output is 4.

**Example 2:**

**Input:**
N = 7, X = 4
Arr[] = {1, 1, 2, 2, 2, 2, 3}
**Output:** 0
**Explanation:** X = 4 is not present in the given array so the output is 0.

**Your Task:**  
You don't need to read input or print anything.  
Your task is to complete the function **count()** which takes the array of integers **arr,** **n,** and **x** as parameters and returns an integer denoting the answer.  
If x is not present in the array (arr) then return 0.

**Expected Time Complexity:** O(logN)  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
1 ≤ N ≤ 105  
1 ≤ Arr[i] ≤ 106  
1 ≤ X ≤ 106

# Optimal

```java
class Solution {
    int first(int[] nums,int target){
        int low=0,high=nums.length-1,ans=-1;
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
    int last(int[] nums, int target){
        int low=0,high=nums.length-1,ans=-1;
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
    int[] searchRange(int[] nums, int target) {
        int firstt = first(nums,target);
        if(firstt == -1) return new int[]{-1,-1};
        return new int[]{firstt,last(nums,target)};
    }
    int count(int[] arr, int n, int x) {
        // code here
        int ans[] = searchRange(arr,x);
        if(ans[0]==-1)return 0;
        else return ans[1]-ans[0]+1;
    }
}
```