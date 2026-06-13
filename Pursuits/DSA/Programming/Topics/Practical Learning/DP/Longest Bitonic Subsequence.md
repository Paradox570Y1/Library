[Link](https://www.geeksforgeeks.org/problems/longest-bitonic-subsequence0824/1)
Given an array of positive integers. Find the **maximum** length of **Bitonic subsequence.**   
A subsequence of array is called Bitonic if it is first strictly increasing, then strictly decreasing. Return the maximum length of bitonic subsequence.  
   
**Note** : A strictly increasing or a **strictly** decreasing sequence should not be considered as a bitonic sequence

**Examples :**

**Input:** n = 5, nums[] = [1, 2, 5, 3, 2]
**Output:** 5
**Explanation:** The sequence {1, 2, 5} is increasing and the sequence {3, 2} is decreasing so merging both we will get length 5.

**Input:** n = 8, nums[] = [1, 11, 2, 10, 4, 5, 2, 1]
**Output:** 6
**Explanation:** The bitonic sequence {1, 2, 10, 4, 2, 1} has length 6.

**Input:** n = 3, nums[] = [10, 20, 30]
**Output:** 0
**Explanation:** The decreasing or increasing part cannot be empty

**Input:** n = 3, nums[] = [10, 10, 10]
**Output:** 0
**Explanation:** The subsequences must be strictly increasing or decreasing

**Constraints:**  
1 ≤ length of array ≤ 103  
1 ≤ arr[i] ≤ 104


# Using LIS

```java

class Solution {
    public static int LongestBitonicSequence(int n, int[] nums) {
        // code here
        int left[] = new int[n];
        for(int i=0;i<n;i++){
            left[i]=1;
            for(int j=0;j<i;j++){
                if(nums[i]>nums[j] && left[i]<1+left[j]){
                    left[i] = 1+left[j];
                }
            }
        }
        int right[] =  new int[n];
        for(int i=n-1;i>=0;i--){
            right[i] = 1;
            for(int j=i+1;j<n;j++){
                if(nums[i]>nums[j] && right[i]<1+right[j]){
                    right[i] = 1+right[j];
                }
            }
        }
        int maxi=0;
        for(int i=0;i<n;i++){
            if(left[i]-1>0 && right[i]-1>0)maxi = Math.max(maxi,left[i]+right[i]-1);
        }
        return maxi;
    }
}
```

OR

```java
class Solution {
    public static int longestBitonicSequence(int n, int[] nums) {
        // code here
        int res = 0;
        int[] LIS = new int[n];
        int[] LDS = new int[n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    LIS[i] = Math.max(LIS[i], LIS[j] + 1);
                }
                if (nums[n-i-1] > nums[n-j-1]) {
                    LDS[n-i-1] = Math.max(LDS[n-i-1], LDS[n-j-1] + 1);
                }
            }
        }
        for (int i = 0; i < n; i++) {
            if (LIS[i] == 0 || LDS[i] == 0) continue;
            res = Math.max(LIS[i] + LDS[i]+1, res);
        }
        return res;
    }
}

```