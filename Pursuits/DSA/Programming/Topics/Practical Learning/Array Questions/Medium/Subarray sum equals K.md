[560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
Given an array of integers `nums` and an integer `k`, return _the total number of subarrays whose sum equals to_ `k`.

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

**Input:** nums = [1,1,1], k = 2
**Output:** 2

**Example 2:**

**Input:** nums = [1,2,3], k = 3
**Output:** 2

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `-1000 <= nums[i] <= 1000`
- `-107 <= k <= 107`

# Brute Force
```java
import java.util.*;

public class tUf {
    public static int findAllSubarraysWithGivenSum(int arr[], int k) {
        int n = arr.length; // size of the given array.
        int cnt = 0; // Number of subarrays:

        for (int i = 0 ; i < n; i++) { // starting index i
            for (int j = i; j < n; j++) { // ending index j

                // calculate the sum of subarray [i...j]
                int sum = 0;
                for (int K = i; K <= j; K++)
                    sum += arr[K];

                // Increase the count if sum == k:
                if (sum == k)
                    cnt++;
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 2, 4};
        int k = 6;
        int cnt = findAllSubarraysWithGivenSum(arr, k);
        System.out.println("The number of subarrays is: " + cnt);
    }
}
```

# Better Approach
```java
import java.util.*;

public class tUf {
    public static int findAllSubarraysWithGivenSum(int arr[], int k) {
        int n = arr.length; // size of the given array.
        int cnt = 0; // Number of subarrays:

        for (int i = 0 ; i < n; i++) { // starting index i
            int sum = 0;
            for (int j = i; j < n; j++) { // ending index j
                // calculate the sum of subarray [i...j]
                // sum of [i..j-1] + arr[j]
                sum += arr[j];

                // Increase the count if sum == k:
                if (sum == k)
                    cnt++;
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 2, 4};
        int k = 6;
        int cnt = findAllSubarraysWithGivenSum(arr, k);
        System.out.println("The number of subarrays is: " + cnt);
    }
}  
```

# Optimal Approach
**Time Complexity:** O(N) or O(N*logN) depending on which map data structure we are using, where N = size of the array.  
**Reason:** For example, if we are using an unordered_map data structure in C++ the time complexity will be O(N) but if we are using a map data structure, the time complexity will be O(N*logN). The least complexity will be O(N) as we are using a loop to traverse the array.

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int cnt =0;
        int prefix_sum=0;
        unordered_map<int,int> mp;
        mp[0] =1;
        for(int i=0;i<nums.size();i++){
            prefix_sum += nums[i];
            int rest = prefix_sum-k;
            cnt += mp[rest];
            mp[prefix_sum]++;
        }
        return cnt;
    }
};
```

```java
import java.util.*;

public class tUf {
    public static int findAllSubarraysWithGivenSum(int arr[], int k) {
        int n = arr.length; // size of the given array.
        Map mpp = new HashMap();
        int preSum = 0, cnt = 0;

        mpp.put(0, 1); // Setting 0 in the map.
        for (int i = 0; i < n; i++) {
            // add current element to prefix Sum:
            preSum += arr[i];

            // Calculate x-k:
            int remove = preSum - k;

            // Add the number of subarrays to be removed:
            cnt += mpp.getOrDefault(remove, 0);

            // Update the count of prefix sum
            // in the map.
            mpp.put(preSum, mpp.getOrDefault(preSum, 0) + 1);
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 2, 4};
        int k = 6;
        int cnt = findAllSubarraysWithGivenSum(arr, k);
        System.out.println("The number of subarrays is: " + cnt);
    }
}
```

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int prefix_sum =0;
        int cnt=0;
        HashMap<Integer,Integer> mp = new HashMap<>();
        mp.put(0,1);
        int t=0;
        for(int i=0;i<nums.length;i++){
            prefix_sum += nums[i];
            int rest = k-prefix_sum;
            if(mp.containsKey(rest)==true){
                cnt += mp.get(rest);
                if(mp.containsKey(nums[i])==true)
                {t = mp.get(nums[i]);
                t++;}
                else{
                    t=0;
                }
            }
            mp.put(nums[i],t);
        }
        return cnt;
    }
}
```
