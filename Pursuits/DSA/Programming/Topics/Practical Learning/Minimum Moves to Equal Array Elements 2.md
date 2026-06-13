[462. Minimum Moves to Equal Array Elements II](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/)

Given an integer array `nums` of size `n`, return _the minimum number of moves required to make all array elements equal_.

In one move, you can increment or decrement an element of the array by `1`.

Test cases are designed so that the answer will fit in a **32-bit** integer.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** 2
**Explanation:**
Only two moves are needed (remember each move increments or decrements one element):
[1,2,3]  =>  [2,2,3]  =>  [2,2,2]

**Example 2:**

**Input:** nums = [1,10,2,9]
**Output:** 16

**Constraints:**

- `n == nums.length`
- `1 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`


```java
class Solution {
    public int minMoves2(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        int mid=-1;
        if(n%2==1)mid = nums[n/2];
        else{
            mid = (nums[n/2] + nums[n/2 - 1])/2;
        }
        int moves=0;
        for(int i=0;i<nums.length;i++){
            moves +=(mid>=nums[i]?mid-nums[i]:nums[i]-mid);
        }
        return moves;
    }
}
```