[Link](https://www.geeksforgeeks.org/problems/rod-cutting0840/1)

Difficulty: **Medium**Accuracy: **60.66%**Submissions: **161K+**Points: **4**Average Time: **20m**

Given a rod of length **n**(size of price) inches and an array of prices, **price**. price[i] denotes the value of a piece of length i. Determine the **maximum** value obtainable by cutting up the rod and selling the pieces.

**Example:**

**Input:** price[] = [1, 5, 8, 9, 10, 17, 17, 20]  
**Output:** 22  
**Explanation:** The maximum obtainable value is 22 by cutting in two pieces of lengths 2 and 6, i.e., 5+17=22.

**Input:** price[] = [3, 5, 8, 9, 10, 17, 17, 20]  
**Output:** 24  
**Explanation:** The maximum obtainable value is 24 by cutting the rod into 8 pieces of length 1, i.e, 8*price[1]= 8*3 = 24.  

**Input:** price[] = [1, 10, 3, 1, 3, 1, 5, 9]  
**Output:** 40

**Constraints:**  
1 ≤ price.size() ≤ 103  
1 ≤ price[i] ≤ 106

# Brute
- **Exponential (O(2^n))** due to redundant calculations of overlapping subproblems.

```java
class Solution {
    public int cutRod(int[] price) {
        // code here
        return helper(price,price.length);
    }
    int helper(int[] price,int rodLen){
        if(rodLen==0)return 0;
        int maxVal=0;
        int curVal=0;
        for(int i=1;i<rodLen+1;i++){
            curVal = price[i-1]+ helper(price,rodLen-i);
            maxVal = Math.max(curVal,maxVal);
        }
        return maxVal;
    }
}
```


### Memoization (Top-Down DP) Approach (O(n²) Time)

```java
class Solution {
    public int cutRod(int[] price) {
        // code here
        int n = price.length;
        int dp[] = new int[n];
        return helper(price,n,dp);
    }
    int helper(int[] price,int rodLen,int[] dp){
        if(rodLen==0)return 0;
        int maxVal=0;
        int curVal=0;
        for(int i=1;i<rodLen+1;i++){
            if(dp[rodLen-i]==0){
                curVal = price[i-1]+ helper(price,rodLen-i,dp);
                dp[rodLen-i] = curVal-price[i-1];
            }
            else curVal = price[i-1] + dp[rodLen-i];
            maxVal = Math.max(curVal,maxVal);
        }
        return maxVal;
    }
}
```
OR
```java
class Solution {
    public int cutRod(int[] price) {
        return helper(price,price.length,new int[price.length+1]);
    }
    public int helper(int[] price , int rodLen,int memo[]){
        if(rodLen==0)return 0;
        if(memo[rodLen]>0)return memo[rodLen];
        int ans = 0;
        for(int i=1;i<=rodLen;i++){
            int cost = price[i-1] + helper(price,rodLen-i,memo);
            ans = Math.max(ans,cost);
        }
        memo[rodLen] = ans;
        return ans;
    }
}
```

### Bottom-Up DP Approach (O(n²) Time)

```java
class Solution {
    public int cutRod(int[] price) {
        int n = price.length;
        int dp[] = new int[n+1];
        int ans = 0;
        for(int i=1;i<=n;i++){
            int maxi = 0;
            for(int j=1;j<=i;j++){
                maxi = Math.max(maxi,price[j-1]+dp[i-j]);
            }
            dp[i] = maxi;
            ans = Math.max(ans,maxi);
        }
        return ans;
    }
}
```