[76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window**_ 

**_substring_**

 _of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window_. If there is no such substring, return _the empty string_ `""`.

The testcases will be generated such that the answer is **unique**.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"
**Output:** "BANC"
**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

**Example 2:**

**Input:** s = "a", t = "a"
**Output:** "a"
**Explanation:** The entire string s is the minimum window.

**Example 3:**

**Input:** s = "a", t = "aa"
**Output:** ""
**Explanation:** Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.

**Constraints:**

- `m == s.length`
- `n == t.length`
- `1 <= m, n <= 105`
- `s` and `t` consist of uppercase and lowercase English letters.


# Brute
1st Way
```java
class Solution {
    private boolean check(HashMap<Character,Integer> mp,HashMap<Character,Integer> db){
        for(char key:db.keySet()){
            if(mp.containsKey(key)){
                if(mp.get(key) < db.get(key))return false;
            }
            else return false;
        }
        return true;
    }
    public String minWindow(String s, String t) {
        int n= s.length();
        HashMap<Character,Integer> mp = new HashMap<>();
        HashMap<Character,Integer> db = new HashMap<>();
        for(char c:t.toCharArray()){
            db.put(c,db.getOrDefault(c,0)+1);
        }
        int mini=s.length();
        String ans="";
        for(int i=0;i<n;i++){
            mp.clear();
            for(int j=i;j<n;j++){
                char ch = s.charAt(j);
                mp.put(ch,mp.getOrDefault(ch,0)+1);
                if(check(mp,db)){
                    if(mini>=j-i+1){
                        ans = s.substring(i,j+1);
                        mini=j-i+1;
                    }
                    break;
                }
            }
        }
        return ans;
    }
}
```

2nd Way
```java
class Solution {
    public String minWindow(String s, String t) {
        int n  = s.length();
        int m = t.length();
        int minLen = n;
        int st=0,end=0;
        for(int i=0;i<n;i++){
            int hash[] = new int[256];
            for(int j=0;j<m;j++){
                hash[t.charAt(j)]++;
            }
            int cnt=0;
            for(int j=i;j<n;j++){
                char ch= s.charAt(j);
                if(hash[ch]>0)cnt++;
                hash[ch]--;
                if(cnt==m){
                    if(minLen>=j-i+1){
                        minLen = j-i+1;
                        st=i;
                        end=j+1;
                    }
                    break;
                }
            }
        }
        return s.substring(st,end);
    }
}
```
# Better

```java
class Solution {
    private boolean check(HashMap<Character,Integer> mp,HashMap<Character,Integer> db){
        for(char key:db.keySet()){
            if(mp.containsKey(key)){
                if(mp.get(key) < db.get(key))return false;
            }
            else return false;
        }
        return true;
    }
    public String minWindow(String s, String t) {
        int n= s.length();
        HashMap<Character,Integer> mp = new HashMap<>();
        HashMap<Character,Integer> db = new HashMap<>();
        for(char c:t.toCharArray()){
            db.put(c,db.getOrDefault(c,0)+1);
        }
        int minLen=s.length();
        String ans="";
        int j=0;
        for(int i=0;i<n;i++){
            char ch = s.charAt(i);
            mp.put(ch,mp.getOrDefault(ch,0)+1);
            if(check(mp,db)){
                while(!db.containsKey(s.charAt(j)) || mp.get(s.charAt(j))>db.get(s.charAt(j))){
                    mp.put(s.charAt(j),mp.get(s.charAt(j))-1);
                    if(mp.get(s.charAt(j))==0)mp.remove(s.charAt(j));
                    j++;
                }
                if(minLen>=i-j+1){
                    ans = s.substring(j,i+1);
                    minLen = i-j+1;
                }
            }
        }
        return ans;
    }
}
```



# Optimal

```java
class Solution {
    public String minWindow(String s, String t) {
        int n  = s.length();
        int m = t.length();
        int minLen = n;
        int st=-1,cnt=0;
        int hash[] = new int[256];
        for(int j=0;j<m;j++){
            hash[t.charAt(j)]++;
        }
        int j=0;
        for(int i=0;i<n;i++){
            char ch= s.charAt(i);
            if(hash[ch]>0)cnt++;
            hash[ch]--;

            while(cnt==m){
                if(minLen>=i-j+1){
                    minLen = i-j+1;
                    st=j;
                }
                hash[s.charAt(j)]++;
                if(hash[s.charAt(j)]>0)cnt--;
                j++;
            }
            
        }
        return (st==-1)?"":s.substring(st,st+minLen);
    }
}
```