[Link](https://www.naukri.com/code360/problems/partitions-with-given-difference_3751628?leftPanelTabValue=PROBLEM)

## Problem statement

Send feedback

Given an array ‘ARR’, partition it into two subsets (possibly empty) such that their union is the original array. Let the sum of the elements of these two subsets be ‘S1’ and ‘S2’.

Given a difference ‘D’, count the number of partitions in which ‘S1’ is greater than or equal to ‘S2’ and the difference between ‘S1’ and ‘S2’ is equal to ‘D’. Since the answer may be too large, return it modulo ‘10^9 + 7’.

If ‘Pi_Sj’ denotes the Subset ‘j’ for Partition ‘i’. Then, two partitions P1 and P2 are considered different if:

```
1) P1_S1 != P2_S1 i.e, at least one of the elements of P1_S1 is different from P2_S2.
2) P1_S1 == P2_S2, but the indices set represented by P1_S1 is not equal to the indices set of P2_S2. Here, the indices set of P1_S1 is formed by taking the indices of the elements from which the subset is formed.
Refer to the example below for clarification.
```

Note that the sum of the elements of an empty subset is 0.

**For example :**

```
If N = 4, D = 3, ARR = {5, 2, 5, 1}
There are only two possible partitions of this array.
Partition 1: {5, 2, 1}, {5}. The subset difference between subset sum is: (5 + 2 + 1) - (5) = 3
Partition 2: {5, 2, 1}, {5}. The subset difference between subset sum is: (5 + 2 + 1) - (5) = 3
These two partitions are different because, in the 1st partition, S1 contains 5 from index 0, and in the 2nd partition, S1 contains 5 from index 2.
```

**Input Format :**

```
The first line contains a single integer ‘T’ denoting the number of test cases, then each test case follows:

The first line of each test case contains two space-separated integers, ‘N’ and ‘D,’ denoting the number of elements in the array and the desired difference.

The following line contains N integers denoting the space-separated integers ‘ARR’.
```

**Output Format :**

```
For each test case, find the number of partitions satisfying the above conditions modulo 10^9 + 7.
Output for each test case will be printed on a separate line.
```

**Note :**

```
You are not required to print anything; it has already been taken care of. Just implement the function.
```

**Constraints :**

```
1 ≤ T ≤ 10
1 ≤ N ≤ 50
0 ≤ D ≤ 2500
0 ≤ ARR[i] ≤ 50

Time limit: 1 sec
```

**Sample Input 1 :**

```
2
4 3
5 2 6 4
4 0
1 1 1 1
```

**Sample Output 1 :**

```
1
6
```

**Explanation For Sample Input 1 :**

```
For test case 1:
We will print 1 because :
There is only one possible partition of this array.
Partition : {6, 4}, {5, 2}. The subset difference between subset sum is: (6 + 4) - (5 + 2) = 3

For test case 2:
We will print 6 because :
The partition {1, 1}, {1, 1} is repeated 6 times:
Partition 1 : {ARR[0], ARR[1]}, {ARR[2], ARR[3]}
Partition 2 : {ARR[0], ARR[2]}, {ARR[1], ARR[3]}
Partition 3 : {ARR[0], ARR[3]}, {ARR[1], ARR[2]}
Partition 4 : {ARR[1], ARR[2]}, {ARR[0], ARR[3]}
Partition 5 : {ARR[1], ARR[3]}, {ARR[0], ARR[2]}
Partition 6 : {ARR[2], ARR[3]}, {ARR[0], ARR[1]}
The difference is in the indices chosen for the subset S1(or S2).
```


# Using Memoization

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	private static int helper(int[] arr,int sum,int i,int[][] memo){
		if(i==0){
			if(arr[0]==0 && sum==0)return 2;
			else if(sum==arr[0] || sum==0)return 1;
			return 0;
		}
		if(memo[i][sum]!=-1)return memo[i][sum];
		int notpick = helper(arr,sum,i-1,memo);
		int pick=0;
		if(arr[i]<=sum)pick = helper(arr,sum-arr[i],i-1,memo);
		return memo[i][sum] = (pick + notpick)%1000000007;
	}
	public static int countPartitions(int n, int d, int[] arr) {
		// Write your code here.
		int total = Arrays.stream(arr).sum();
		if(total-d<0 || (total-d)%2==1)return 0;
		int reqSum = (total-d)/2;
		int memo[][] = new int[n][reqSum+1];
		for(int i=0;i<n;i++){
			Arrays.fill(memo[i],-1);
		}
		return helper(arr,reqSum,n-1,memo);
	}
}
```

OR

```java
class Solution {
    private int helper(int[] nums,int i,int sum){
        if(i==0){
            if(nums[i]==0 && sum==0)return 2;
            if(nums[i]==sum || sum==0)return 1;
            return 0;
        }
        int notpick = helper(nums,i-1,sum);
        int pick=0;
        if(nums[i]<=sum)pick = helper(nums,i-1,sum-nums[i]);
        return pick + notpick;
    }
    public int findTargetSumWays(int[] nums, int target) {
        int n = nums.length;
        int total = Arrays.stream(nums).sum();
        if((total+target)%2==1 || total+target<0)return 0;
        int set1 = (total+target)/2;
        return helper(nums,n-1,set1);
    }
}
```


# Using Memoization

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int countPartitions(int n, int d, int[] arr) {
		// Write your code here.
		int total = Arrays.stream(arr).sum();
		if(total-d<0 || (total-d)%2==1)return 0;
		int reqSum = (total-d)/2;
		int dp[] = new int[reqSum+1];
		if(arr[0]==0)dp[0]=2;
		else dp[0]=1;
		if(arr[0] != 0 && arr[0]<=reqSum)dp[arr[0]]=1;
		for(int i=1;i<n;i++){
			int cur[] = new int[reqSum+1];
			for(int j=0;j<=reqSum;j++){
				int notpick = dp[j];
				int pick=0;
				if(arr[i]<=j)pick=dp[j-arr[i]];
				cur[j] = pick+notpick;
			}
			dp=cur;
		}
		return dp[reqSum];
	}
}
```

