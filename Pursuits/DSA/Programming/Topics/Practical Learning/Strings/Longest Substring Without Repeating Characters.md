[3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string `s`, find the length of the **longest** **substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"
**Output:** 3
**Explanation:** The answer is "abc", with the length of 3.

**Example 2:**

**Input:** s = "bbbbb"
**Output:** 1
**Explanation:** The answer is "b", with the length of 1.

**Example 3:**

**Input:** s = "pwwkew"
**Output:** 3
**Explanation:** The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

**Constraints:**

- `0 <= s.length <= 5 * 104`
- `s` consists of English letters, digits, symbols and spaces.


# Better
	
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s.length()==0)return 0;
        int i=0,j=0;
        HashSet<Character> hs = new HashSet<>();
        int cnt = 0;
        int ans = 0;
        while(j<s.length()){
            char ch = s.charAt(j);
            if(hs.contains(ch)){
                char start = s.charAt(i);
                hs.remove(start);
                cnt--;
                i++;
            }
            else{
                hs.add(ch);
                cnt++;
                j++;
            }
            if(ans<cnt)ans = cnt;
        }
        return ans;

    }
}
```

giving better runtime
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s.length()==0)return 0;
        int i=0,j=0;
        char[] arr = s.toCharArray();
        HashSet<Character> hs = new HashSet<>();
        int ans = 0;
        while(j<arr.length){
            while(hs.contains(arr[j])){
                hs.remove(arr[i++]);
            }
            hs.add(arr[j]);
            j++;
            ans = Math.max(ans,j-i);
        }
        return ans;

    }
}
```


```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashSet<Character> hs = new HashSet<>();
        int ans=0;
        int j=0;
        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            while(hs.contains(ch)){
                hs.remove(s.charAt(j++));
            }
            hs.add(ch);
            ans = Math.max(ans,i-j+1);
        }
        return ans;
    }
}
```


# Optimal
TC -> O(N)
SC -> O(128)
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int hash[] = new int[128];
        for(int i=0;i<128;i++){
            hash[i] = -1;
        }
        int j=0,ans=0;
        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            if(hash[ch]>=j){
                j= hash[ch]+1;
            }
            hash[ch]=i;
            ans = Math.max(ans,i-j+1);
        }
        return ans;
    }
}
```


100% runtime
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int hash[] = new int[128];
        int j=0,ans=0;
        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            if(hash[ch]>=j){
                j= hash[ch];
            }
            hash[ch]=i+1;
            ans = Math.max(ans,i-j+1);
        }
        return ans;
    }
}
```