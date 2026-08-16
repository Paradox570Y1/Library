[Link](https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1)
Given an array **arr[]** containing integers and an integer **k**, your task is to find the length of the longest subarray where the sum of its elements is equal to the given value k. If there is no subarray with sum equal to k, return 0.

**Examples:**

**Input:** arr[] = [10, 5, 2, 7, 1, -10], k = 15
**Output:** 6
**Explanation:** Subarrays with sum = 15 are [5, 2, 7, 1], [10, 5] and [10, 5, 2, 7, 1, -10]. The length of the longest subarray with a sum of 15 is 6.

**Input:** arr[] = [-5, 8, -14, 2, 4, 12], k = -5
**Output:** 5
**Explanation:** Subarrays with sum = -5 are [-5] and [-5, 8, -14, 2, 4]. The length of the longest subarray with a sum of -5 is 5.

**Input:** arr[] = [10, -10, 20, 30], k = 5
**Output:** 0
**Explanation:** No subarray with sum = 5 is present in arr[].

**Constraints:**  
1 ≤ arr.size() ≤ 105  
-104 ≤ arr[i] ≤ 104  
-109 ≤ k ≤ 109

**Expected Complexities**
Time Complexity: O(n)
Auxiliary Space: O(n)
## Brute Force
```java
import java.util.*;

public class tUf {
    public static int getLongestSubarray(int []a, long k) {
        int n = a.length; // size of the array.

        int len = 0;
        for (int i = 0; i < n; i++) { // starting index
            for (int j = i; j < n; j++) { // ending index
                // add all the elements of
                // subarray = a[i...j]:
                long s = 0;
                for (int K = i; K <= j; K++) {
                    s += a[K];
                }

                if (s == k)
                    len = Math.max(len, j - i + 1);
            }
        }
        return len;
    }

    public static void main(String[] args) {
        int[] a = {2, 3, 5, 1, 9};
        long k = 10;
        int len = getLongestSubarray(a, k);
        System.out.println("The length of the longest subarray is: " + len);
    }
}
```
**Time Complexity:** O(N3) approx., where N = size of the array.  
**Reason:** We are using three nested loops, each running approximately N times.

**Space Complexity:** O(1) as we are not using any extra space.

### Better Brute force
```java
import java.util.*;

public class tUf {
    public static int getLongestSubarray(int []a, long k) {
        int n = a.length; // size of the array.

        int len = 0;
        for (int i = 0; i < n; i++) { // starting index
            long s = 0; // Sum variable
            for (int j = i; j < n; j++) { // ending index
                // add the current element to
                // the subarray a[i...j-1]:
                s += a[j];

                if (s == k)
                    len = Math.max(len, j - i + 1);
            }
        }
        return len;
    }

    public static void main(String[] args) {
        int[] a = {2, 3, 5, 1, 9};
        long k = 10;
        int len = getLongestSubarray(a, k);
        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

OR

```java
class Solution {
    public int longestSubarray(int[] arr, int target) {
        // code here
        int maxLen = 0;
        int total = 0;
        for (int i = 0; i < arr.length; i++) {
            total += arr[i];
            int subTotal = total;
            for (int j = 0; j <= i; j++) {
                int subLen = i-j+1;
                if (subTotal == target && subLen > maxLen) {
                    maxLen = subLen;
                    break;
                }
                subTotal -= arr[j];
            }
        }
        return maxLen;
    }
}
```
## Optimal approach(for +ve,-ve and 0)

#### **Prefix Sum + HashMap Technique**

In C++, the `find()` method in `std::map` (or `std::unordered_map`) is used to search for a key in the map. The `find()` method returns an iterator to the element if the key is found. If the key is not found, it returns an iterator to the past-the-end element (i.e., the element one past the last element in the map), which can be obtained using `map.end()`

![[Pasted image 20240712155531.png|300]]

- In java
```java
class Solution{
    
