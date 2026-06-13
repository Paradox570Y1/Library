[992. Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/)

Given an integer array `nums` and an integer `k`, return _the number of **good subarrays** of_ `nums`.

A **good array** is an array where the number of different integers in that array is exactly `k`.

- For example, `[1,2,3,1,2]` has `3` different integers: `1`, `2`, and `3`.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

**Input:** nums = [1,2,1,2,3], k = 2
**Output:** 7
**Explanation:** Subarrays formed with exactly 2 different integers: [1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,1,2]

**Example 2:**

**Input:** nums = [1,2,1,3,4], k = 3
**Output:** 3
**Explanation:** Subarrays formed with exactly 3 different integers: [1,2,1,3], [2,1,3], [1,3,4].

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `1 <= nums[i], k <= nums.length`
# Better

```java
class Solution {
    public int subarraysWithKDistinct(int[] nums, int k) {
        int atmostK=0,lessThanK =0;
        int cnt=0;
        int i=0;
        HashMap<Integer,Integer> hs = new HashMap<>();
        for(int r=0;r<nums.length;r++){
            if(!hs.containsKey(nums[r])){
                hs.put(nums[r],1);
                cnt++;
            }
            else hs.put(nums[r],hs.get(nums[r])+1);
            while(cnt>k && i<=r){
                hs.put(nums[i],hs.get(nums[i])-1);
                if(hs.get(nums[i])==0){
                    hs.remove(nums[i]);
                    cnt--;
                }
                i++;
            }
            atmostK+= (r-i+1);
        }
        hs.clear();
        i=0;cnt=0;
        for(int r=0;r<nums.length;r++){
            if(!hs.containsKey(nums[r])){
                hs.put(nums[r],1);
                cnt++;
            }
            else hs.put(nums[r],hs.get(nums[r])+1);
            while(cnt==k && i<=r){
                hs.put(nums[i],hs.get(nums[i])-1);
                if(hs.get(nums[i])==0){
                    hs.remove(nums[i]);
                    cnt--;
                }
                i++;
            }
            lessThanK +=(r-i+1);
        }
        return atmostK-lessThanK;
    }
}
```


# Optimal

```java
class Solution {
    public int atmostK(int[] nums,int k){
        int n= nums.length;
        int left=0,cnt=0,ans=0;
        int hash[] = new int[n+1];
        for(int right=0;right<n;right++){
            if(hash[nums[right]]==0)cnt++;
            hash[nums[right]]++;
            while(cnt>k){
                hash[nums[left]]--;
                if(hash[nums[left]]==0)cnt--;
                left++;
            }
            ans += (right-left+1);
        }
        return ans;
    }
    public int subarraysWithKDistinct(int[] nums, int k) {
        return atmostK(nums,k)-atmostK(nums,k-1);
    }
}
```