[Boolean Parenthesization](https://www.geeksforgeeks.org/problems/boolean-parenthesization5610/1)

You are given a boolean expression **s** containing  
    'T' ---> true  
    'F' ---> false   
and following operators between symbols  
   &   ---> boolean AND  
    |   ---> boolean OR  
   ^   ---> boolean XOR  
Count the number of ways we can **parenthesize** the expression so that the value of expression evaluates to **true**.

Note: The answer is guaranteed to fit within a **32-bit** integer.

**Examples:**

**Input:** s = "T|T&F^T"
**Output:** 4
**Explaination:** The expression evaluates to true in 4 ways: ((T|T)&(F^T)), (T|(T&(F^T))), (((T|T)&F)^T) and (T|((T&F)^T)).

**Input:** s = "T^F|F"
**Output:** 2
**Explaination:** The expression evaluates to true in 2 ways: ((T^F)|F) and (T^(F|F)).

**Constraints:**  
1 ≤ |s| ≤ 100


# Recursion

```java
// User function Template for Java
class Solution {
    private static int helper(String s, int i, int j, int isTrue) {
        if (i > j) return 0;
        if (i == j) {
            if (isTrue == 1) {
                return (s.charAt(i) == 'T') ? 1 : 0;
            } else {
                return (s.charAt(i) == 'F') ? 1 : 0;
            }
        }
        
        int ways = 0;
        for (int k = i + 1; k < j; k+=2) {
            int leftT = helper(s, i, k - 1, 1);
            int leftF = helper(s, i, k - 1, 0);
            int rightT = helper(s, k + 1, j, 1);
            int rightF = helper(s, k + 1, j, 0);
            
            char op = s.charAt(k);
            
            if (op == '&') {
                if (isTrue == 1) {
                    ways += leftT * rightT;
                } else {
                    ways += (leftF * rightF) + (leftT * rightF) + (leftF * rightT);
                }
            }
            else if (op == '|') {
                if (isTrue == 1) {
                    ways += (leftT * rightT) + (leftT * rightF) + (leftF * rightT);
                } else {
                    ways += (leftF * rightF);
                }
            }
            else {
                if (isTrue == 1) {
                    ways += (leftT * rightF) + (leftF * rightT);
                } else {
                    ways += (leftT * rightT) + (leftF * rightF);
                }
            }
        }
        return ways;
    }
    static int countWays(String s) {
        // code here
        int n = s.length();
        return helper(s,0,n-1,1);
    }
}
```


# Memoization

```java
// User function Template for Java
class Solution {
    static int memo[][][];
    private static int helper(String s, int i, int j, int isTrue) {
        if (i > j) {
            return 0;
        }
        if (i == j) {
            if (isTrue == 1) {
                return (s.charAt(i) == 'T') ? 1 : 0;
            } else {
                return (s.charAt(i) == 'F') ? 1 : 0;
            }
        }
        if (memo[i][j][isTrue] != -1) {
            return memo[i][j][isTrue];
        }
        int ways = 0;
        for (int k = i + 1; k < j; k+=2) {
            int leftT = helper(s, i, k - 1, 1);
            int leftF = helper(s, i, k - 1, 0);
            int rightT = helper(s, k + 1, j, 1);
            int rightF = helper(s, k + 1, j, 0);
            
            char op = s.charAt(k);
            
            if (op == '&') {
                if (isTrue == 1) {
                    ways += leftT * rightT;
                } else {
                    ways += (leftF * rightF) + (leftT * rightF) + (leftF * rightT);
                }
            }
            else if (op == '|') {
                if (isTrue == 1) {
                    ways += (leftT * rightT) + (leftT * rightF) + (leftF * rightT);
                } else {
                    ways += (leftF * rightF);
                }
            }
            else {
                if (isTrue == 1) {
                    ways += (leftT * rightF) + (leftF * rightT);
                } else {
                    ways += (leftT * rightT) + (leftF * rightF);
                }
            }
        }
        return memo[i][j][isTrue] = ways;
    }
    static int countWays(String s) {
        // code here
        int n = s.length();
        memo = new int[n][n][2];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                memo[i][j][0] = -1;
                memo[i][j][1] = -1;
            }
        }
        return helper(s,0,n-1,1);
    }
}
```


# DP

```java
// User function Template for Java
class Solution {
    
    static int countWays(String s) {
        // code here
        int n = s.length();
        int dp[][][] = new int[n][n][2];
        for (int i = 0; i < n; i += 2) {
            if (s.charAt(i) == 'T') {
                dp[i][i][1] = 1;
            } else {
                dp[i][i][0] = 1;
            }
        }
        
        for (int i = n-1; i >= 0; i -= 2) {
            for (int j = i + 2; j < n; j += 2) {
                for (int isTrue = 0; isTrue <= 1; isTrue++) {
                    int ways = 0;
                    for (int k = i + 1; k < j; k+=2) {
                        int leftT = dp[i][k - 1][1];
                        int leftF = dp[i][k - 1][0];
                        int rightT = dp[k + 1][j][1];
                        int rightF = dp[k + 1][j][0];
                        
                        char op = s.charAt(k);
                        
                        if (op == '&') {
                            if (isTrue == 1) {
                                ways += leftT * rightT;
                            } else {
                                ways += (leftF * rightF) + (leftT * rightF) + (leftF * rightT);
                            }
                        }
                        else if (op == '|') {
                            if (isTrue == 1) {
                                ways += (leftT * rightT) + (leftT * rightF) + (leftF * rightT);
                            } else {
                                ways += (leftF * rightF);
                            }
                        }
                        else {
                            if (isTrue == 1) {
                                ways += (leftT * rightF) + (leftF * rightT);
                            } else {
                                ways += (leftT * rightT) + (leftF * rightF);
                            }
                        }
                    }
                    dp[i][j][isTrue] = ways;
                }
            }
        }
        return dp[0][n - 1][1];
    }
}
```

OR

```java
// User function Template for Java
class Solution {
    
    static int countWays(String s) {
        // code here
        int n = s.length();
        int dp[][][] = new int[n][n][2];
        for (int i = 0; i < n; i += 2) {
            if (s.charAt(i) == 'T') {
                dp[i][i][1] = 1;
            } else {
                dp[i][i][0] = 1;
            }
        }
        
        for (int len = 3; len <= n; len += 2) {
            for (int i = 0; i + len - 1 < n; i += 2) {
                int j = i + len - 1;
                for (int isTrue = 0; isTrue <= 1; isTrue++) {
                    int ways = 0;
                    for (int k = i + 1; k < j; k+=2) {
                        int leftT = dp[i][k - 1][1];
                        int leftF = dp[i][k - 1][0];
                        int rightT = dp[k + 1][j][1];
                        int rightF = dp[k + 1][j][0];
                        
                        char op = s.charAt(k);
                        
                        if (op == '&') {
                            if (isTrue == 1) {
                                ways += leftT * rightT;
                            } else {
                                ways += (leftF * rightF) + (leftT * rightF) + (leftF * rightT);
                            }
                        }
                        else if (op == '|') {
                            if (isTrue == 1) {
                                ways += (leftT * rightT) + (leftT * rightF) + (leftF * rightT);
                            } else {
                                ways += (leftF * rightF);
                            }
                        }
                        else {
                            if (isTrue == 1) {
                                ways += (leftT * rightF) + (leftF * rightT);
                            } else {
                                ways += (leftT * rightT) + (leftF * rightF);
                            }
                        }
                    }
                    dp[i][j][isTrue] = ways;
                }
            }
        }
        return dp[0][n - 1][1];
    }
}
```

OR

```java
// User function Template for Java
class Solution {
    static boolean evalOp(boolean i, boolean j, char op) {
        if (op == '|') {
            return (i|j);
        } else if(op == '&') {
            return (i&j);
        }
        return (i^j);
    }
    static int[] evaluate(char op, int[] v1, int[] v2) {
        int res[] = new int[2];
        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < 2; j++) {
                int id = (evalOp((i == 1)?true:false, (j == 1)?true:false, op))?1:0;
                res[id] += v1[i] * v2[j];
            }
        }
        return res;
    }
    static int countWays(String s) {
        // code here
        int n = s.length();
        int dplen = n/2+1;
        int[][][] dp = new int[dplen][dplen][2];
        
        for (int i = 0; i < dplen; i++) {
            int id = (s.charAt(2*i) == 'T')?1:0;
            dp[i][i][id] = 1;
        }
        for (int j = 1; j < dplen;  j++) {
            for (int i = j-1; i >= 0; i--) {
                for (int k = 2*i+1; k < 2*j; k+=2) {
                    int buffer[] = evaluate(s.charAt(k), dp[i][(k-1)/2], dp[(k+1)/2][j]);
                    dp[i][j][0] += buffer[0];
                    dp[i][j][1] += buffer[1];
                }
            }
        }
        return dp[0][dplen-1][1];
    }
}
```