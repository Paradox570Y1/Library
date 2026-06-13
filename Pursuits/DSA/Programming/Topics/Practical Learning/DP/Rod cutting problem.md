[Link](https://www.naukri.com/code360/problems/rod-cutting-problem_800284?leftPanelTabValue=PROBLEM)

## Problem statement

Send feedback

Given a rod of length ‘N’ units. The rod can be cut into different sizes and each size has a cost associated with it. Determine the maximum cost obtained by cutting the rod and selling its pieces.

**Note:**

```
1. The sizes will range from 1 to ‘N’ and will be integers.

2. The sum of the pieces cut should be equal to ‘N’.

3. Consider 1-based indexing.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= T <= 50
1 <= N <= 100
1 <= A[i] <= 100

Where ‘T’ is the total number of test cases, ‘N’ denotes the length of the rod, and A[i] is the cost of sub-length.

Time limit: 1 sec.
```

**Sample Input 1:**

```
2
5
2 5 7 8 10
8
3 5 8 9 10 17 17 20
```

**Sample Output 1:**

```
12
24
```

**Explanation of sample input 1:**

```
Test case 1:

All possible partitions are:
1,1,1,1,1           max_cost=(2+2+2+2+2)=10
1,1,1,2             max_cost=(2+2+2+5)=11
1,1,3               max_cost=(2+2+7)=11
1,4                 max_cost=(2+8)=10
5                   max_cost=(10)=10
2,3                 max_cost=(5+7)=12
1,2,2               max _cost=(1+5+5)=12    

Clearly, if we cut the rod into lengths 1,2,2, or 2,3, we get the maximum cost which is 12.


Test case 2:

Possible partitions are:
1,1,1,1,1,1,1,1         max_cost=(3+3+3+3+3+3+3+3)=24
1,1,1,1,1,1,2           max_cost=(3+3+3+3+3+3+5)=23
1,1,1,1,2,2             max_cost=(3+3+3+3+5+5)=22
and so on….

If we cut the rod into 8 pieces of length 1, for each piece 3 adds up to the cost. Hence for 8 pieces, we get 8*3 = 24.
```

**Sample Input 2:**

```
1
6
3 5 6 7 10 12
```

**Sample Output 2:**

```
18
```



# Using Memoization

```java
public class Solution {
	private static int helper(int price[],int i,int size,int[][] memo){
		if(size==0)return 0;
		if(i==0)return size * price[0];
		if(memo[i][size]!= 0)return memo[i][size];
		int notpick = helper(price,i-1,size,memo);
		int pick=0;
		if(size>=i+1)pick = price[i] + helper(price,i,size-i-1,memo);
		return memo[i][size] = Math.max(notpick,pick);
	}
	public static int cutRod(int price[], int n) {
		int memo[][] = new int[n][n+1];
		return helper(price,n-1,n,memo);
	}
}
```

OR

```java
public class Solution {
	public static int cutRod(int price[], int n) {
		// Write your code here.
        int[][] memo = new int[n][n+1];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= n; j++) {
                memo[i][j] = -1;
            }
        }
        int val = helper(price, n-1, n, memo);
        if(val < 0) return 0;
        return val;
	}
    private static int helper(int[] price, int i, int T, int[][] memo) {
        if (T == 0) return 0;
        if (i < 0 || T < 0) return (int) -1e9;
        if(memo[i][T] != -1) return memo[i][T];
        int p1 = helper(price, i-1, T, memo);
        int p2 = price[i] + helper(price, i, T-i-1, memo);
        return memo[i][T] = Math.max(p1, p2);
    }
}
```

# Using Tabulation

```java
public class Solution {
	public static int cutRod(int price[], int n) {
		int dp[] = new int[n+1];
		for(int i=0;i<=n;i++){
			dp[i] = i*price[0];
		}
		for(int i=1;i<n;i++){
			int cur[] = new int[n+1];
			for(int j=0;j<=n;j++){
				int notpick = dp[j];
				int pick = 0;
				if(j>=i+1)pick = price[i] + cur[j-i-1];
				cur[j] = Math.max(pick,notpick);
			}
			dp = cur;
		}
		return dp[n];
	}
}
```

OR

```java
public class Solution {
	public static int cutRod(int price[], int n) {
		// Write your code here.
		int dp[] = new int[n+1];
		for(int i=0;i<n;i++){
			for(int j=i+1;j<=n;j++){
				dp[j] = Math.max(dp[j],dp[j-i-1]+price[i]);
			}
		}
		return dp[n];
	}
}
```

OR

```java
public class Solution {
	public static int cutRod(int price[], int n) {
		// Write your code here.
		int[] dp = new int[n];
		for (int sz = 1; sz <= n; sz++) {
			dp[sz-1] = price[sz-1];
			for (int p = 1; p < sz; p++) {
				dp[sz-1] = Math.max(dp[sz-p-1] + price[p-1], dp[sz-1]);
			}
		}
		return dp[n-1];
	}
}
```