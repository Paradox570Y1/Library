[Link](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)
Difficulty: **Medium**Accuracy: **41.84%**Submissions: **322K+**Points: **4**

Given an array having both positive and negative integers. The task is to compute the length of the largest subarray with sum 0.

**Examples:**

**Input:** arr[] = {15,-2,2,-8,1,7,10,23}, n = 8
**Output:** 5
**Explanation:** The largest subarray with sum 0 is -2 2 -8 1 7.

**Input:** arr[] = {2,10,4}, n = 3
**Output:** 0
**Explanation:** There is no subarray with 0 sum.

**Input:** arr[] = {1, 0, -4, 3, 1, 0}, n = 6
**Output:** 5
**Explanation:** The subarray is 0 -4 3 1 0.

**Expected Time Complexity:** O(n).  
**Expected Auxiliary Space:** O(n).


# Optimal
```java
class GfG
{
    int maxLen(int arr[], int n)
    {
        // Your code here
        Map<Integer,Integer> mp = new HashMap<>();
        int sum=0,len=0;
        for(int i=0;i<n;i++){
            sum += arr[i];
            if(sum==0) len = len<i+1?i+1:len;
            if(mp.containsKey(sum)){
                len = len<i-mp.get(sum)?i-mp.get(sum):len;
            }
            else{
                mp.put(sum,i);
            }
        }
        return len;
        
    }
}
```

OR

```java
class Solution {
    int maxLen(int arr[]) {
        // code here
        int n = arr.length;
        HashMap<Integer,Integer> hm = new HashMap<>();
        hm.put(0,-1);
        int total=0;
        int maxLen=0;
        for(int i=0;i<n;i++){
            total+=arr[i];
            if(hm.containsKey(-total)){
                maxLen = Math.max(maxLen,i-hm.get(-total));
            }
            hm.put(-total,hm.getOrDefault(-total,i));
        }
        return maxLen;
    }
}
```

OR

```java
class Solution {
    int maxLength(int arr[]) {
        // code here
        int n = arr.length;
        HashMap<Integer, Integer> hm = new HashMap<>();
        int prefixSum = 0;
        hm.put(0, -1);
        int res = 0;
        for (int i = 0; i < n; i++) {
            prefixSum += arr[i];
            if (hm.containsKey(-prefixSum)) {
                res = Math.max(res, i - hm.get(-prefixSum));
            } else hm.put(-prefixSum, i);
        }
        return res;
    }
}
```

OR

```java
class Solution {
    int maxLength(int arr[]) {
        // code here
        int n = arr.length;
        HashMap<Integer, Integer> hm = new HashMap<>();
        int prefixSum = 0;
        hm.put(0, -1);
        int res = 0;
        for (int i = 0; i < n; i++) {
            prefixSum += arr[i];
            if (hm.containsKey(prefixSum)) {
                res = Math.max(res, i - hm.get(prefixSum));
            } else hm.put(prefixSum, i);
        }
        return res;
    }
}
```