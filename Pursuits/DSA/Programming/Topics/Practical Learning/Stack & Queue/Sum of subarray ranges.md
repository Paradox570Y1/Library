[2104. Sum of Subarray Ranges](https://leetcode.com/problems/sum-of-subarray-ranges/)

You are given an integer array `nums`. The **range** of a subarray of `nums` is the difference between the largest and smallest element in the subarray.

Return _the **sum of all** subarray ranges of_ `nums`_._

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** 4
**Explanation:** The 6 subarrays of nums are the following:
[1], range = largest - smallest = 1 - 1 = 0 
[2], range = 2 - 2 = 0
[3], range = 3 - 3 = 0
[1,2], range = 2 - 1 = 1
[2,3], range = 3 - 2 = 1
[1,2,3], range = 3 - 1 = 2
So the sum of all ranges is 0 + 0 + 0 + 1 + 1 + 2 = 4.

**Example 2:**

**Input:** nums = [1,3,3]
**Output:** 4
**Explanation:** The 6 subarrays of nums are the following:
[1], range = largest - smallest = 1 - 1 = 0
[3], range = 3 - 3 = 0
[3], range = 3 - 3 = 0
[1,3], range = 3 - 1 = 2
[3,3], range = 3 - 3 = 0
[1,3,3], range = 3 - 1 = 2
So the sum of all ranges is 0 + 0 + 0 + 2 + 0 + 2 = 4.

**Example 3:**

**Input:** nums = [4,-2,-3,4,1]
**Output:** 59
**Explanation:** The sum of all subarray ranges of nums is 59.

**Constraints:**

- `1 <= nums.length <= 1000`
- `-109 <= nums[i] <= 109`



# Better
TC-> O(N²)
SC-> O(1)

```java
class Solution {
    public long subArrayRanges(int[] nums) {
        int n= nums.length;
        long ans=0;
        for(int i=0;i<n;i++){
            int mini = nums[i];
            int maxi = nums[i];
            for(int j=i+1;j<n;j++){
                mini = Math.min(mini,nums[j]);
                maxi = Math.max(maxi,nums[j]);
                ans+=(maxi-mini);
            }
        }
        return ans;
    }
}
```

# Optimal

```java
class Solution {
    private long calSum(int nums[],boolean min){
        int n= nums.length;
        Stack<Integer> st = new Stack<>();
        int next[] = new int[n];
        for(int i=0;i<n;i++){
            next[i] = n;
            while(!st.isEmpty() && ((min)?nums[st.peek()]>=nums[i]:nums[st.peek()]<=nums[i])){
                next[st.pop()] = i;
            }
            st.push(i);
        }
        st.clear();
        long ans=0;
        for(int i=0;i<n;i++){
            while(!st.isEmpty() && ((min)?nums[st.peek()]>=nums[i]:nums[st.peek()]<=nums[i]))st.pop();
            int left = i-((st.isEmpty())?-1:st.peek());
            int right = next[i]-i;
            ans = ans+ (long)left*right*nums[i];
            st.push(i);
        }
        return ans;
    }
    public long subArrayRanges(int[] nums) {
        return calSum(nums,false) - calSum(nums,true);
    }
}
```