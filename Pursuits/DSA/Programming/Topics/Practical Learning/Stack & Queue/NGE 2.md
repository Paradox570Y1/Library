[503. Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)

Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return _the **next greater number** for every element in_ `nums`.

The **next greater number** of a number `x` is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.

**Example 1:**

**Input:** nums = [1,2,1]
**Output:** [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number. 
The second 1's next greater number needs to search circularly, which is also 2.

**Example 2:**

**Input:** nums = [1,2,3,4,3]
**Output:** [2,3,4,-1,4]

**Constraints:**

- `1 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`


# Better

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int ans[] = new int[nums.length];
        Stack<Integer> st = new Stack();
        for(int i=nums.length-1;i>=0;i--){
            st.push(nums[i]);
        }
        for(int i=nums.length-1;i>=0;i--){
            while(!st.isEmpty() && st.peek()<=nums[i])st.pop();
            if(st.isEmpty())ans[i] = -1;
            else ans[i] = st.peek();
            st.push(nums[i]);
        }
        return ans;
    }
}
```

More Better ( we assume that we have doubled the nums array by doing modulus)
```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int ans[] = new int[n];
        Stack<Integer> st = new Stack();
        for(int i=2*n-1;i>=0;i--){
            while(!st.isEmpty() && st.peek()<=nums[i%n])st.pop();
            if(i<n)ans[i] = st.isEmpty()? -1:st.peek();
            st.push(nums[i%n]);
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        Stack<Integer> st = new Stack<>();
        int n = nums.length;
        int ans[] = new int[n];
        for(int i=0;i<2*n;i++){
            if(i<n)ans[i] = -1;
            while(!st.isEmpty() && nums[st.peek()]<nums[i%n]){
                ans[st.pop()] = nums[i%n];
            }
            st.push(i%n);
        }
        return ans;
    }
}
```