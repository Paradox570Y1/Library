[Link](https://www.naukri.com/code360/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum_842494?leftPanelTabValue=PROBLEM)
## Problem statement

Send feedback

You are given an array **'arr'** containing **'n'** non-negative integers.
Your task is to partition this array into two subsets such that the absolute difference between subset sums is minimum.

You just need to find the minimum absolute difference considering any valid division of the array elements.
Note:

```
1. Each array element should belong to exactly one of the subsets.

2. Subsets need not always be contiguous.
For example, for the array : [1, 2, 3], some of the possible divisions are 
   a) {1,2} and {3}
   b) {1,3} and {2}.

3. Subset-sum is the sum of all the elements in that subset. 
```

**Example:**

```
Input: 'n' = 5, 'arr' = [3, 1, 5, 2, 8].

Ouput: 1

Explanation: We can partition the given array into {3, 1, 5} and {2, 8}. 
This will give us the minimum possible absolute difference i.e. (10 - 9 = 1).
```


# Brute

```java
public class Solution{
	private static int min;
	private static int total;
	private static void helper(int[] arr,int i,int sum) {
		if(i<0) {
			min = Math.min(min,Math.abs(sum-(total-sum)));
			return;
		}
		helper(arr,i-1,sum+arr[i]);
		helper(arr,i-1,sum);
	}
	public static int minSubsetSumDifference(int []arr, int n) {
		min =  Integer.MAX_VALUE;
		total=0;
		for(int i=0;i<n;i++) {
			total+=arr[i];
		}
		helper(arr,n-1,0);
		return min;
	}
}
```

# Using Memoization

```java
import java.util.HashSet;
public class Solution{
	private static int min;
	private static int total;
	private static HashSet<String>visited;
	private static void helper(int[] arr,int i,int sum) {
		if(i<0) {
			min = Math.min(min,Math.abs(sum-(total-sum)));
			return;
		}
		String val = i+"|"+sum;
		if(visited.contains(val))return;
		visited.add(val);
		helper(arr,i-1,sum+arr[i]);
		helper(arr,i-1,sum);
	}
	public static int minSubsetSumDifference(int []arr, int n) {
		min =  Integer.MAX_VALUE;
		total=0;
		for(int i=0;i<n;i++) {
			total+=arr[i];
		}
		visited=new HashSet<>();
		helper(arr,n-1,0);
		return min;
	}
}

```



# Using Tabulation

```java
public class Solution {
    public static int minSubsetSumDifference(int []arr, int n) {
        // Write your code here.
        int total=0;
        for(int num:arr)total+=num;
        boolean[][] dp = new boolean[n][total+1];
        for(int i=0;i<n;i++)dp[i][0]=true;
        if(arr[0]<=total)dp[0][arr[0]] = true;
        for(int i=1;i<n;i++) {
        	for(int j=1;j<total+1;j++) {
        		boolean pick = false;
        		if(arr[i]<=j) pick = dp[i-1][j-arr[i]];
        		boolean unpick = dp[i-1][j];
        		dp[i][j] = pick | unpick;
        	}
        }
        int ans = Integer.MAX_VALUE;
        for(int i=0;i<total+1;i++){
          if(!dp[n-1][i])continue;
          int sum1 = i;
          int sum2 = total-i;
          ans = Math.min(ans,Math.abs(sum1-sum2));
        }
        return ans;
    }
}
```


After space Optimization

```java
public class Solution {
    public static int minSubsetSumDifference(int []arr, int n) {
        // Write your code here.
        int total=0;
        for(int num:arr)total+=num;
        boolean[] dp = new boolean[total+1];
        dp[0]=true;
        if(arr[0]<=total)dp[arr[0]] = true;
        for(int i=1;i<n;i++) {
          boolean[] cur = new boolean[total+1];
          cur[0] = true;
        	for(int j=1;j<total+1;j++) {
        		boolean pick = false;
        		if(arr[i]<=j) pick = dp[j-arr[i]];
        		boolean unpick = dp[j];
        		cur[j] = pick | unpick;
        	}
          dp = cur;
        }
        int ans = Integer.MAX_VALUE;
        for(int i=0;i<total+1;i++){
          if(!dp[i])continue;
          int sum1 = i;
          int sum2 = total-i;
          ans = Math.min(ans,Math.abs(sum1-sum2));
        }
        return ans;
    }
}

```

OR

```java
public class Solution {
    public static int minSubsetSumDifference(int []arr, int n) {
        // Write your code here.
        int total = 0;
        for(int i=0;i<n;i++)total+=arr[i];
        boolean[] dp = new boolean[total+1];
        dp[0] = true;
        int ans = total;
        for(int i=0;i<n;i++){
            boolean[] temp = new boolean[total+1];
            temp[0] = true;
            for(int j=1;j<=total;j++){
                boolean notPick = dp[j];
                boolean Pick = false;
                if(j>=arr[i])Pick = dp[j-arr[i]];
                temp[j] = Pick | notPick;
                if(temp[j])ans = Math.min(ans,Math.abs(2*j-total));
            }
            dp = temp;
        }
        return ans;
    }
}
```

OR

Little better to calculate min at last instead of every row 

```java
public class Solution {
    public static int minSubsetSumDifference(int []arr, int n) {
        // Write your code here.
        int total = 0;
        for(int i=0;i<n;i++)total+=arr[i];
        boolean[] dp = new boolean[total+1];
        dp[0] = true;
        int ans = total;
        for(int i=0;i<n;i++){
            boolean[] temp = new boolean[total+1];
            temp[0] = true;
            for(int j=1;j<=total;j++){
                boolean notPick = dp[j];
                boolean Pick = false;
                if(j>=arr[i])Pick = dp[j-arr[i]];
                temp[j] = Pick | notPick;
            }
            dp = temp;
        }
        for(int i=0;i<=total;i++){
            if(!dp[i])continue;
            ans = Math.min(ans,Math.abs(2*i-total));
        }
        return ans;
    }
}
```

OR

```java
public class Solution {
    private static int memo[][];
    public static int minSubsetSumDifference(int []arr, int n) {
        // Write your code here.
        int T = 0;
        for (int ele : arr) {
            T += ele;
        }
        boolean[] dp = new boolean[T+1];
        dp[0] = true;
        for (int i = 0; i < n; i++) {
            boolean cur[] = new boolean[T+1];
            cur[0] = true;
            for (int j = 1; j < T+1; j++) {
                cur[j] = dp[j];
                if (j >= arr[i]) cur[j] |= dp[j-arr[i]];
            }
            dp = cur;
        }
        int res = (int) 1e9;
        for (int i = 0; i <= T; i++) {
            if (dp[i]) res = Math.min(res, Math.abs(2*i - T));
        }
        return res;
    }
}
```

OR

```java
public class Solution {
    public static int minSubsetSumDifference(int []arr, int n) {
        // Write your code here.
        int T = 0;
        for (int val : arr) T+= val;
        boolean dp[] = new boolean[T+1];
        dp[0] = true;
        for (int val : arr) {
            boolean cur[] = new boolean[T+1];
            cur[0] = true;
            for (int j = 1; j <= T; j++) {
                cur[j] = dp[j]; //not take
                if(j >= val) cur[j] |= dp[j-val]; // take
            }
            dp = cur;
        }

        int min = T;
        for (int i = 0; i < T; i++) {
            if(dp[i]) {
                min = Math.min(min, Math.abs(2*i - T));
            }
        }
        return min;
    }
}
```