OR

```java
class Solution {
    private int helper(int[] nums,int i,int sum,int[][] memo){
        if(i==0){
            if(nums[i]==0 && sum==0)return 2;
            if(nums[i]==sum || sum==0)return 1;
            return 0;
        }
        if(memo[i][sum]!=-1)return memo[i][sum];
        int notpick = helper(nums,i-1,sum,memo);
        int pick=0;
        if(nums[i]<=sum)pick = helper(nums,i-1,sum-nums[i],memo);
        return memo[i][sum] = pick + notpick;
    }
    public int findTargetSumWays(int[] nums, int target) {
        int n = nums.length;
        int total = Arrays.stream(nums).sum();
        if((total+target)%2==1 || total+target<0)return 0;
        int set1 = (total+target)/2;
        int memo[][] = new int[n][set1+1];
        for(int i=0;i<n;i++){
            Arrays.fill(memo[i],-1);
        }
        return helper(nums,n-1,set1,memo);
    }
}
```

OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	private static int helper(int[] arr,int i,int diff,int sum,int total,int[][] memo){
		if(i<0){
			if(sum >= total-sum && 2*sum-total == diff)return 1;
			return 0;
		}
		if(memo[i][sum]!=-1)return memo[i][sum];
		int notTake = helper(arr,i-1,diff,sum,total,memo);
		int Take = helper(arr,i-1,diff,sum+arr[i],total,memo);
		return memo[i][sum] = (int)((1L*Take + notTake)%(1e9+7));
	}
	public static int countPartitions(int n, int d, int[] arr) {
		// Write your code here.
		int sum = 0;
		for(int ele:arr)sum+=ele;
		int memo[][] = new int[n][sum+1];
		for(int i=0;i<n;i++){
			Arrays.fill(memo[i],-1);
		}
		return helper(arr,n-1,d,0,sum,memo);
	}
}
```

# Using Tabulation

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int countPartitions(int n, int d, int[] arr) {
		// Write your code here.
		int total = Arrays.stream(arr).sum();
		if(total-d<0 || (total-d)%2==1)return 0;
		int reqSum = (total-d)/2;
		int dp[] = new int[reqSum+1];
		dp[0]=1;
		if (arr[0] == 0) dp[0] = 2;
		else if (arr[0] <= reqSum) dp[arr[0]] = 1;

		for(int i=1;i<n;i++){
			int cur[] = new int[reqSum+1];
			for(int j=0;j<=reqSum;j++){
				int notpick = dp[j];
				int pick=0;
				if(arr[i]<=j)pick=dp[j-arr[i]];
				cur[j] = (pick+notpick)%((int)1e9+7);
			}
			dp=cur;
		}
		return dp[reqSum];
	}
}
```

OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int countPartitions(int n, int d, int[] arr) {
		// Write your code here.
		int t = 0;
		int MOD = (int) 1e9 + 7;
		for (int num: arr) {
			t += num;
		}
		if((t+d) % 2 == 1) return 0;
		int k = (t+d)/2;
		int dp[] = new int[k+1];
		dp[0] = 1;
		for (int num : arr) {
			int cur[] = new int[k+1];
			for (int j = 0; j <= k; j++) {
				cur[j] = dp[j];
				if(j >= num) cur[j] = (int)(1L*cur[j] + dp[j-num]) % MOD;
			}
			dp = cur;
		}
		return dp[k];
	}
}
```