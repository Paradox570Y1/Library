[1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

Given a binary array `nums` and an integer `k`, return _the maximum number of consecutive_ `1`_'s in the array if you can flip at most_ `k` `0`'s.

**Example 1:**

**Input:** nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
**Output:** 6
**Explanation:** [1,1,1,0,0,**1**,1,1,1,1,**1**]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

**Example 2:**

**Input:** nums = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], k = 3
**Output:** 10
**Explanation:** [0,0,1,1,**1**,**1**,1,1,1,**1**,1,1,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

**Constraints:**

- `1 <= nums.length <= 105`
- `nums[i]` is either `0` or `1`.
- `0 <= k <= nums.length`



# Brute

```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        int n = nums.length;
        int maxi=0;
        for(int i=0;i<n;i++){
            int cnt=0;
            for(int j=i;j<n;j++){
                if(nums[j]==0)cnt++;
                if(cnt<=k) maxi = Math.max(maxi,j-i+1);
                else break;
            }
        }
        return maxi;
    }
}
```


# Better
TC-> O(2N)
SC-> O(1)
```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        int n = nums.length;
        int maxi=0;
        int j=0;
        int cnt=0;
        for(int i=0;i<n;i++){
            if(nums[i]==0)cnt++;
            while(cnt>k){
                if(nums[j]==0){
                    cnt--;
                }
                j++;
            }
            maxi = Math.max(maxi,i-j+1);
        }
        return maxi;
    }
}
```


# Optimal
TC -> O(N)
SC -> O(1)
```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        int n = nums.length;
        int maxi=0;
        int j=0;
        int cnt=0;
        for(int i=0;i<n;i++){
            if(nums[i]==0)cnt++;
            if(cnt>k){
                if(nums[j]==0)cnt--;
                j++;
            }
            else maxi = Math.max(maxi,i-j+1);
        }
        return maxi;
    }
}
```