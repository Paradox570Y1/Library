[Link](https://www.naukri.com/code360/problems/subset-sum-equal-to-k_1550954?leftPanelTabValue=PROBLEM)

## Problem statement

Send feedback

You are given an array/list ‘ARR’ of ‘N’ positive integers and an integer ‘K’. Your task is to check if there exists a subset in ‘ARR’ with a sum equal to ‘K’.

Note: Return true if there exists a subset with sum equal to ‘K’. Otherwise, return false.

**For Example :**

```
If ‘ARR’ is {1,2,3,4} and ‘K’ = 4, then there exists 2 subsets with sum = 4. These are {1,3} and {4}. Hence, return true.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= T <= 5
1 <= N <= 10^3
0 <= ARR[i] <= 10^9
0 <= K <= 10^3

Time Limit: 1 sec
```


# Using memoization

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    private static boolean helper(int[] arr,int target,int i,Boolean[][] memo){ 
        if(target==0)return true;
        if(target<0)return false;
        if(i==0)return (target-arr[i] == 0);
        if(memo[i][target]!=null)return memo[i][target];
        return memo[i][target] = (helper(arr,target-arr[i],i-1,memo) || helper(arr,target,i-1,memo));
    }
    public static boolean subsetSumToK(int n, int k, int arr[]){
        // Write your code here.
        Boolean memo[][] = new Boolean[n][k+1];
        return helper(arr,k,n-1,memo);
    }
}
```

OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    private static boolean helper(int[] arr,int i,int sum,Boolean memo[][]){
        if(sum<0)return false;
        if(i<0)return sum == 0;
        if(memo[i][sum]!=null)return memo[i][sum];
        if(helper(arr,i-1,sum-arr[i],memo) || helper(arr,i-1,sum,memo))return memo[i][sum] = true;
        return memo[i][sum] = false;
    }
    public static boolean subsetSumToK(int n, int k, int arr[]){
        // Write your code here.
        Boolean[][] memo = new Boolean[n][k+1];
        return helper(arr,n-1,k,memo);
    }
}

```

# Using Tabulation

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    public static boolean subsetSumToK(int n, int k, int arr[]){
        // Write your code here.
        boolean dp[][] = new boolean[n][k+1];
        for(int i=0;i<n;i++)dp[i][0] = true;
        if(arr[0]<=k)dp[0][arr[0]] = true;
        for(int i=1;i<n;i++){
            for(int j=1;j<=k;j++){
                boolean notTake = dp[i-1][j];
                boolean Take = false;
                if(arr[i]<= j) Take = dp[i-1][j-arr[i]];
                dp[i][j] = Take | notTake;
            }
        }
        return dp[n-1][k];
    }
}
```


After space optimization

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    public static boolean subsetSumToK(int n, int k, int arr[]){
        // Write your code here.
        boolean dp[] = new boolean[k+1];
        dp[0] = true;
        if(arr[0]<=k)dp[arr[0]] = true;
        for(int i=1;i<n;i++){
            boolean cur[] = new boolean[k+1];
            cur[0]=true;
            for(int j=1;j<=k;j++){
                boolean notTake = dp[j];
                boolean Take = false;
                if(arr[i]<= j) Take = dp[j-arr[i]];
                cur[j] = Take | notTake;
            }
            dp=cur;
        }
        return dp[k];
    }
}
```

OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    public static boolean subsetSumToK(int n, int k, int arr[]){
        // Write your code here.
        boolean[] dp = new boolean[k+1];
        dp[0] = true;
        boolean[] temp;
        for (int i = 0; i < n; i++) {
            temp = new boolean[k+1];
            temp[0] = true;
            for (int j = 1; j <= k; j++) {
                temp[j] = dp[j];
                if(j >= arr[i]) temp[j] |= dp[j-arr[i]];
            }
            dp = temp;
        }
        return dp[k];
    }
}

```

OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    public static boolean subsetSumToK(int n, int k, int arr[]){
        // Write your code here.
        boolean dp[] = new boolean[k+1];
        dp[0] = true;
        for (int val : arr) {
            if(val > k) continue; //these can't get me k
            boolean[] cur = new boolean[k+1];
            cur[0] = true;
            for (int j = 1; j < val; j++) { // i need to have previous value
                cur[j] = dp[j];
            }
            for (int j = val; j <= k; j++) { 
                cur[j] = dp[j-val] | dp[j]; //dp[j] for previous 
                //                            and dp[j-val] for take
            }
            dp = cur;
        }
        return dp[k];
    }
}

```