[Link](https://www.naukri.com/code360/problems/count-subsets-with-sum-k_3952532?leftPanelTabValue=PROBLEM)
## Problem statement

Send feedback

You are given an array _**'arr'**_ of size _**'n'**_ containing positive integers and a target sum _**'k'**_.

Find the number of ways of selecting the elements from the array such that the sum of chosen elements is equal to the target 'k'.
Since the number of ways can be very large, print it modulo 10 ^ 9 + 7.

**Example:**

```
Input: 'arr' = [1, 1, 4, 5]

Output: 3

Explanation: The possible ways are:
[1, 4]
[1, 4]
[5]
Hence the output will be 3. Please note that both 1 present in 'arr' are treated differently.
```

Detailed explanation ( Input/output format, Notes, Images )

**Sample Input 1 :**

```
4 5
1 4 4 5
```

**Sample Output 1 :**

```
 3
```

**Explanation For Sample Output 1:**

```
The possible ways are:
[1, 4]
[1, 4]
[5]
Hence the output will be 3. Please note that both 1 present in 'arr' are treated differently.
```

**Expected time complexity :**

```
The expected time complexity is O('n' * 'k').
```

  

**Constraints:**

```
1 <= 'n' <= 100
0 <= 'arr[i]' <= 1000
1 <= 'k' <= 1000

Time limit: 1 sec
```


# Using Memoization

- Here base case is modified to handle , 0 in array as well
```java
import java.util.*;
import java.io.*;

public class Solution {
    private static int helper(int[] num,int target,int i,int[][] memo){
        if(i==0){
            if(target==0 && num[0]==0) return 2; 
            if(target==0 || num[0]==target) return 1; 
            return 0; 
        }

        if(memo[i][target]!=-1)return memo[i][target];
        int pick=0;
        if(num[i]<=target)pick=helper(num,target-num[i],i-1,memo);
        int notpick=helper(num,target,i-1,memo);
        return memo[i][target] = (pick+notpick)%(1000000007);
    }
    public static int findWays(int num[], int tar) {
        // Write your code here.
        int n = num.length;
        int memo[][] = new int[n][tar+1];
        for(int i=0;i<n;i++){
            Arrays.fill(memo[i],-1);
        }
        return helper(num,tar,n-1,memo);
    }
}
```


>Usual base case to cnt subsets for positive numbers

```java
if(target==0)return 1;
if(i==0){
	if(target==nums[i])return 1;
	return 0;
}
```




# Using Tabulation

```java
import java.util.*;
import java.io.*;

public class Solution {
    public static int findWays(int num[], int tar) {
        // Write your code here.
        int n = num.length;
        int dp[][] = new int[n][tar+1];
        dp[0][0] = 1; //we only know that at base case cnt start from 1
        if(num[0]<=tar)dp[0][num[0]]++;
        for(int i=1;i<n;i++){
            for(int j=0;j<=tar;j++){ //as 0 cnt can increase
                int notpick = dp[i-1][j];
                int pick=0;
                if(num[i]<=j)pick=dp[i-1][j-num[i]];
                dp[i][j] = (pick+notpick)%(1000000007);
            }
        }
        return dp[n-1][tar];
    }
}
```


After space optimization

```java
import java.util.*;
import java.io.*;

public class Solution {
    public static int findWays(int num[], int tar) {
        // Write your code here.
        int n = num.length;
        int dp[] = new int[tar+1];
        dp[0] = 1;
        if(num[0]<=tar)dp[num[0]]++;
        for(int i=1;i<n;i++){
            int cur[] = new int[tar+1];
            for(int j=0;j<=tar;j++){
                int notpick = dp[j];
                int pick=0;
                if(num[i]<=j)pick=dp[j-num[i]];
                cur[j] = (pick+notpick)%(1000000007);
            }
            dp=cur;
        }
        return dp[tar];
    }
}
```

OR

```java
import java.util.*;
import java.io.*;

public class Solution {
    public static int findWays(int num[], int tar) {
        // Write your code here.
        int n = num.length;
        int dp[] = new int[tar+1];
        dp[0] = 1;
        for(int i=0;i<n;i++){
            int temp[] = new int[tar+1];
            temp[0] = 1;
            for(int j=0;j<=tar;j++){
                int notTake = dp[j];
                int Take = 0;
                if(j>=num[i])Take = dp[j-num[i]];
                temp[j] = (int)((1L*Take + notTake)%(1e9+7));
            }
            dp = temp;
        }
        return dp[tar];
    }
}
```

OR
```java
import java.util.*;
import java.io.*;

public class Solution {
    public static int findWays(int num[], int tar) {
        // Write your code here.
        int n = num.length;
        int mod = (int)1e9 + 7;
        int[] dp = new int[tar+1];
        dp[0] = 1;
        for (int i = 0; i < n; i++) {
            int[] cur = new int[tar+1];
            for (int j = 0; j <= tar; j++) {
                cur[j] = dp[j];
                if(j >= num[i]) cur[j] = (int)(1L*cur[j] + dp[j-num[i]]) % mod;
            }
            dp = cur;
        }
        return dp[tar];
    }
}
```