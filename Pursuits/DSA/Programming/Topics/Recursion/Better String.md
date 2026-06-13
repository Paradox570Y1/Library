[Link](https://www.geeksforgeeks.org/problems/better-string/1)
### Better String

Difficulty: **Hard**Accuracy: **44.5%**Submissions: **83K+**Points: **8**

Given a pair of strings of equal lengths, Geek wants to find the **better string**. The **better string** is the string having more number of **distinct** **subsequences**.  
If both the strings have equal count of distinct subsequence then return **str1**.

**Example 1:**

**Input:**
str1 = "gfg", str2 = "ggg"
**Output:** "gfg"
**Explanation: "**gfg" have 6 distinct subsequences whereas "ggg" have 3 distinct subsequences. 

**Example 2:**

**Input:** str1 = "a", str2 = "b"
**Output:** "a"
**Explanation:** Both the strings have only 1 distinct subsequence. 

**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **betterString()** which takes **str1** and **str2** as input parameters and returns the better string.

**Expected Time Complexity:** O( N ), where **N** is the length of both provided strings.

**Expected Auxiliary Space:** O( N )

**Constraints:**  
1 <= N <= 30

# Basic recursion

TC-> O(2^n)
The current implementation generates all distinct subsequences, leading to a time complexity of O(2^n), which is infeasible for large inputs. To improve the time efficiency and meet the time constraints, we need to avoid explicitly generating all subsequences and instead use a **dynamic programming approach** to count the number of distinct subsequences.

```java
class Solution {
    static int findDistinct(String s,HashSet<String> hs,String out){
        if(s.length() == 0){
            hs.add(out);
            return hs.size();
        }
        findDistinct(s.substring(1),hs,out+s.charAt(0));
        findDistinct(s.substring(1),hs,out);
        return hs.size();
    }
    public static String betterString(String str1, String str2) {
        // Code here
        int cnt1 = findDistinct(str1,new HashSet<>(),"");
        int cnt2 = findDistinct(str2,new HashSet<>(),"");
        if(cnt1<cnt2){
            return str2;
        }
        return str1;
    }
}
```

```java
class Solution {
    static void findDistinct(String s,HashSet<String> hs,String out){
        if(s.length() == 0){
            hs.add(out);
            return;
        }
        findDistinct(s.substring(1),hs,out+s.charAt(0));
        findDistinct(s.substring(1),hs,out);
    }
    static int findDistinctCnt(String s){
        HashSet<String> hs = new HashSet<>();
        findDistinct(s,hs,"");
        return hs.size();
    }
    public static String betterString(String str1, String str2) {
        // Code here
        int cnt1 = findDistinctCnt(str1);
        int cnt2 = findDistinctCnt(str2);
        if(cnt1<cnt2){
            return str2;
        }
        return str1;
    }
}
```

OR

```java
class Solution {
    private static void cntSubsequence(String s,HashSet<String> hs,int i,StringBuilder sb){
        if(i==s.length()){
            hs.add(sb.toString());
            return;
        }
        cntSubsequence(s,hs,i+1,sb);
        sb.append(s.charAt(i));
        cntSubsequence(s,hs,i+1,sb);
        sb.setLength(sb.length()-1);
    }
    private static int subsequence(String s){
        HashSet<String> hs = new HashSet<>();
        cntSubsequence(s,hs,0,new StringBuilder());
        return hs.size();
    }
    public static String betterString(String s1, String s2) {
        // Code here
        if(subsequence(s1)<subsequence(s2))return s2;
        return s1;
    }
}
```

# Using DP

Dynamic Programming (DP) is a powerful technique used to solve problems by breaking them down into smaller subproblems, solving each subproblem once, and storing its solution. This avoids redundant calculations and is particularly useful for optimization problems.


```java
class Solution {
    static int findDistinct(String s){
        HashMap<Character,Integer> mp = new HashMap<>();
        int dp[] = new int[s.length()+1];
        dp[0] = 1;
        for(int i=0;i<s.length();i++){
            char ele = s.charAt(i);
            dp[i+1] =2 * dp[i];
            if(mp.containsKey(ele)) dp[i+1] -= dp[mp.get(ele)];
            mp.put(ele,i);
        }
        return dp[s.length()];
    }
    public static String betterString(String str1, String str2) {
        // Code here
        int cnt1 = findDistinct(str1);
        int cnt2 = findDistinct(str2);
        if(cnt1<cnt2){
            return str2;
        }
        return str1;
    }
}
```

# Optimal

```java
class Solution {
    public static int generate(String s){
        int n = s.length();
        int[] dp = new int[n+1];
        dp[0] = 1;
        int hash[] = new int[26];
        for(int i=0;i<26;i++)hash[i]=-1;
        for(int i=0;i<n;i++){
            int ch = s.charAt(i)-'a';
            dp[i+1] = dp[i]*2;
            if(hash[ch]!=-1)dp[i+1]-=dp[hash[ch]];
            hash[ch] = i;
        }
        return dp[n];
    }
    public static String betterString(String str1, String str2) {
        // Code here
        int cnt1= generate(str1);
        int cnt2= generate(str2);
        if(cnt1>=cnt2)return str1;
        return str2;
    }
}
```