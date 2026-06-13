[1011. Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)

A conveyor belt has packages that must be shipped from one port to another within `days` days.

The `ith` package on the conveyor belt has a weight of `weights[i]`. Each day, we load the ship with packages on the conveyor belt (in the order given by `weights`). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within `days` days.

**Example 1:**

**Input:** weights = [1,2,3,4,5,6,7,8,9,10], days = 5
**Output:** 15
**Explanation:** A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.

**Example 2:**

**Input:** weights = [3,2,2,4,1,4], days = 3
**Output:** 6
**Explanation:** A ship capacity of 6 is the minimum to ship all the packages in 3 days like this:
1st day: 3, 2
2nd day: 2, 4
3rd day: 1, 4

**Example 3:**

**Input:** weights = [1,2,3,1,1], days = 4
**Output:** 3
**Explanation:**
1st day: 1
2nd day: 2
3rd day: 3
4th day: 1, 1

**Constraints:**

- `1 <= days <= weights.length <= 5 * 104`
- `1 <= weights[i] <= 500`


# Brute
```java
import java.util.*;
public class tUf {
    public static int findDays(int[] weights, int cap) {
        int days = 1; //First day.
        int load = 0;
        int n = weights.length; //size of array.
        for (int i = 0; i < n; i++) {
            if (load + weights[i] > cap) {
                days += 1; //move to next day
                load = weights[i]; //load the weight.
            } else {
                //load the weight on the same day.
                load += weights[i];
            }
        }
        return days;
    }

    public static int leastWeightCapacity(int[] weights, int d) {
        //Find the maximum and the summation:
        int maxi = Integer.MIN_VALUE, sum = 0;
        for (int i = 0; i < weights.length; i++) {
            sum += weights[i];
            maxi = Math.max(maxi, weights[i]);
        }

        for (int i = maxi; i <= sum; i++) {
            if (findDays(weights, i) <= d) {
                return i;
            }
        }
        //dummy return statement:
        return -1;
    }
}
```


# Optimal
**Time Complexity:** O(N * log(sum(weights[]) - max(weights[]) + 1)), where sum(weights[]) = summation of all the weights, max(weights[]) = maximum of all the weights, N = size of the weights array.  
**Reason:** We are applying binary search on the range [max(weights[]), sum(weights[])]. For every possible answer ‘mid’, we are calling findDays() function. Now, inside the findDays() function, we are using a loop that runs for N times.

**Space Complexity:** O(1) as we are not using any extra space to solve this problem.
```java
class Solution {
    int func(int[] arr,int n){
        int ans=1,load=0;
        for(int i=0;i<arr.length;i++){
            if(load+arr[i]>n){
                ans++;
                load = arr[i];
            }
            else{
                load += arr[i];
            }
        }
        return ans;
    }
    int maxsum(int[] weights){
        int sum=0;
        for(int i=0;i<weights.length;i++){
            sum += weights[i];
        }
        return sum;
    }
    int maxele(int[] weights){
        int l=-1;
        for(int i=0;i<weights.length;i++){
            l = Math.max(l,weights[i]);
        }
        return l;
    }
    public int shipWithinDays(int[] weights, int days) {
        int low = maxele(weights),high = maxsum(weights);
        int ans=-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int cnt = func(weights,mid);
            if(cnt<=days){
                ans = mid;
                high = mid-1;
            }
            else low = mid+1;
        }
        return ans;
    }
}
```

```java
class Solution {
    int func(int[] arr,int n){
        int ans=1,load=0;
        for(int i=0;i<arr.length;i++){
            if(load+arr[i]>n){
                ans++;
                load = arr[i];
            }
            else{
                load += arr[i];
            }
        }
        return ans;
    }

    public int shipWithinDays(int[] weights, int days) {
        int low=0,high=0;
        for(int i=0;i<weights.length;i++){
            low = Math.max(weights[i],low);
            high += weights[i];
        }
        while(low<=high){
            int mid = low + (high-low)/2;
            int cnt = func(weights,mid);
            if(cnt<=days){
                high = mid-1;
            }
            else low = mid+1;
        }
        return low;
    }
}
```