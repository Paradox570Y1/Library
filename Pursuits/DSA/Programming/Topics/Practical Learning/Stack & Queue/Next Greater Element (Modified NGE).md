[496. Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)

The **next greater element** of some element `x` in an array is the **first greater** element that is **to the right** of `x` in the same array.

You are given two **distinct 0-indexed** integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the **next greater element** of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

Return _an array_ `ans` _of length_ `nums1.length` _such that_ `ans[i]` _is the **next greater element** as described above._

**Example 1:**

**Input:** nums1 = [4,1,2], nums2 = [1,3,4,2]
**Output:** [-1,3,-1]
**Explanation:** The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.

**Example 2:**

**Input:** nums1 = [2,4], nums2 = [1,2,3,4]
**Output:** [3,-1]
**Explanation:** The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,2,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,4]. There is no next greater element, so the answer is -1.

**Constraints:**

- `1 <= nums1.length <= nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 104`
- All integers in `nums1` and `nums2` are **unique**.
- All the integers of `nums1` also appear in `nums2`.



# Brute

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
        int[] ans = new int[nums1.length];
        for(int i=nums2.length-1;i>=0;i--){
            for(int j=0;j<nums1.length;j++){
                if(nums1[j] == nums2[i]){
                    int cmp=-1;
                    int k=i+1;
                    while(k<nums2.length && nums2[k]<=nums2[i]){
                        k++;
                    }
                    if(k<nums2.length)cmp = nums2[k];
                    ans[j] = cmp;
                }
            }
            
        }
        return ans;
    }
}
```

# Better
TC-> O(n\*m)
SC-> O(n)to return answer
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
        int[] ans = new int[nums1.length];
        
        for(int i=0;i<nums2.length;i++){
            int exist=-1;
            for(int j=0;j<nums1.length;j++){
                if(nums2[i] == nums1[j] && ans[j]==0)exist = j;
            }
            if(exist==-1)continue;
            int p=nums2.length;
            for(int j=i+1;j<nums2.length;j++){
                if(nums2[j]>nums2[i]){
                    p=j;
                    break;
                }
            }
            
            if(p<nums2.length)ans[exist] = nums2[p];
            else ans[exist] = -1;
        }
        return ans;
    }
}
```


# Using stack
- **Time Complexity:** O(2\*n + m), where `n` is the length of `nums2` and `m` is the length of `nums1`.
    
    - O(m) for building the `HashMap` (`hm`).
    - O(2\*n) for iterating through `nums2` and performing stack operations as removing elements can also take upto O(n) during whole iteration .
- **Space Complexity:** O(n), where `n` is the length of `nums2`.
    
    - O(n) for the stack (`st`).
    - O(m) for the `HashMap` (`hm`), but since `m ≤ n` in the worst case, the overall space complexity is O(n).

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
        int[] ans = new int[nums1.length];
        HashMap<Integer,Integer> hm = new HashMap<>();
        Stack<Integer> st = new Stack();
        for(int i=0;i<nums1.length;i++){
            hm.put(nums1[i],i);
        }
        
        for(int i=nums2.length-1;i>=0;i--){
            int cur = nums2[i];
            int idx = -1;
            if(hm.containsKey(cur))idx=hm.get(cur);
            if(!st.isEmpty()){
                while(!st.isEmpty() && st.peek()<=cur)st.pop();
                if(!st.isEmpty() && idx!=-1)ans[idx] = st.peek();
            }
            if(st.isEmpty() && idx!=-1)ans[idx] = -1;
            st.push(cur);
        }
        return ans;
    }
}
```
OR
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Stack<Integer> st = new Stack<>();
        HashMap<Integer,Integer> hm = new HashMap<>();
        int n =nums2.length;
        for(int i=0;i<n;i++){
            while(!st.isEmpty() && nums2[st.peek()]<nums2[i]){
                hm.put(nums2[st.pop()],nums2[i]);
            }
            st.push(i);
        }
        n = nums1.length;
        int ans[] = new int[n];
        for(int i=0;i<n;i++){
            if(hm.containsKey(nums1[i]))ans[i] = hm.get(nums1[i]);
            else ans[i] = -1;
        }
        return ans;
    }
}
```
OR

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        HashMap<Integer,Integer> hm = new HashMap<>();
        int[] ans = new int[nums1.length];
        int n = nums2.length;
        Stack<Integer> st = new Stack<>();
        for(int i=0;i<n;i++){
            hm.put(nums2[i],-1);
            while(!st.isEmpty() && nums2[st.peek()]<nums2[i]){
                hm.put(nums2[st.pop()],nums2[i]);
            }
            st.push(i);
        }
        for(int i=0;i<ans.length;i++){
            ans[i] = hm.get(nums1[i]);
        }
        return ans;
    }
}
```
# For modified NGE (giving better TC on leetcode)
- **Time Complexity:** O(m * n), where `m` is the length of `nums1` and `n` is the length of `nums2`.
    
    - O(m) for building the `HashMap` (`hm`).
    - O(n) for iterating through `nums2`.
    - For each element in `nums2`, you potentially iterate through the remaining elements (nested loop), leading to O(n) for each iteration of `nums1`.
- **Space Complexity:** O(m), where `m` is the length of `nums1`.
    
    - O(m) for the `HashMap` (`hm`).
    - The array `ans` is of size `m`, but it's included in the output and not considered additional memory overhead.

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
        int[] ans = new int[nums1.length];
        HashMap<Integer,Integer> hm = new HashMap<>();
        for(int i=0;i<nums1.length;i++){
            hm.put(nums1[i],i);
        }
        int exist = -1;
        for(int i=0;i<nums2.length;i++){
            if(hm.containsKey(nums2[i]))exist=hm.get(nums2[i]);
            else continue;
            int p=nums2.length;
            for(int j=i+1;j<nums2.length;j++){
                if(nums2[j]>nums2[i]){
                    p=j;
                    break;
                }
            }
            
            if(p<nums2.length)ans[exist] = nums2[p];
            else ans[exist] = -1;
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int st[] = new int[nums2.length];
        int top=-1;
        HashMap<Integer,Integer> hm = new HashMap<>();
        int n =nums2.length;
        for(int i=0;i<n;i++){
            while(top>-1 && nums2[st[top]]<nums2[i]){
                hm.put(nums2[st[top]],nums2[i]);
                top--;
            }
            st[++top] = i;
        }
        n = nums1.length;
        int ans[] = new int[n];
        for(int i=0;i<n;i++){
            if(hm.containsKey(nums1[i]))ans[i] = hm.get(nums1[i]);
            else ans[i] = -1;
        }
        return ans;
    }
}
```