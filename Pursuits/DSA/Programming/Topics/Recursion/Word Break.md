[139. Word Break](https://leetcode.com/problems/word-break/)

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

**Input:** s = "leetcode", wordDict = ["leet","code"]
**Output:** true
**Explanation:** Return true because "leetcode" can be segmented as "leet code".

**Example 2:**

**Input:** s = "applepenapple", wordDict = ["apple","pen"]
**Output:** true
**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.

**Example 3:**

**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
**Output:** false

**Constraints:**

- `1 <= s.length <= 300`
- `1 <= wordDict.length <= 1000`
- `1 <= wordDict[i].length <= 20`
- `s` and `wordDict[i]` consist of only lowercase English letters.
- All the strings of `wordDict` are **unique**.
# Brute
TC->O(2^n)
```java
class Solution {
    boolean check(String s,List<String> wordDict,int i,String curr){
        if(i==s.length()){
            if(wordDict.contains(curr))return true;
            return false;
        }
        if(check(s,wordDict,i+1,curr+s.charAt(i)))return true;
        if(wordDict.contains(curr)){
            if(check(s,wordDict,i+1,""+s.charAt(i)))return true;
        }
        return false;
    }
    public boolean wordBreak(String s, List<String> wordDict) {
        return check(s,wordDict,0,"");
    }
}
```

OR

```java
class Solution {
    boolean check(String s,List<String> wordDict,int i){
        if(i==s.length()){
            return true;
        }
        String curr= "";
        for(int j=i;j<s.length();j++){
            curr+=s.charAt(j);
            if(wordDict.contains(curr)){
                if(check(s,wordDict,j+1)){
                    return true;
                }
            }
        }
        return false;
    }
    public boolean wordBreak(String s, List<String> wordDict) {
        return check(s,wordDict,0);
    }
}
```

OR

```java
class Solution {
    HashSet<String> dict;
    String s;
    private boolean check(int st,int end){
        if(end==s.length()){
            return (st==s.length());
        }
        if(dict.contains(s.substring(st,end+1))){
            if(check(end+1,end+1))return true;
        }
        if(check(st,end+1))return true;
        return false;
    }
    public boolean wordBreak(String s, List<String> wordDict) {
        this.dict = new HashSet<>();
        for(String word:wordDict){
            dict.add(word);
        }
        this.s = s;
        return check(0,0);
    }
}
```


Using [[memoization]] 
TC-> O(n^2)
```java
class Solution {
    boolean check(String s,List<String> wordDict,int i,HashMap<Integer,Boolean> memo){
        if(i==s.length()){
            return true;
        }
        if(memo.containsKey(i))return memo.get(i);
        String curr= "";
        for(int j=i;j<s.length();j++){
            curr+=s.charAt(j);
            if(wordDict.contains(curr)){
                if(check(s,wordDict,j+1,memo)){
                    memo.put(i,true);
                    return true;
                }
            }
        }
        memo.put(i,false);
        return false;
    }
    public boolean wordBreak(String s, List<String> wordDict) {
        HashMap<Integer,Boolean> memo = new HashMap<>();
        return check(s,wordDict,0,memo);
    }
}
```

# Better

Here i have used `Boolean` Wrapper class which has default value of `null`
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> hs = new HashSet(wordDict);
        Boolean memo[] = new Boolean[s.length()];
        return helper(s,hs,0,memo);
    }
    boolean helper(String s, HashSet<String> hs,int st,Boolean memo[]){
        if(st== s.length()){
            return true;
        }
        if(memo[st] != null)return memo[st];
        for(int end=st+1;end<=s.length();end++){
            String temp = s.substring(st,end);
            if(hs.contains(temp)){
                if(helper(s,hs,end,memo))return true;
            }
        }
        memo[st] = false;
        return false;
    }
}
```

OR

```java
class Solution {
    HashSet<String> dict;
    String s;
    Boolean[] memo;
    private boolean check(int st,int end){
        if(end==s.length()){
            return (st==end);
        }
        if(memo[st]!=null)return memo[st];
        if(dict.contains(s.substring(st,end+1))){
            if(check(end+1,end+1)){
                return memo[st]=true;
            }
        }
        if(check(st,end+1))return true;
        return memo[st] = false;
    }
    public boolean wordBreak(String s, List<String> wordDict) {
        this.dict = new HashSet<>();
        for(String word:wordDict){
            dict.add(word);
        }
        this.s = s;
        this.memo = new Boolean[s.length()];
        return check(0,0);
    }
}
```


Different way using only one index
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> hs = new HashSet(wordDict);
        StringBuilder sb = new StringBuilder();
        boolean memo[] = new boolean[s.length()];
        return helper(s,hs,0,memo);
    }
    boolean helper(String s, HashSet<String> hs,int i,boolean[] memo){
        if(i== s.length()){
            return true;
        }
        if(memo[i] == true)return false;
        StringBuilder sb = new StringBuilder();
        for(int j=i;j<s.length();j++){
            sb.append(s.charAt(j));
            String temp = sb.toString();
            if(hs.contains(temp)){
                if(helper(s,hs,j+1,memo))return true;
            }
        }
        memo[i] = true;
        return false;
    }
}
```

Without using wrapper class

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> hs = new HashSet(wordDict);
        boolean memo[] = new boolean[s.length()];
        return helper(s,hs,0,memo);
    }
    boolean helper(String s, HashSet<String> hs,int st,boolean memo[]){
        if(st== s.length()){
            return true;
        }
        if(memo[st] == true)return false;
        for(int end=st+1;end<=s.length();end++){
            String temp = s.substring(st,end);
            if(hs.contains(temp)){
                if(helper(s,hs,end,memo))return true;
            }
        }
        memo[st] = true;
        return false;
    }
}
```