[242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)


Given two strings `s` and `t`, return `true` if `t` is an 

anagram

 of `s`, and `false` otherwise.

**Example 1:**

**Input:** s = "anagram", t = "nagaram"

**Output:** true

**Example 2:**

**Input:** s = "rat", t = "car"

**Output:** false

**Constraints:**

- `1 <= s.length, t.length <= 5 * 104`
- `s` and `t` consist of lowercase English letters.

# Better
TC=> O(n)  
SC => O(300)

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length())return false;
        int hash1[] = new int[150];
        int hash2[] = new int[150];
        
        for(int i=0;i<s.length();i++){
            hash1[s.charAt(i)]++;
            hash2[t.charAt(i)]++;
        }
        for(int i=0;i<150;i++){
            if(hash1[i] != hash2[i])return false;
        }
        return true;
    }
}
```

# Slightly Better

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length())return false;
        //for lowercase letters
        int hash[] = new int[26];
        
        for(int i=0;i<s.length();i++){
            hash[s.charAt(i)-'a']++;
            hash[t.charAt(i)-'a']--;
        }
        for(int i=0;i<26;i++){
            if(hash[i]!=0)return false;
        }
        return true;
    }
}
```

# Optimal
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length())return false;
        int hash[] = new int[26];
        
        for(char c:s.toCharArray()){
            hash[c-'a']++;
        }
        for(char c:t.toCharArray()){
            if(--hash[c-'a']<0)return false;
        }
        for(int count:hash){
            if(count!=0)return false;
        }
        return true;
    }
}
```

**NOTE**
Another approach is to sort the strings and then iterate and compare which takes O(nlogn+mlogm) time complexity and O(1) space