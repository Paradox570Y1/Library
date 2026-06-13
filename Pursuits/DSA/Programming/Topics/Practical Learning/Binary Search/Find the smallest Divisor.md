[Link](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/)
Given an array of integers `nums` and an integer `threshold`, we will choose a positive integer `divisor`, divide all the array by it, and sum the division's result. Find the **smallest** `divisor` such that the result mentioned above is less than or equal to `threshold`.

Each result of the division is rounded to the nearest integer greater than or equal to that element. (For example: `7/3 = 3` and `10/2 = 5`).

The test cases are generated so that there will be an answer.

**Example 1:**

**Input:** nums = [1,2,5,9], threshold = 6
**Output:** 5
**Explanation:** We can get a sum to 17 (1+2+5+9) if the divisor is 1. 
If the divisor is 4 we can get a sum of 7 (1+1+2+3) and if the divisor is 5 the sum will be 5 (1+1+1+2). 

**Example 2:**

**Input:** nums = [44,22,33,11,1], threshold = 5
**Output:** 44

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `1 <= nums[i] <= 106`
- `nums.length <= threshold <= 106`

# Brute
```java
import java.util.*;

public class tUf {
    public static int smallestDivisor(int[] arr, int limit) {
        int n = arr.length; //size of array.
        //Find the maximum element:
        int maxi = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            maxi = Math.max(maxi, arr[i]);
        }

        //Find the smallest divisor:
        for (int d = 1; d <= maxi; d++) {
            //Find the summation result:
            int sum = 0;
            for (int i = 0; i < n; i++) {
                sum += Math.ceil((double)(arr[i]) / (double)(d));
            }
            if (sum <= limit)
                return d;
        }
        return -1;
    }
}
```

# Optimal

```java
class Solution {
    public int func(int[] arr,int mid){
        int cnt = 0;
        for(int i=0;i<arr.length;i++){
            cnt += Math.ceil(arr[i]/(double)mid);
        }
        return cnt;
    }
    public int smallestDivisor(int[] nums, int threshold) {
        int low=1,high= Arrays.stream(nums).max().getAsInt();
        int ans=-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int cnt = func(nums,mid);
            if(cnt<=threshold){
                ans = mid;
                high = mid -1;
            } 
            else {
                low = mid+1;
            }
        }
        return ans;
    }
}
```

```java
class Solution {
    public int func(int[] arr,int mid){
        int cnt = 0;
        for(int i=0;i<arr.length;i++){
            int x = arr[i]/mid;
            cnt += x;
            if(x*mid != arr[i])cnt++;
        }
        return cnt;
    }
    public int calMax(int[]arr){
        int maxi =-2147483648;
        for(int i=0;i<arr.length;i++){
            maxi = maxi<arr[i]? arr[i]: maxi;
        }
        return maxi;
    }
    public int smallestDivisor(int[] nums, int threshold) {
        int low=1,high= calMax(nums);
        int ans=-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int cnt = func(nums,mid);
            if(cnt<=threshold){
                ans = mid;
                high = mid -1;
            } 
            else {
                low = mid+1;
            }
        }
        return ans;
    }
}
```

```
```cpp
class Solution {
public:
    int func(vector<int> v,int n,int threshold){
        int ans=0;
        for(int i=0;i<v.size();i++){
            ans += ceil((double)v[i]/(double)n);
        }
        if(ans==threshold)return 1;
        else if(ans<threshold)return 2;
        return 0;
    }
    int smallestDivisor(vector<int>& nums, int threshold) {
        int low=1,high = *max_element(nums.begin(),nums.end());
        int ans=high;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(func(nums,mid,threshold)>=1){
                ans=mid;
                high=mid-1;
            }
            else low = mid+1;
        }
        return ans;
    }
};
```