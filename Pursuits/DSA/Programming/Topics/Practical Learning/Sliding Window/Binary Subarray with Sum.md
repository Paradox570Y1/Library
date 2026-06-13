[930. Binary Subarrays With Sum](https://leetcode.com/problems/binary-subarrays-with-sum/)

Given a binary array `nums` and an integer `goal`, return _the number of non-empty **subarrays** with a sum_ `goal`.

A **subarray** is a contiguous part of the array.

**Example 1:**

**Input:** nums = [1,0,1,0,1], goal = 2
**Output:** 4
**Explanation:** The 4 subarrays are bolded and underlined below:
[**1,0,1**,0,1]
[**1,0,1,0**,1]
[1,**0,1,0,1**]
[1,0,**1,0,1**]

**Example 2:**

**Input:** nums = [0,0,0,0,0], goal = 0
**Output:** 15

**Constraints:**

- `1 <= nums.length <= 3 * 104`
- `nums[i]` is either `0` or `1`.
- `0 <= goal <= nums.length`

# Brute
TC-> O(N²)
SC-> O(1)
```java
class Solution {
    public int numSubarraysWithSum(int[] nums, int goal) {
        int n = nums.length;
        int cnt=0;
        for(int i=0;i<n;i++){
            int sum=0;
            for(int j=i;j<n;j++){
                sum+=nums[j];
                if(sum==goal)cnt++;
            }
        }
        return cnt;
    }
}
```


# Better
TC-> O(N)
SC-> O(N)
```java
class Solution {
    public int numSubarraysWithSum(int[] nums, int goal) {
        int n = nums.length;
        int cnt=0;
        int sum=0;
        HashMap<Integer,Integer> hm = new HashMap<>();
        hm.put(0,1);
        for(int i=0;i<n;i++){
            sum+=nums[i];
            int rest = sum-goal;
            if(hm.containsKey(rest)){
                cnt+=hm.get(rest);
            }
            hm.put(sum,hm.getOrDefault(sum,0)+1);
        }
        return cnt;
    }
}
```


# Optimal
TC-> O(2N)
SC-> O(1)

> Note : In sliding window if array contains 0 or duplicates then traditional way of counting subarrays having target k doesn't work.
> Then try counting at most k target and subtract by at most k-1


```java
class Solution {
    private int atmostK(int nums[],int goal){
        if(goal<0)return 0; //if goal becomes -ve for goal-1
        int cnt=0;
        int sum=0;
        int j=0;
        int n = nums.length;
        for(int i=0;i<n;i++){
            sum+=nums[i];
            while(j<n && sum>goal){
                sum-=nums[j++];
            }
            cnt+=(i-j+1);
        }
        return cnt;
    }
    public int numSubarraysWithSum(int[] nums, int goal) {
        return atmostK(nums,goal)-atmostK(nums,goal-1);
    }
}
```