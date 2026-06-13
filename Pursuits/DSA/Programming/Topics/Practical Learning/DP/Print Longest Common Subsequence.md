[Link](https://www.naukri.com/code360/problems/print-longest-common-subsequence_8416383?leftPanelTabValue=SUBMISSION)

## Problem statement 

Send feedback
You are given two strings **_‘s1’_** and **_‘s2’_**.
Return the longest common subsequence of these strings.

If there’s no such string, return an empty string. If there are multiple possible answers, return any such string.

**Note:**

```
Longest common subsequence of string ‘s1’ and ‘s2’ is the longest subsequence of ‘s1’ that is also a subsequence of ‘s2’. A ‘subsequence’ of ‘s1’ is a string that can be formed by deleting one or more (possibly zero) characters from ‘s1’.
```

**Example:**

```
Input: ‘s1’  = “abcab”, ‘s2’ = “cbab”

Output: “bab”

Explanation:
“bab” is one valid longest subsequence present in both strings ‘s1’ , ‘s2’.
```


# Using Recursion

```java
class Solution {
    private String helper(String s1,String s2,int i,int j){
        if(i==0)return s2.substring(0,j);
        if(j==0)return s1.substring(0,i);
        StringBuilder sb = new StringBuilder();
        if(s1.charAt(i-1) == s2.charAt(j-1)){
            sb.append((helper(s1,s2,i-1,j-1)) + s1.charAt(i-1));
        }
        else{
            String a = helper(s1,s2,i-1,j) + s1.charAt(i-1);
            String b = helper(s1,s2,i,j-1) + s2.charAt(j-1);
            sb.append((a.length() > b.length())?b:a);
        }
        return sb.toString();
    }
    public String shortestCommonSupersequence(String str1, String str2) {
        int n = str1.length();
        int m = str2.length();
        return helper(str1,str2,n,m);
    }
}
```

---
# Using Memoization

```java
public class Solution {
    private static String helper(String a,String b,int i,int j,String[][] memo){
        if(i<0 || j<0)return "";
        if(memo[i][j]!=null)return memo[i][j];
        StringBuilder sb = new StringBuilder();
        if(a.charAt(i) == b.charAt(j)){
            sb.append( helper(a,b,i-1,j-1,memo) + a.charAt(i));
        }
        else{
            StringBuilder s1 = new StringBuilder(helper(a,b,i-1,j,memo));
            StringBuilder s2 = new StringBuilder(helper(a,b,i,j-1,memo));
            sb.append((s1.length()>s2.length())?s1.toString():s2.toString());
        }
        return memo[i][j] = sb.toString();
    }
    public static String findLCS(int n, int m, String s1, String s2){
        // Write your code here.
        String memo[][] = new String[n][m];
        return helper(s1,s2,n-1,m-1,memo);
    }
}
```

---

```java
public class Solution {
    public static String findLCS(int n, int m, String s1, String s2){
        // Write your code here.
        StringBuilder[][] memo = new StringBuilder[n+1][m+1];
        return helper(s1, s2, n, m, new StringBuilder(), memo).toString();
    }
    private static StringBuilder helper(String s1, String s2, int i, int j, StringBuilder word, StringBuilder[][] memo) {
        if (i == 0 || j == 0) return new StringBuilder();
        if (memo[i][j] != null) return memo[i][j];
        if (s1.charAt(i-1) == s2.charAt(j-1)) {
            StringBuilder new_word = new StringBuilder(helper(s1, s2, i-1, j-1, new StringBuilder(word), memo));
            new_word.append(s1.charAt(i-1));
            return memo[i][j] = new_word;
        }
        StringBuilder w1 = helper(s1, s2, i-1, j, new StringBuilder(word), memo);
        StringBuilder w2 = helper(s1, s2, i, j-1, new StringBuilder(word), memo);
        if (w1.length() > w2.length()) return memo[i][j] = w1;
        return memo[i][j] = w2;
    }
}
```

# Using Tabulation

```java
public class Solution {
    public static String findLCS(int n, int m, String s1, String s2){
        // Write your code here.
        int dp[][] = new int[n+1][m+1];
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(s1.charAt(i-1) == s2.charAt(j-1)){
                    dp[i][j] = 1 + dp[i-1][j-1];
                }
                else{
                    dp[i][j] = Math.max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
        int i=n;
        int j=m;
        StringBuilder sb = new StringBuilder();
        while(i>0 && j>0){
            if(s1.charAt(i-1) == s2.charAt(j-1)){
                sb.append(s1.charAt(i-1));
                i--;j--;
            }
            else{
                if(dp[i-1][j]>dp[i][j-1]){
                    i--;
                }
                else j--;
            }
        }
        return sb.reverse().toString();
    }
}
```

OR

```java
public class Solution {
    public static String findLCS(int n, int m, String s1, String s2){
        // Write your code here.
        int[][] dp = new int[n+1][m+1];
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (s1.charAt(i-1) == s2.charAt(j-1)) {
                    dp[i][j] = 1 + dp[i-1][j-1];
                } else {
                    dp[i][j] = Math.max(dp[i][j-1], dp[i-1][j]);
                }
            }
        }

        int i = n, j = m;
        StringBuilder sb = new StringBuilder();
        while (i != 0 && j != 0) {
            if (s1.charAt(i-1) == s2.charAt(j-1)) {
                sb.append(s1.charAt(i-1));
                i--;
                j--;
            } else {
                if (dp[i][j-1] > dp[i-1][j]) j--;
                else i--;
            }
        }
        return sb.reverse().toString();
    }
}
```