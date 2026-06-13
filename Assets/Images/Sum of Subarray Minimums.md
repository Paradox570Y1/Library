[907. Sum of Subarray Minimums](https://leetcode.com/problems/sum-of-subarray-minimums/)

Given an array of integers arr, find the sum of `min(b)`, where `b` ranges over every (contiguous) subarray of `arr`. Since the answer may be large, return the answer **modulo** `109 + 7`.

**Example 1:**

**Input:** arr = [3,1,2,4]
**Output:** 17
**Explanation:** 
Subarrays are [3], [1], [2], [4], [3,1], [1,2], [2,4], [3,1,2], [1,2,4], [3,1,2,4]. 
Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1.
Sum is 17.

**Example 2:**

**Input:** arr = [11,81,94,43,3]
**Output:** 444

**Constraints:**

- `1 <= arr.length <= 3 * 104`
- `1 <= arr[i] <= 3 * 104`



# Brute

```java
class Solution {
    public int sumSubarrayMins(int[] arr) {
        long ans=0;
        for(int i=0;i<arr.length;i++){
            long mini = arr[i];
            ans=((ans+ mini)%1000000007);
            for(int j=i+1;j<arr.length;j++){
                mini = Math.min(arr[j],mini);
                ans=((ans+ mini)%1000000007);
            }
        }
        return (int)ans;
    }
}
```

# Optimal using stack

```java
class Solution {
    public int sumSubarrayMins(int[] arr) {
      int n = arr.length;
      Stack<Integer> st = new Stack<>();
      long ans=0;
      int nse[] = new int[n];
      int MOD = 1_000_000_007;
      for(int i=0;i<n;i++){
        nse[i] = -1;
      }
      for(int i=0;i<n;i++){
        while(!st.isEmpty() && arr[st.peek()]>arr[i]){
            int idx = st.pop();
            nse[idx] = i;
        }
        st.add(i);
      }
      st.clear();
      for(int i=0;i<n;i++){
        while(!st.isEmpty() && arr[st.peek()]>arr[i])st.pop();
        int prev_idx = st.isEmpty()?-1:st.peek();
        st.add(i);
        int next_idx = nse[i];
        int left = prev_idx==-1?i+1:i-prev_idx;
        int right = next_idx==-1?n-i:next_idx-i;
        ans=(ans+(long) left*right*arr[i])%MOD;
      }
      return (int)ans;
    }
}
```

Further optimization

```java
class Solution {
    public int sumSubarrayMins(int[] arr) {
      int n = arr.length;
      Stack<Integer> st = new Stack<>();
      long ans=0;
      int nse[] = new int[n];
      int MOD = 1_000_000_007;
      for(int i=0;i<n;i++){
        nse[i] = n;
        while(!st.isEmpty() && arr[st.peek()]>arr[i]){
            int idx = st.pop();
            nse[idx] = i;
        }
        st.add(i);
      }
      st.clear();
      for(int i=0;i<n;i++){
        while(!st.isEmpty() && arr[st.peek()]>arr[i])st.pop();
        int left = i-(st.isEmpty()?-1:st.peek());
        int right = nse[i]-i;
        st.add(i);
        ans=(ans+(long) left*right*arr[i])%MOD;
      }
      return (int)ans;
    }
}
```


# Using Stack

TC- > O(10N)
SC-> O(2N)

```java
class Solution {
    private long calMin(int nums[]){
        int n= nums.length;
        Stack<Integer> st = new Stack<>();
        int nse[] = new int[n];
        for(int i=0;i<n;i++){
            nse[i] = n;
            //can also use >= to deal with duplicates although works even without it
            while(!st.isEmpty() && nums[st.peek()]>nums[i]){
                nse[st.pop()] = i;
            }
            st.push(i);
        }
        st.clear();
        long ans=0;
        for(int i=0;i<n;i++){
        //can also use >= to deal with duplicates although works even without it
            while(!st.isEmpty() && nums[st.peek()]>nums[i])st.pop();
            int pse = (st.isEmpty())?-1:st.peek();
            st.push(i);
            int left = i-pse;
            int right = nse[i]-i;
            ans = ans+ (long)left*right*nums[i];
        };
        return ans;
    }
    private long calMax(int nums[]){
        int n= nums.length;
        Stack<Integer> st = new Stack<>();
        int nle[] = new int[n];
        for(int i=0;i<n;i++){
            nle[i] = n;
            //can also use <= to deal with duplicates although works even without it
            while(!st.isEmpty() && nums[st.peek()]<nums[i]){
                nle[st.pop()] = i;
            }
            st.push(i);
        }
        st.clear();
        long ans=0;
        for(int i=0;i<n;i++){
        //can also use <= to deal with duplicates although works even without it
            while(!st.isEmpty() && nums[st.peek()]<nums[i])st.pop();
            int ple = (st.isEmpty())?-1:st.peek();
            st.push(i);
            int left = i-ple;
            int right = nle[i]-i;
            ans = ans+ (long)left*right*nums[i];
        };
        return ans;
    }
    public long subArrayRanges(int[] nums) {
        return calMax(nums) - calMin(nums);
    }
}
```


```java
class Solution {
    private long calSum(int nums[],boolean min){
        int n= nums.length;
        Stack<Integer> st = new Stack<>();
        int next[] = new int[n];
        for(int i=0;i<n;i++){
            next[i] = n;
            while(!st.isEmpty() && ((min)?nums[st.peek()]>nums[i]:nums[st.peek()]<nums[i])){
                next[st.pop()] = i;
            }
            st.push(i);
        }
        st.clear();
        long ans=0;
        for(int i=0;i<n;i++){
            while(!st.isEmpty() && ((min)?nums[st.peek()]>nums[i]:nums[st.peek()]<nums[i]))st.pop();
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



# Solution in comments

```cpp
class Solution {
public:
    long long subArrayRanges(vector<int>& n) {
        return sumSubarrayComp(n, less<int>()) - sumSubarrayComp(n, greater<int>());
    }    
    long long sumSubarrayComp(vector<int>& n, function<bool (int, int)> comp) {
        long long res = 0;
        vector<int> s;
        for (int i = 0; i <= n.size(); ++i) {
            while (!s.empty() && (i == n.size() || comp(n[s.back()], n[i]))) {
                int j = s.back(), k = s.size() < 2 ? -1 : s[s.size() - 2]; 
                res += (long long)(i - j) * (j - k) * n[j];
                s.pop_back();
            }
            s.push_back(i);
        }    
        return res;
    }
};
```