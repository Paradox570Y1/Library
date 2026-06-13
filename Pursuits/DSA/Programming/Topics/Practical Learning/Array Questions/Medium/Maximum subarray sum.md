[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
###### In this question in case all integers are -ve then return 0.
Given an integer array `nums`, find the subarray with the largest sum, and return _its sum_.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]
**Output:** 6
**Explanation:** The subarray [4,-1,2,1] has the largest sum 6.

**Example 2:**

**Input:** nums = [1]
**Output:** 1
**Explanation:** The subarray [1] has the largest sum 1.

**Example 3:**

**Input:** nums = [5,4,-1,7,8]
**Output:** 23
**Explanation:** The subarray [5,4,-1,7,8] has the largest sum 23.

**Constraints:**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

## Brute Force (TC=>O(N³))
```java
import java.util.*;

public class tUf {
    public static int maxSubarraySum(int[] arr, int n) {
        int maxi = Integer.MIN_VALUE; // maximum sum

        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                // subarray = arr[i.....j]
                int sum = 0;

                //add all the elements of subarray:
                for (int k = i; k <= j; k++) {
                    sum += arr[k];
                }

                maxi = Math.max(maxi, sum);
            }
        }

        return maxi;
    }

    public static void main(String args[]) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4};
        int n = arr.length;
        int maxSum = maxSubarraySum(arr, n);
        System.out.println("The maximum subarray sum is: " + maxSum);

    }

}
```

## Better Approach (TC=> O(N²))
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum;
        int n=nums.length;
        int l_sum = -2147483648;
        for(int i=0;i<n;i++){
            sum=0;
            for(int j=i;j<n;j++){
                sum+=nums[j];
                if(sum > l_sum){
                    l_sum = sum;
                }
            }
        }
        return l_sum;

    }
}
```

# Kadane's Algorithm
[Link](obsidian://open?vault=Lessons&file=DSA%2FProgramming%2FTopics%2FArray%20Questions%2FAlgo%2FKadane's%20Algorithm)
## Optimal (TC=> O(N) , SC => O(1))
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum=0;
        int n=nums.length;
        int maxi = nums[0];   // can take INT_MIN too
        for(int i=0;i<n;i++){
            sum += nums[i];
            if(sum>maxi) {
                maxi = sum;
            }
            if(sum<0) sum=0;
        }
        return maxi;

    }
}

```

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum=nums[0];
        int n=nums.length;
        int maxi = sum;
        for(int i=1;i<n;i++){
            sum = Math.max(nums[i],sum+nums[i]);
            if(sum>maxi) maxi = sum;
        }
        return maxi;

    }
}
```

## Follow Up question
-  To return the subarray instead of just sum.
```java

import java.util.*;

public class tUf {
    public static long maxSubarraySum(int[] arr, int n) {
        long maxi = Long.MIN_VALUE; // maximum sum
        long sum = 0;

        int start = 0;
        int ansStart = -1, ansEnd = -1;
        for (int i = 0; i < n; i++) {

            if (sum == 0) start = i; // starting index

            sum += arr[i];

            if (sum > maxi) {
                maxi = sum;

                ansStart = start;
                ansEnd = i;
            }

            // If sum < 0: discard the sum calculated
            if (sum < 0) {
                sum = 0;
            }
        }

        //printing the subarray:
        System.out.print("The subarray is: [");
        for (int i = ansStart; i <= ansEnd; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.print("]n");

        // To consider the sum of the empty subarray
        // uncomment the following check:

        //if (maxi < 0) maxi = 0;

        return maxi;
    }

    public static void main(String args[]) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4};
        int n = arr.length;
        long maxSum = maxSubarraySum(arr, n);
        System.out.println("The maximum subarray sum is: " + maxSum);

    }

}


```