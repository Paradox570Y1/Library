[Link](https://www.geeksforgeeks.org/problems/matrix-chain-multiplication0303/1)
Given an array **arr[]** which represents **the** dimensions of a sequence of matrices where the **ith** matrix has the dimensions **(arr[i-1] x arr[i])** for i>=1, find the most efficient way to multiply these matrices together. The efficient way is the one that involves the least number of multiplications.

**Examples:**

**Input:** arr[] = [2, 1, 3, 4]
**Output:** 20
**Explanation:** There are 3 matrices of dimensions 2 × 1, 1 × 3, and 3 × 4, Let this 3 input matrices be M1, M2, and M3. There are two ways to multiply: ((M1 x M2) x M3) and (M1 x (M2 x M3)), note that the result of (M1 x M2) is a 2 x 3 matrix and result of (M2 x M3) is a 1 x 4 matrix. ((M1 x M2) x M3)  requires (2 x 1 x 3) + (2 x 3 x 4) = 30 
(M1 x (M2 x M3))  requires (1 x 3 x 4) + (2 x 1 x 4) = 20. The minimum of these two is 20.

**Input:** arr[] = [1, 2, 3, 4, 3]
**Output:** 30
**Explanation:** There are 4 matrices of dimensions 1 × 2, 2 × 3, 3 × 4, 4 × 3. Let this 4 input matrices be M1, M2, M3 and M4. The minimum number of multiplications are obtained by ((M1 x M2) x M3) x M4). The minimum number is (1 x 2 x 3) + (1 x 3 x 4) + (1 x 4 x 3) = 30.

**Input:** arr[] = [3, 4]
**Output:** 0  
**Explanation:** As there is only one matrix so, there is no cost of multiplication.

**Constraints:**   
2 ≤ arr.size() ≤ 100  
1 ≤ arr[i] ≤ 200


# Theory

- You will be given an entire array you need to solve it in particular pattern.
- In this the pattern is to try different ways to make partitions  and sub partitions of the array.
![[Pasted image 20250814184738.png|300]]
- There will be a start point and a end point.
![[Pasted image 20250814185048.png|300]]

Example:
![[Pasted image 20250814185116.png|350]]
![[Pasted image 20250814185129.png|350]]

So, these problems require partition DP.
- For array of size `N` there are `N-1` matrix possible.
![[Pasted image 20250814185310.png|400]]

# Steps to solve this problem
1. Start with entire block/array and always represent them with `f(i,j)` where i is start point and j is end point.
	- Partitioning will be like making pairs and inside either partition in pair their could be more pair.
	![[Pasted image 20250814185647.png|340]]
2. Try all pair of partitions using a loop.
	- You will be taking size of 1st partition and the remaining length will become size of 2nd partition.
	- Two ways to run a loop. Just indexing is different.
	![[Pasted image 20250814191146.png|400]]
	
3. Return the best two partitions.
	![[Pasted image 20250814190139.png|400]]
4. Now write the base case.
	- Base case is when `i==j` which represent a single matrix and a single matrix does 0 operations as there is no other matrix to multiply with.
	- So at `i==j` return 0.

![[Pasted image 20250814192817.png|400]]




# Using recursion

```java
class Solution {
    static int helper(int arr[], int i, int j) {
        if (i == j) return 0;
        int ans = Integer.MAX_VALUE;
        for(int k = i; k < j; k++){
            int op = arr[i-1] * arr[k] * arr[j];
            ans = Math.min(op + helper(arr, i, k) + helper(arr, k+1, j),ans);
        }
        return ans;
    }
    static int matrixMultiplication(int arr[]) {
        // code here
        int n = arr.length;
        return helper(arr, 1, n-1);
    }
}
```


# Using Memoization

```java
class Solution {
    static int helper(int arr[], int i, int j, int[][] memo) {
        if (i == j) return 0;
        if(memo[i][j] != -1)return memo[i][j];
        int ans = Integer.MAX_VALUE;
        for(int k = i; k < j; k++){
            int op = arr[i-1] * arr[k] * arr[j];
            ans = Math.min(op + helper(arr, i, k, memo) + helper(arr, k+1, j, memo),ans);
        }
        return memo[i][j] = ans;
    }
    static int matrixMultiplication(int arr[]) {
        // code here
        int n = arr.length;
        int memo[][] = new int[n][n];
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++){
                memo[i][j] = -1;
            }
        }
        return helper(arr, 1, n-1,memo);
    }
}
```

# Bottom Up DP method (Tabulation)

```java
class Solution {
    static int matrixMultiplication(int arr[]) {
        // code here
        int n = arr.length;
        int dp[][] = new int[n][n];
        for(int i = 1; i < n; i++) {
            dp[i][i] = 0;
        }
        
        for (int i = n-2; i>=1; i--){
            for (int j = i+1; j<n; j++){
                int ans = Integer.MAX_VALUE;
                for (int k = i; k < j; k++) {
                    int op = arr[i-1] * arr[k] * arr[j];
                    ans = Math.min(ans, op + dp[i][k] + dp[k+1][j]);
                }
                dp[i][j] = ans;
            }                             
        }
        return dp[1][n-1];
    }
}
```

OR

```java
class Solution {
    static int matrixMultiplication(int arr[]) {
        // code here
        int n = arr.length;
        int dp[][] = new int[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(dp[i], (int) 1e9);
            dp[i][i] = 0;
        }
        for (int i = 2; i < n ; i++) {
            for (int j = i-1; j > 0; j--) {
                for (int k = j; k < i; k++) {
                    int mul = arr[j-1] * arr[k] * arr[i];
                    dp[j][i] = Math.min(dp[j][i], mul + dp[j][k] + dp[k+1][i]);
                }
            }
        }
        return dp[1][n-1];
    }
}
```
here we do M1xM2 , M2xM3, M1xM2xM3, M3xM4, M2xM3xM4, M1xM2xM3xM4 and so on

OR
This DP transition is different then others
```java
class Solution {
    static int matrixMultiplication(int arr[]) {
        // code here
        int n = arr.length;
        int dp[][] = new int[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(dp[i], (int) 1e9);
            dp[i][i] = 0;
        }
        for (int mat = 2; mat < n; mat++) {
            for (int i = 1; i <= n-mat; i++) {
                int j = i+mat-1;
                for (int k = i; k < j; k++) {
                    int mul = arr[i-1] * arr[k] * arr[j];
                    dp[i][j] = Math.min(dp[i][j], mul + dp[i][k] + dp[k+1][j]);
                }
            }
        }
        return dp[1][n-1];
    }
}
```

here we calculate M1xM2 , M2xM3, M3xM4 etc. first then proceed with (M1xM2xM3) then (M2xM3xM4) and so on. So at first we take 2 matrix pairs then 3 matrix pairs then 4 and so on.