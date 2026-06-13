[438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)
Given two strings `s` and `p`, return an array of all the start indices of `p`'s 

anagrams

 in `s`. You may return the answer in **any order**.

**Example 1:**

**Input:** s = "cbaebabacd", p = "abc"
**Output:** [0,6]
**Explanation:**
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".

**Example 2:**

**Input:** s = "abab", p = "ab"
**Output:** [0,1,2]
**Explanation:**
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".

**Constraints:**

- `1 <= s.length, p.length <= 3 * 104`
- `s` and `p` consist of lowercase English letters.


# Brute

```java
class Solution {
    boolean isAnagram(String s,int i,int j,String p){
        int[] hash = new int[26];
        int st=i;
        for(;i<=j;i++){
            hash[s.charAt(i)-'a']++;
            hash[p.charAt(i-st)-'a']--;
        }
        for(int k=0;k<26;k++)if(hash[k]!=0)return false;
        return true;
    }
    public List<Integer> findAnagrams(String s, String p) {
        int n = s.length();
        int m = p.length();
        List<Integer> ans = new ArrayList<>();
        for(int i=0;i<n;i++){
            int j= i+m-1;
            if(j>=n)break;
            if(isAnagram(s,i,j,p))ans.add(i);
        }
        return ans;
    }
}
```

