[509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)

The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.

Given `n`, calculate `F(n)`.

**Example 1:**

**Input:** n = 2
**Output:** 1
**Explanation:** F(2) = F(1) + F(0) = 1 + 0 = 1.

**Example 2:**

**Input:** n = 3
**Output:** 2
**Explanation:** F(3) = F(2) + F(1) = 1 + 1 = 2.

**Example 3:**

**Input:** n = 4
**Output:** 3
**Explanation:** F(4) = F(3) + F(2) = 2 + 1 = 3.

**Constraints:**

- `0 <= n <= 30`

# Using recursion

```java
class Solution {
    public int fib(int n) {
        if(n<=1)return n;
        return fib(n-1)+fib(n-2);
    }
}
```

# Using Memoization

```java
class Solution {
    private int helper(int i,int[] dp){
        if(i<=1)return i;
        if(dp[i]!=-1)return dp[i];
        return dp[i] = helper(i-1,dp) + helper(i-2,dp);
    }
    public int fib(int n) {
        int[] dp= new int[n+1];
        Arrays.fill(dp,-1);
        return helper(n,dp);
    }
}
```


# Using Tabulation

Without space optimization
```java
class Solution {
    public int fib(int n) {
        if(n==0)return 0;
        int[] dp= new int[n+1];
        dp[0] = 0;
        dp[1] = 1;
        for(int i=2;i<n+1;i++){
            dp[i] = dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
}
```


After Optimizing space
```java
class Solution {
    public int fib(int n) {
        if(n==1)return n;
        int prev1 = 0;
        int prev2 = 1;
        int cur=0;
        for(int i=2;i<n+1;i++){
            cur = prev1+prev2;
            prev1 = prev2;
            prev2 = cur;
        }
        return cur;
    }
}
```








# Generate Fibonacci sequence

We will be using the example of Fibonacci numbers here. The following series is called the Fibonacci series:

**0,1,1,2,3,5,8,13,21,...**

We need to find the nth Fibonacci number, where n is based on a 0-based index.

# Using Memoization

```java
import java.util.Scanner;
class Main {
    private static int generate(int[] dp,int n){
        if(dp[n]!=-1)return dp[n];
        if(n<=1)return dp[n]=n;
        dp[n-1] = generate(dp,n-1);
        dp[n-2] = generate(dp,n-2);
        return dp[n] = dp[n-1]+dp[n-2];
    }
    public static void main(String[] args) {
        int n;
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        int[] dp = new int[n+1];
        //or Arrays.fill(dp,-1);
        for(int i=0;i<n+1;i++){
            dp[i] = -1;
        }
        generate(dp,n);
        for(int i=0;i<n+1;i++){
            System.out.print(dp[i]+" ");
        }
    }
}
```

OR

```java
import java.util.Scanner;
import java.util.Arrays;
class Main {
    private static int generate(int[] dp,int n){
        if(n<=1)return dp[n]=n; // if you don't do dp[n] = n then
							    // base cases will remain -1
        if(dp[n]!=-1)return dp[n];
        return dp[n] = generate(dp,n-1)+generate(dp,n-2);
    }
    public static void main(String[] args) {
        int n;
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        int[] dp = new int[n+1];
        Arrays.fill(dp,-1);
        generate(dp,n);
        for(int i=0;i<n+1;i++){
            System.out.print(dp[i]+" ");
        }
    }
}
```
# Using Tabulation

Without Optimization
```java
import java.util.Scanner;
import java.util.Arrays;
class Main {
    public static void main(String[] args) {
        int n;
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        int[] dp = new int[n+1];
        dp[0]=0;
        dp[1]=1;
        for(int i=2;i<n+1;i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        for(int i=0;i<n+1;i++){
            System.out.print(dp[i]+" ");
        }
    }
}
```

