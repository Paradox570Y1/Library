### Longest Substring with K Uniques

Difficulty: **Medium**Accuracy: **34.65%**Submissions: **177K+**Points: **4**

Given a string **s**, you need to print the size of the longest possible substring with exactly **k unique** characters. If no possible substring exists, print -1.

**Examples:**

**Input:** s = "aabacbebebe", k = 3
**Output:** 7
**Explanation**: "cbebebe" is the longest substring with 3 distinct characters.

**Input**: s = "aaaa", k = 2
**Output:** -1
**Explanation**: There's no substring with 2 distinct characters.  

**Input:** s = "aabaaab", k = 2
**Output:** 7
**Explanation**: "aabaaab" is the longest substring with 2 distinct characters.

**Constraints:**  
1 ≤ s.size() ≤ 105  
1 ≤ k ≤ 26  
All characters are lowercase letters


# Better

```java
class Solution {
    public int longestkSubstr(String s, int k) {
        // code here
        HashMap<Character,Integer> mp = new HashMap<>();
        int ans=-1;
        int j=0;
        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            mp.put(ch,mp.getOrDefault(ch,0)+1);
            while(mp.size()>k){
                char ele = s.charAt(j);
                mp.put(ele,mp.get(ele)-1);
                if(mp.get(ele)==0)mp.remove(ele);
                j++;
            }
            if(mp.size()==k){
                ans = Math.max(ans,i-j+1);
            }
        }
        return ans;
    }
}
```


```java
class Solution {
    public int longestkSubstr(String s, int k) {
        // code here
        HashMap<Character,Integer> mp = new HashMap<>();
        int ans=-1;
        int j=0;
        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            mp.put(ch,mp.getOrDefault(ch,0)+1);
            if(mp.size()>k){
                char ele = s.charAt(j);
                mp.put(ele,mp.get(ele)-1);
                if(mp.get(ele)==0)mp.remove(ele);
                j++;
            }
            else if(mp.size()==k){
                ans = Math.max(ans,i-j+1);
            }
        }
        return ans;
    }
}
```


# Optimal

```java
class Solution {
    public int longestkSubstr(String s, int k) {
        // code here
        HashMap<Character,Integer> mp = new HashMap<>();
        int ans=-1;
        int j=0;
        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            mp.put(ch,mp.getOrDefault(ch,0)+1);
            if(mp.size()>k){
                char ele = s.charAt(j);
                mp.put(ele,mp.get(ele)-1);
                if(mp.get(ele)==0)mp.remove(ele);
                j++;
            }
            else if(mp.size()==k){
                ans = Math.max(ans,i-j+1);
            }
        }
        return ans;
    }
}
```