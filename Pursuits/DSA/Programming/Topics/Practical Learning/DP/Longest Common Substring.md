[Link](https://www.naukri.com/code360/problems/longest-common-substring_1235207?leftPanelTabValue=PROBLEM)

## Problem statement

Send feedback

You are given two strings, _**'str1'**_ and _**'str2'**_. You have to find the length of the longest common substring.
A substring is a continuous segment of a string. For example, "bcd" is a substring of "abcd", while "acd" or "cda" are not.

**Example:**

```
Input: ‘str1’ = “abcjklp” , ‘str2’ = “acjkp”.

Output: 3

Explanation:  The longest common substring between ‘str1’ and ‘str2’ is “cjk”, of length 3.
```

Detailed explanation ( Input/output format, Notes, Images )

##### Sample Input 1:

```
wasdijkl
wsdjkl
```

##### Sample Output 1:

```
 3
```

##### Explanation Of Sample Input 1 :

```
 The longest common substring is “jkl”, of length 3.
```

##### Sample Input 2:

```
tyfg
cvbnuty
```

##### Sample Output 2:

```
2
```

##### Explanation Of Sample Input 2 :

```
The longest common substring is “ty”, of length 2.
```

##### Expected time complexity:

```
The expected time complexity is O(n*m),
Where ‘n’ and ‘m’ are the lengths of ‘st1’ and ‘str2’ respectively.
```

##### Constraints:

```
1 <= str1.length <= 1000
1 <= str2.length <= 1000
```

# Using Recursion

```java
// User function Template for Java

class Solution {
    int ans;
    private int helper(String s1,String s2,int i,int j){
        if(i==0 || j==0)return 0;
        int cnt=0;
        if(s1.charAt(i-1) == s2.charAt(j-1)){
            cnt = 1+helper(s1,s2,i-1,j-1);
        }
        else{
            ans = Math.max(ans,Math.max(helper(s1,s2,i-1,j),helper(s1,s2,i,j-1)));
            return 0;
        }
        ans = Math.max(ans,cnt);
        return cnt;
    }
    public int longestCommonSubstr(String s1, String s2) {
        // code here
        ans=0;
        helper(s1,s2,s1.length(),s2.length());
        return this.ans;
    }
}
```
OR
```java
// User function Template for Java

class Solution {
    private int helper(String s1,String s2,int i,int j,int cnt){
        if(i==0 || j==0)return cnt;
        if(s1.charAt(i-1) == s2.charAt(j-1)){
            cnt = helper(s1,s2,i-1,j-1,cnt+1);
        }
        cnt = Math.max(cnt,Math.max(helper(s1,s2,i-1,j,0),helper(s1,s2,i,j-1,0)));
        return cnt;
    }
    public int longestCommonSubstr(String s1, String s2) {
        // code here
        return helper(s1,s2,s1.length(),s2.length(),0);
    }
}
```
# Using Memoization

But not as efficient as tabulation
![[Pasted image 20250731190838.png]]
```java
public class Solution {
    private static int helper(String str1,String str2,int n,int m,int len,int[][][] memo){
        if(n==-1 || m==-1)return len;
        if(memo[n][m][len] != 0)return memo[n][m][len];
        int curLen=len;
        if(str1.charAt(n) ==  str2.charAt(m)){
            len = helper(str1,str2,n-1,m-1,len+1,memo);
        }
        int res = Math.max(helper(str1,str2,n-1,m,0,memo),helper(str1,str2,n,m-1,0,memo));
        len = Math.max(len,res);
        return memo[n][m][curLen] =  len;
    }
    public static int lcs(String str1, String str2){
        // Write your code here.
        int n = str1.length();
        int m = str2.length();
        int memo[][][] = new int[n][m][Math.min(n,m)+1];
        return helper(str1,str2,n-1,m-1,0,memo);
    }
}
```

OR

```java
// User function Template for Java

class Solution {
    int memo[][][];
    private int helper(String s1,String s2,int i,int j,int cnt){
        if(i==0 || j==0)return cnt;
        if(memo[i][j][cnt]!=-1)return memo[i][j][cnt];
        
        int match=cnt;
        if(s1.charAt(i-1) == s2.charAt(j-1)){
            match = helper(s1,s2,i-1,j-1,cnt+1);
        }
        
        int res = Math.max(match,Math.max(
            helper(s1,s2,i-1,j,0),
            helper(s1,s2,i,j-1,0)
        ));
        
        return memo[i][j][cnt] = res;
    }
    public int longestCommonSubstr(String s1, String s2) {
        // code here
        int n = s1.length();
        int m = s2.length();
        memo = new int[n+1][m+1][Math.min(n,m)+1];
        for(int i=0;i<=n;i++){
            for(int j=0;j<=m;j++){
                Arrays.fill(memo[i][j],-1);
            }
        }
        return helper(s1,s2,n,m,0);
    }
}
```

OR
Still gives TLE so prefer DP approach
```java
public class Solution {
    public static int lcs(String str1, String str2){
        // Write your code here.
        int n = str1.length(), m = str2.length();
        int[][][] memo = new int[n][m][Math.min(n, m)];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                for (int k = 0; k < Math.min(n, m); k++) {
                    memo[i][j][k] = -1;
                }
            }
        }
        return helper(str1, str2, n-1, m-1, 0, memo);
    }
    private static int helper(String str1, String str2, int i, int j, int c, int[][][] memo) {
        if (i < 0 || j < 0) return c;
        if (memo[i][j][c] != -1) return memo[i][j][c];
        int cnt = c;
        if (str1.charAt(i) == str2.charAt(j)) {
            cnt = helper(str1, str2, i-1, j-1, c+1, memo);
        }
        cnt = Math.max(cnt, helper(str1, str2, i-1, j, 0, memo));
        cnt = Math.max(cnt, helper(str1, str2, i, j-1, 0, memo));
        return memo[i][j][c] = cnt;
    }
}

```
# Using Tabulation

```java
public class Solution {
    public static int lcs(String str1, String str2){
        // Write your code here.
        int n = str1.length();
        int m = str2.length();
        int dp[][] = new int[n][m];
        int maxi = 0;
        for(int i=0;i<n;i++){
            char ch = str1.charAt(i);
            for(int j=0;j<m;j++){
                if(ch == str2.charAt(j)){
                    dp[i][j] = 1;
                    if(i>0 && j>0) dp[i][j] +=dp[i-1][j-1];
                }
                maxi = Math.max(maxi,dp[i][j]);
            }
        }
        return maxi;
    }
}

```

OR
```java
// User function Template for Java

class Solution {
    public int longestCommonSubstr(String s1, String s2) {
        // code here
        int n = s1.length();
        int m = s2.length();
        int dp[] = new int[m+1];
        int ans=0;
        for(int i=1;i<=n;i++){
            int cur[] = new int[m+1];
            for(int j=1;j<=m;j++){
                int match=0;
                int notMatch=-1;
                if(s1.charAt(i-1) == s2.charAt(j-1)){
                    match = dp[j-1]+1;
                    cur[j] = match;
                }
                else{
                    notMatch = Math.max(cur[j-1],dp[j]);
                    cur[j] = 0;
                }
                ans = Math.max(ans,Math.max(match,notMatch));
            }
            dp = cur;
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    public int longestCommonSubstr(String s1, String s2) {
        // code here
        int n = s1.length();
        int m = s2.length();
        int dp[] = new int[m+1];
        int ans=0;
        for(int i=1;i<=n;i++){
            int cur[] = new int[m+1];
            for(int j=1;j<=m;j++){
                if(s1.charAt(i-1) == s2.charAt(j-1)){
                    cur[j] = dp[j-1]+1;
                    ans = Math.max(ans,cur[j]);
                }
            }
            dp = cur;
        }
        return ans;
    }
}
```

OR

```java
public class Solution {
    public static int lcs(String str1, String str2){
        // Write your code here.
        int n = str1.length();
        int m = str2.length();
        int[] dp = new int[m+1];
        int max = 0;
        for (int i = 0; i < n; i++) {
            int prev = 0;
            for (int j = 1; j <= m; j++) {
                int buffer = dp[j];
                if (str1.charAt(i) == str2.charAt(j-1)) {
                    dp[j] = 1 + prev;
                    max = Math.max(max, dp[j]);
                } else {
                    dp[j] = 0;
                }
                prev = buffer;
            }
        }
        return max;
    }
}
```