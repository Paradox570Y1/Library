[Link](https://www.naukri.com/code360/problems/frog-jump_3621012)
## Problem statement

Send feedback

There is a frog on the '1st' step of an 'N' stairs long staircase. The frog wants to reach the 'Nth' stair. 'HEIGHT[i]' is the height of the '(i+1)th' stair.If Frog jumps from 'ith' to 'jth' stair, the energy lost in the jump is given by absolute value of ( HEIGHT\[i-1] - HEIGHT\[j-1] ). If the Frog is on 'ith' staircase, he can jump either to '(i+1)th' stair or to '(i+2)th' stair. Your task is to find the minimum total energy used by the frog to reach from '1st' stair to 'Nth' stair.

**For Example**

```
If the given ‘HEIGHT’ array is [10,20,30,10], the answer 20 as the frog can jump from 1st stair to 2nd stair (|20-10| = 10 energy lost) and then a jump from 2nd stair to last stair (|10-20| = 10 energy lost). So, the total energy lost is 20.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= T <= 10
1 <= N <= 100000.
1 <= HEIGHTS[i] <= 1000 .

Time limit: 1 sec
```

##### Sample Input 1:

```
2
4
10 20 30 10
3
10 50 10
```

##### Sample Output 1:

```
20
0
```

##### Explanation of sample input 1:

```
For the first test case,
The frog can jump from 1st stair to 2nd stair (|20-10| = 10 energy lost).
Then a jump from the 2nd stair to the last stair (|10-20| = 10 energy lost).
So, the total energy lost is 20 which is the minimum. 
Hence, the answer is 20.

For the second test case:
The frog can jump from 1st stair to 3rd stair (|10-10| = 0 energy lost).
So, the total energy lost is 0 which is the minimum. 
Hence, the answer is 0.
```


# Brute

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    private static int ans=Integer.MAX_VALUE;
    private static int helper(int n,int i,int[] heights,int energyLoss){
        if(i==n-1){
            ans = Math.min(ans,energyLoss);
            return energyLoss;
        }
        int oneStep = helper(n,i+1,heights,energyLoss+Math.abs(heights[i]-heights[i+1]));
        int twoStep = Integer.MAX_VALUE;
        if(i+2<n)helper(n,i+2,heights,energyLoss+Math.abs(heights[i]-heights[i+2]));
        return Math.min(oneStep,twoStep);
    }
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        ans=Integer.MAX_VALUE;
        helper(n,0,heights,0);
        return ans;
    }

}
```

OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    private static int helper(int i,int[] heights){
        if(i==0)return 0;
        int oneStep = helper(i-1,heights)+Math.abs(heights[i]-heights[i-1]);
        int twoStep = Integer.MAX_VALUE;
        if(i>1)
        twoStep = helper(i-2,heights)+Math.abs(heights[i]-heights[i-2]);
        return Math.min(oneStep,twoStep);

    }
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        return helper(n-1,heights);
    }
}
```
or

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    private static int helper(int i,int jumpSt,int[] heights){
        if(i==heights.length)return 0;
        int step1 = Math.abs(heights[i]-jumpSt) + helper(i+1,heights[i],heights);
        if(i+2>=heights.length)return step1;
        int step2 = Math.abs(heights[i]-jumpSt) + helper(i+2,heights[i],heights);
        return Math.min(step1,step2);
    }
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        return helper(0,heights[0],heights);
    }

}
```
OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    private static int helper(int i,int[] heights){
        if(i+1==heights.length)return 0;
        int step1 = Math.abs(heights[i+1]-heights[i]) + helper(i+1,heights);
        if(i+2>=heights.length)return step1;
        int step2 = Math.abs(heights[i+2]-heights[i]) + helper(i+2,heights);
        return Math.min(step1,step2);
    }
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        return helper(0,heights);
    }

}
```
# Using memo

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    private static int helper(int i,int[] heights,int[] memo){
        if(i==0)return 0;
        if(memo[i]!=-1)return memo[i];
        int oneStep = helper(i-1,heights,memo)+Math.abs(heights[i]-heights[i-1]);
        int twoStep = Integer.MAX_VALUE;
        if(i>1)
        twoStep = helper(i-2,heights,memo)+Math.abs(heights[i]-heights[i-2]);
        return memo[i] = Math.min(oneStep,twoStep);

    }
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        int[] memo = new int[n+1];
        Arrays.fill(memo,-1);
        return helper(n-1,heights,memo);
    }
}
```

or

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    private static int memo[];
    private static int helper(int i,int[] heights){
        if(memo[i]!=-1)return memo[i];
        if(i==heights.length || i+1>=heights.length)return 0;
        int step1 = Math.abs(heights[i+1]-heights[i]) + helper(i+1,heights);
        if(i+2>=heights.length)return step1;
        int step2 = Math.abs(heights[i+2]-heights[i]) + helper(i+2,heights);
        return memo[i] = Math.min(step1,step2);
    }
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        memo = new int[n+1];
        Arrays.fill(memo,-1);
        return helper(0,heights);
    }

}
```

# Using Tabulation

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        if(n==1)return 0;
        int[] dp = new int[n+1];
        dp[0] = 0;
        dp[1] = Math.abs(heights[0]-heights[1]);
        for(int i=2;i<n;i++){
            int prev1 = Math.abs(heights[i-1]-heights[i]);
            int prev2 = Math.abs(heights[i-2]-heights[i]);
            dp[i] = Math.min(prev1+dp[i-1],prev2+dp[i-2]);
        }
        return dp[n-1];
    }
}
```

OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        int dp[] = new int[n];
        dp[0] = 0;
        if(n==1)return 0;
        dp[1] = Math.abs(heights[1]-heights[0]);
        for(int i=2;i<n;i++){
            int step1 = Math.abs(heights[i]-heights[i-1])+dp[i-1];
            int step2 = Math.abs(heights[i]-heights[i-2])+dp[i-2];
            dp[i] = Math.min(step1,step2);
        }
        return dp[n-1];
    }

	}
```


After space optimization
```java
import java.util.* ;
import java.io.*; 
public class Solution {
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        if(n==1)return 0;
        int prev2 = 0;
        int prev1 = Math.abs(heights[0]-heights[1]);
        for(int i=2;i<n;i++){
            int loss1 = Math.abs(heights[i-1]-heights[i]);
            int loss2 = Math.abs(heights[i-2]-heights[i]);
            int cur = Math.min(prev1+loss1,prev2+loss2);
            prev2 = prev1;
            prev1 = cur;
        }
        return prev1;
    }
}
```

OR

```java
public class Solution {
    public static int frogJump(int n, int heights[]) {

        // Write your code here..
        if(n == 1) return 0;
        int st1 = 0;
        int st2 = Math.abs(heights[1]-heights[0]);
        int res = st2;
        for (int i = 2; i < heights.length; i++) {
            res = Math.min(Math.abs(heights[i] - heights[i-1]) + st2, Math.abs(heights[i]-heights[i-2]) + st1);
            st1 = st2;
            st2 = res;
        }
        return res;
    }

}
```