[Link](https://www.naukri.com/code360/problems/ninja-and-his-friends_3125885?leftPanelTabValue=PROBLEM)

## Problem statement

Send feedback

Ninja has a 'GRID' of size 'R' X 'C'. Each cell of the grid contains some chocolates. Ninja has two friends Alice and Bob, and he wants to collect as many chocolates as possible with the help of his friends.

Initially, Alice is in the top-left position i.e. (0, 0), and Bob is in the top-right place i.e. (0, ‘C’ - 1) in the grid. Each of them can move from their current cell to the cells just below them. When anyone passes from any cell, he will pick all chocolates in it, and then the number of chocolates in that cell will become zero. If both stay in the same cell, only one of them will pick the chocolates in it.

If Alice or Bob is at (i, j) then they can move to (i + 1, j), (i + 1, j - 1) or (i + 1, j + 1). They will always stay inside the ‘GRID’.

Your task is to find the maximum number of chocolates Ninja can collect with the help of his friends by following the above rules.

**Example:**

```
Input: ‘R’ = 3, ‘C’ = 4
       ‘GRID’ = [[2, 3, 1, 2], [3, 4, 2, 2], [5, 6, 3, 5]]
Output: 21

Initially Alice is at the position (0,0) he can follow the path (0,0) -> (1,1) -> (2,1) and will collect 2 + 4 + 6 = 12 chocolates.

Initially Bob is at the position (0, 3) and he can follow the path (0, 3) -> (1,3) -> (2, 3) and will colllect 2 + 2 + 5 = 9 chocolates.

Hence the total number of chocolates collected will be 12 + 9 = 21. there is no other possible way to collect a greater number of chocolates than 21.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints :**

```
1 <= ‘T’ <= 10
2 <= 'R', 'C' <= 50
0 <= 'GRID[i][j]'<= 10^2
Time Limit: 1sec
```

**Sample Input 1 :**

```
2
3 4
2 3 1 2
3 4 2 2
5 6 3 5
2 2
1 1
1 2
```

**Sample Output 1 :**

```
21
5
```

**Explanation Of Sample Input 1 :**

```
For the first test case, Initially Alice is at the position (0, 0) he can follow the path (0, 0) -> (1, 1) -> (2, 1) and will collect 2 + 4 + 6 = 12 chocolates.

Initially Bob is at the position (0, 3) and he can follow the path (0, 3) -> (1, 3) -> (2, 3) and will collect 2 + 2 + 5 = 9 chocolates.

Hence the total number of chocolates collected will be 12 + 9 = 21.

For the second test case, Alice will follow the path (0, 0) -> (1, 0) and Bob will follow the path (0, 1) -> (1, 1). total number of chocolates collected will be 1 + 1 + 1 + 2 = 5
```

**Sample Input 2 :**

```
2
2 2
3 7
7 6
3 2
4 5
3 7
4 2
```

**Sample Output 2 :**

```
23
25
```

# Using Recursion
![[Pasted image 20250723191921.png|300]]
# Using Memoization

![[Pasted image 20250723191843.png|300]]
```java
import java.util.* ;
import java.io.*; 
public class Solution {
	private static int helper(int[][] grid,int col1,int col2,int row,int r,int c,int[][][] memo){
		if(col1<0 || col1>=c || col2<0 || col2>=c)return (int)-1e10;
		if(row == r-1){
			if(col1==col2)return grid[row][col1];
			return grid[row][col1] + grid[row][col2];
		}
		if(memo[row][col1][col2]!=-1)return memo[row][col1][col2];
		int maxSum = 0;
		for(int i=col1-1;i<=col1+1;i++){
			for(int j=col2-1;j<=col2+1;j++){
				int sum = helper(grid,i,j,row+1,r,c,memo);
				if(col1==col2)sum+=grid[row][col1];
				else sum+=grid[row][col1] + grid[row][col2];
				maxSum = Math.max(sum,maxSum);
			}
		}
		return memo[row][col1][col2] = maxSum;
	}
	public static int maximumChocolates(int r, int c, int[][] grid) {
		// Write your code here.
		int memo[][][] = new int[r][c][c];
		for(int i=0;i<r;i++){
			for(int j=0;j<c;j++){
				Arrays.fill(memo[i][j],-1);
			}
		}
		return helper(grid,0,c-1,0,r,c,memo);
	}
}
```

or

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	private static int helper(int[][] grid,int i,int j1,int j2,int row,int col,int[][][] memo){
		//base case
		if(j1<0 || j2<0 || j1>=col || j2 >=col)return Integer.MIN_VALUE;
		if(i==row-1){
			if(j1==j2)return grid[i][j1];
			return grid[i][j1]+grid[i][j2];
		}
		if(memo[i][j1][j2]!= -1)return memo[i][j1][j2];
		int maxi=-1;
		for(int c1=-1;c1<=1;c1++){
			for(int c2=-1;c2<=1;c2++){
				int cal = (j1==j2)?grid[i][j1]:grid[i][j1]+grid[i][j2];
				cal+=helper(grid,i+1,j1+c1,j2+c2,row,col,memo);
				maxi = Math.max(maxi,cal);
			}
		}
		return memo[i][j1][j2] = maxi;
	}
	public static int maximumChocolates(int r, int c, int[][] grid) {
		// Write your code here.
		int[][][] memo = new int[r][c][c];
		for(int i=0;i<r;i++){
			for(int j=0;j<c;j++){
				for(int k=0;k<c;k++){
					memo[i][j][k] = -1;
				}
			}
		}
		return helper(grid,0,0,c-1,r,c,memo);
	}
}
```
# Using Tabulation

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int maximumChocolates(int r, int c, int[][] grid) {
		// Write your code here.
		int dp[][][] = new int[r][c][c];
		for(int i=0;i<c;i++){
			for(int j=0;j<c;j++){
				if(i==j)dp[r-1][i][j] = grid[r-1][i];
				else dp[r-1][i][j] = grid[r-1][i] + grid[r-1][j];
			}
		}
		
		for(int i=r-2;i>=0;i--){
			for(int j1=0;j1<c;j1++){
				for(int j2=0;j2<c;j2++){
					int sum=grid[i][j1];
					if(j1!=j2)sum+=grid[i][j2];
					int prevSum = 0;
					for(int p=j1-1;p<=j1+1;p++){
						if(p==-1 || p==c)continue;
						for(int q=j2-1;q<=j2+1;q++){
							if(q==-1 || q==c)continue;
							prevSum = Math.max(prevSum,dp[i+1][p][q]);
						}
					}
					dp[i][j1][j2] = sum+prevSum;
				}
			}
		}
		return dp[0][0][c-1];
	}
}
```

OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int maximumChocolates(int r, int c, int[][] grid) {
		// Write your code here.
		int dp[][] = new int[c][c];
		for(int i=0;i<c;i++){
			for(int j=0;j<c;j++){
				if(i==j)dp[i][j] = grid[r-1][i];
				else dp[i][j] = grid[r-1][i] + grid[r-1][j];
			}
		}
		for(int i=r-2;i>=0;i--){
			int temp[][] = new int[c][c];
			for(int j1=0;j1<c;j1++){
				for(int j2=0;j2<c;j2++){
					int sum=grid[i][j1];
					if(j1!=j2)sum+=grid[i][j2];
					int prevSum = 0;
					for(int p=j1-1;p<=j1+1;p++){
						if(p==-1 || p==c)continue;
						for(int q=j2-1;q<=j2+1;q++){
							if(q==-1 || q==c)continue;
							prevSum = Math.max(prevSum,dp[p][q]);
						}
					}
					temp[j1][j2] = sum+prevSum;
				}
			}
			dp = temp;
		}
		return dp[0][c-1];
	}
}
```

