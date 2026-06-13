[1248. Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/)

Given an array of integers `nums` and an integer `k`. A continuous subarray is called **nice** if there are `k` odd numbers on it.

Return _the number of **nice** sub-arrays_.

**Example 1:**

**Input:** nums = [1,1,2,1,1], k = 3
**Output:** 2
**Explanation:** The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].

**Example 2:**

**Input:** nums = [2,4,6], k = 1
**Output:** 0
**Explanation:** There are no odd numbers in the array.

**Example 3:**

**Input:** nums = [2,2,2,1,2,2,1,2,2,2], k = 2
**Output:** 16

**Constraints:**

- `1 <= nums.length <= 50000`
- `1 <= nums[i] <= 10^5`
- `1 <= k <= nums.length`

# Less Better
TC-> O(N)
SC-> O(N) of HashMap
```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        int n= nums.length;
        int sum=0;
        int cnt=0;
        HashMap<Integer,Integer> hm = new HashMap<>();
        hm.put(0,1);
        for(int i=0;i<n;i++){
            sum+= nums[i]&1;
            if(hm.containsKey(sum-k)){
                cnt+=hm.get(sum-k);
            }
            hm.put(sum,hm.getOrDefault(sum,0)+1);
        }
        return cnt;
    }
}
```

# Better

>NOTE : It is similar to Binary Subarray with Sum here -
>		odd numbers act like 1
>		even numbers act like 0
>		hence traditional way of applying sliding window doesn't work.

TC-> O(2N)
SC-> O(1)
```java
class Solution {
    private int func(int[] nums,int k){
        int n = nums.length;
        int j=0;
        int cnt=0;
        int ans=0;
        for(int i=0;i<n;i++){
            cnt += nums[i] & 1;
            while(cnt>k){
                if(nums[j]%2 == 1)cnt--;
                j++;
            }
            ans+=(i-j+1);
        }
        return ans;
    }
    public int numberOfSubarrays(int[] nums, int k) {
        return func(nums,k) - func(nums,k-1);
    }
}
```

# Optimal

TC-> O(N)
SC-> O(N) of hash array
```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        int n= nums.length;
        int sum=0;
        int cnt=0;
        int hash[] = new int[n+1];
        hash[0]=1;
        for(int num:nums){
            sum+= num&1;
            if(sum-k>=0)cnt+=hash[sum-k];
            hash[sum]++;
        }
        return cnt;
    }
}
```