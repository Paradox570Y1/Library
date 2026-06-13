[1781. Sum of Beauty of All Substrings](https://leetcode.com/problems/sum-of-beauty-of-all-substrings/)

The **beauty** of a string is the difference in frequencies between the most frequent and least frequent characters.

- For example, the beauty of `"abaacc"` is `3 - 1 = 2`.

Given a string `s`, return _the sum of **beauty** of all of its substrings._

**Example 1:**

**Input:** s = "aabcb"
**Output:** 5
**Explanation:** The substrings with non-zero beauty are ["aab","aabc","aabcb","abcb","bcb"], each with beauty equal to 1.

**Example 2:**

**Input:** s = "aabcbaa"
**Output:** 17

**Constraints:**

- `1 <= s.length <= 500`
- `s` consists of only lowercase English letters.

# Brute

TC-> O(N³)


```java
class Solution {
    public int beautySum(String s) {
        int ans=0;
        
        for(int i=0;i<s.length();i++){
            HashMap<Character,Integer> mp = new HashMap<>();
            for(int j = i;j<s.length();j++){
                mp.put(s.charAt(j),mp.getOrDefault(s.charAt(j),0)+1);
                int mini = Integer.MAX_VALUE,maxi = Integer.MIN_VALUE;
                for(int val:mp.values()){
                    mini = Math.min(mini,val);
                    maxi = Math.max(maxi,val);
                }
                ans += (maxi-mini);
            }
        }
        return ans;
    }
}
```


```java
class Solution {
    public int beautySum(String s) {
        int ans=0;
        for(int i=0;i<s.length();i++){
            int hash[] = new int[26];
            int maxi = 0;
            for(int j = i;j<s.length();j++){
                int curr = s.charAt(j)-'a';
                hash[curr]++;
                maxi =  Math.max(maxi,hash[curr]);
                int mini = s.length();
                for(int k=0;k<hash.length;k++){
                    if(hash[k]!=0 )mini = Math.min(mini,hash[k]);
                }
                ans += (maxi-mini);
            }
        }
        return ans;
    }
}
```