   static int max(int a,int b){
       if(a>b) return a;
       return b;
   }
    // Function for finding maximum and value pair
    public static int lenOfLongSubarr (int A[], int N, int K) {
        //Complete the function
        int sum=0;
        int len=0;
        HashMap<Integer,Integer> mp = new HashMap<>();
        for(int i=0;i<N;i++){
            sum += A[i];
            
            if(sum == K) len = max(len,i+1);
            
            int rem = sum-K;
            if(mp.containsKey(rem)){
                len = max(len,i-mp.get(rem));
            }
            if(mp.containsKey(sum) == false)
            mp.put(sum,i);
        }
        return len;
    }
    
    
}
```

- In c++
```cpp
class Solution{
    public:
    int lenOfLongSubarr(int A[],  int N, int K) 
    { 
        // Complete the function
        int sum=0;
        int len=0;
        int rem=0;
        map<int,int> mp;
        for(int i=0;i<N;i++){
            sum +=A[i];
            if(sum==K) len = max(len,i+1);
            
            rem = sum-K;
            if(mp.find(rem) != mp.end()){
                len = max(len,i-mp[rem]);
            } else mp[sum]=i;
        }
        return len;
    } 

};
```
![[Pasted image 20240713115641.png|600]]
we can use insert also without any condition
**Insertion Behavior**:

- If the key does not exist in the map, `insert()` will insert the key-value pair.
- If the key already exists in the map, `insert()` does nothing and returns an iterator to the existing element (key-value pair).
```cpp
class Solution{
    public:
    int lenOfLongSubarr(int A[],  int N, int K) 
    { 
        // Complete the function
        int sum=0;
        int len=0;
        int rem=0;
        map<int,int> mp;
        for(int i=0;i<N;i++){
            sum +=A[i];
            if(sum==K) len = max(len,i+1);
            mp.insert({sum,i});
            rem = sum-K;
            if(mp.find(rem) != mp.end()){
                len = max(len,i-mp[rem]);
            }
        }
        return len;
    } 

};
```

##### Complexity Analysis
**Time Complexity:** O(N) or O(N*logN) depending on which map data structure we are using, where N = size of the array.  
**Reason:** For example, if we are using an unordered_map data structure in C++ the time complexity will be O(N)(_though in the worst case, unordered_map takes O(N) to find an element and the time complexity becomes O(N²)_) but if we are using a map data structure, the time complexity will be O(N*logN). The least complexity will be O(N) as we are using a loop to traverse the array.

**Space Complexity:** O(N) as we are using a map data structure.


OR

```java
class Solution {
    public int longestSubarray(int[] arr, int target) {
        // code here
        HashMap<Integer,Integer> mp = new HashMap<>();
        mp.put(0,-1);
        int total = 0;
        int res = 0;
        for(int i = 0; i < arr.length; i++){
            total += arr[i];
            int subLen = i - mp.getOrDefault(total - target, i);
            res = Math.max(subLen, res);
            mp.putIfAbsent(total, i);
        }
        return res;
    }
}
```

## Approach(for +ve and 0)

#### **Sliding Window Technique** (also known as the **Two Pointer Technique**)
# Optimal 
```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        int maxLen=0;
        int j=0;
        int total=0;
        for(int i=0;i<n;i++){
            total+=nums[i];
            if(total>k){
                while(j<=i && total>k){
                    total-=nums[j++];
                }
            }
            if(total==k)maxLen = Math.max(maxLen, i-j+1);
        }
        return maxLen;
    }
}
```
OR
```java
public class m {
    public static int getLongestSubarray(int[] a, long k) {
        int n = a.length; // size of the array.

        int left = 0, right = 0; // 2 pointers
        long sum = a[0];
        int maxLen = 0;
        while (right < n) {
            // if sum > k, reduce the subarray from left
            // until sum becomes less or equal to k:
            while (left <= right && sum > k) {
                sum -= a[left];
                left++;
            }

            // if sum = k, update the maxLen i.e. answer:
            if (sum == k) {
                maxLen = Math.max(maxLen, right - left + 1);
            }

            // Move forward the right pointer:
            right++;
            if (right < n)
                sum += a[right];
        }

        return maxLen;
    }

    public static void main(String[] args) {
        int[] a = { 1,2,1,2,1,2};
        long k = 15;
        int len = getLongestSubarray(a, k);
        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

Complexity Analysis

**Time Complexity:** O(2*N), where N = size of the given array.  
**Reason:** The outer while loop i.e. the right pointer can move up to index n-1(_the last index_). Now, the inner while loop i.e. the left pointer can move up to the right pointer at most. So, every time the inner loop does not run for n times rather it can run for n times in total. So, the time complexity will be O(2*N) instead of O(N2).

**Space Complexity:** O(1) as we are not using any extra space.
