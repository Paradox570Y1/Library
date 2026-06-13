[Link](https://www.geeksforgeeks.org/problems/rotation4723/1)
Given an increasing sorted rotated array **arr** of distinct integers. The array is right-rotated **k** times. Find the value of **k**.  
Let's suppose we have an array arr = [2, 4, 6, 9], so if we rotate it by 2 times so that it will look like this:  
After 1st Rotation : [9, 2, 4, 6]  
After 2nd Rotation : [6, 9, 2, 4]

**Examples:**

**Input:** arr = [5, 1, 2, 3, 4]
**Output:** 1
**Explanation:** The given array is 5 1 2 3 4. The original sorted array is 1 2 3 4 5. We can see that the array was rotated 1 times to the right.  

**Input:** arr = [1, 2, 3, 4, 5]
**Output:** 0
**Explanation:** The given array is not rotated.

**Expected Time Complexity:** O(log(n))  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
1 <= n <=105  
1 <= arri <= 107

# Optimal
```java
class Solution {
    public int findKRotation(List<Integer> arr) {
        // Code here
        int n= arr.size();
        int low =0,high = n-1;
        int ans=2147483647,check=2147483647;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(arr.get(mid)>arr.get(high)) low = mid+1;
            else high =mid-1;
            if(arr.get(mid)<check){
                check=arr.get(mid);
                ans = mid;
            }
        }
        return ans;
    }
}
```


OR

```java
class Solution {
    public int findKRotation(List<Integer> arr) {
        // Code here
        int n = arr.size();
        int i=0,j=n-1;
        while(i<=j){
            int mid = (i+j)/2;
            if(arr.get(mid)>arr.get(n-1)){
                i=mid+1;
            }
            else j=mid-1;
        }
        return i;
    }
}
```