OR

```java
public class Solution {
	public static int maximumChocolates(int r, int c, int[][] grid) {
		int[][] dp = new int[c][c];
		for (int j1 = 0; j1 < c; j1++) {
			for (int j2 = 0; j2 < c; j2++) {
				dp[j1][j2] = (j1 == j2) ? grid[r - 1][j1] : grid[r - 1][j1] + grid[r - 1][j2];
			}
		}
		for (int i = r - 2; i >= 0; i--) {
			int[][] temp = new int[c][c];
			for (int j1 = 0; j1 < c; j1++) {
				for (int j2 = 0; j2 < c; j2++) {
					int maxChoco = Integer.MIN_VALUE;
					for (int p = j1 - 1; p <= j1 + 1; p++) {
						for (int q = j2 - 1; q <= j2 + 1; q++) {
							if (p >= 0 && p < c && q >= 0 && q < c) {
								maxChoco = Math.max(maxChoco, dp[p][q]);
							}
						}
					}
					int curr = (j1 == j2) ? grid[i][j1] : grid[i][j1] + grid[i][j2];
					temp[j1][j2] = curr + maxChoco;
				}
			}
			dp = temp;
		}
		return dp[0][c - 1];
	}
}
```


OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int maximumChocolates(int r, int c, int[][] grid) {
		// Write your code here.
		int dp[][] = new int[c][c];
		for (int i = 0; i < c; i++) {
			for (int j = 0; j < c; j++) {
				if(i==j) {
					dp[i][j] = grid[r-1][i];
				} else {
					dp[i][j] = grid[r-1][i] + grid[r-1][j];
				}
			}
		}

		for (int i = r-2; i >= 0; i--) {
			int[][] temp = new int[c][c];
			for (int j1 = 0; j1 < c; j1++) {
				for (int j2 = 0; j2 < c; j2++) {
					int val = 0;
					for (int p = j1-1; p <= j1+1; p++) {
						if (p < 0 || p == c) continue;
						for (int q = j2-1; q <= j2+1; q++) {
							if (q < 0 || q == c) continue;
							val = Math.max(val, dp[p][q]);
						}
					}
					temp[j1][j2] = val + grid[i][j1];
					if(j1 != j2) temp[j1][j2] += grid[i][j2];
				}
			}
			dp = temp;
		}
		return dp[0][c-1];
	}
}
```


OR

```java
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int maximumChocolates(int r, int c, int[][] grid) {
		// Write your code here.
		int dp[][] = new int[c][c];
		for (int k = r-1; k >= 0; k--) {
			int cur[][] = new int[c][c];
			for (int i = 0; i < (c+1)/2; i++) {
				for (int j = i; j < c; j++) {
					int max = -1;
					for (int p = i-1; p <= i+1; p++) {
						for (int q = j-1; q <= j+1; q++) {
							if(p<0 || q<0 || p==c || q==c)continue;
							max = Math.max(max, dp[p][q]);
						}
					}
					cur[i][j] = grid[k][i] + max;
					if (i != j) {
						cur[i][j] += grid[k][j];
					}
				}
			}
			dp = cur;
		}
		return dp[0][c-1];
	}
}
```