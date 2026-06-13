[875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return _the minimum integer_ `k` _such that she can eat all the bananas within_ `h` _hours_.

**Example 1:**

**Input:** piles = [3,6,7,11], h = 8
**Output:** 4

**Example 2:**

**Input:** piles = [30,11,23,4,20], h = 5
**Output:** 30

**Example 3:**

**Input:** piles = [30,11,23,4,20], h = 6
**Output:** 23

**Constraints:**

- `1 <= piles.length <= 104`
- `piles.length <= h <= 109`
- `1 <= piles[i] <= 109`
# Brute
```java
import java.util.*;
public class tUf {
    public static int findMax(int[] v) {
        int maxi = Integer.MIN_VALUE;;
        int n = v.length;
        //find the maximum:
        for (int i = 0; i < n; i++) {
            maxi = Math.max(maxi, v[i]);
        }
        return maxi;
    }

    public static int calculateTotalHours(int[] v, int hourly) {
        int totalH = 0;
        int n = v.length;
        //find total hours:
        for (int i = 0; i < n; i++) {
            totalH += Math.ceil((double)(v[i]) / (double)(hourly));
        }
        return totalH;
    }

    public static int minimumRateToEatBananas(int[] v, int h) {
        //Find the maximum number:
        int maxi = findMax(v);

        //Find the minimum value of k:
        for (int i = 1; i <= maxi; i++) {
            int reqTime = calculateTotalHours(v, i);
            if (reqTime <= h) {
                return i;
            }
        }

        //dummy return statement
        return maxi;
    }
}
```
# Optimal

- Take cnt as long
```java
class Solution {
    long func(int[] arr,int n){
        long ans=0;
        for(int i=0;i<arr.length;i++){
            long rem = arr[i]%n;
            if(rem==0) ans += arr[i]/n;
            else ans += arr[i]/n + 1;
        }
        return ans;
    }
    public int minEatingSpeed(int[] piles, int h) {
        int l=-1;
        for(int i=0;i<piles.length;i++){
            l = Math.max(l,piles[i]);
        }
        if(l==-1)return 0;
        int low=1,high=l,ans=-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            long cal_h=func(piles,mid);
            if(cal_h<=h) {
                ans= mid;
                high=mid-1;
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
        int ans=0;
        for(int i=0;i<arr.length;i++){
            ans += Math.ceil((double)arr[i]/n);
        }
        return ans;
    }
    int findMax(int[] piles){
        int l=-1;
        for(int i=0;i<piles.length;i++){
            l = Math.max(l,piles[i]);
        }
        return l;
    }
    public int minEatingSpeed(int[] piles, int h) {
        int low=1,high=findMax(piles),ans=-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int cal_h=func(piles,mid);
            if(cal_h<=h) {
                ans= mid;
                high=mid-1;
            }
            else low = mid+1;
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    private long getTime(int[] piles,int rate){
        long cnt=0;
        for(int pile:piles){
            cnt += (pile+rate-1)/rate; 
        }
        return cnt;
    }
    public int minEatingSpeed(int[] piles, int h) {
        int n  = piles.length;
        int low =1,high=Integer.MIN_VALUE;
        for(int i=0;i<n;i++){
            high = Math.max(high,piles[i]);
        }
        int ans=-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            long cal_hr = getTime(piles,mid);
            if(cal_hr<=h){
                ans = mid;
                high = mid-1;
            }
            else low = mid+1;
        }
        return ans;
    }
}
```


>**NOTE**
>To do Ceil without using library function
> `Math.ceil((double)pile/rate)` is equivalent to `(pile+rate-1)/rate` 