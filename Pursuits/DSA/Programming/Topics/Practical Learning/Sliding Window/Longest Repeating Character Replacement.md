[424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return _the length of the longest substring containing the same letter you can get after performing the above operations_.

**Example 1:**

**Input:** s = "ABAB", k = 2
**Output:** 4
**Explanation:** Replace the two 'A's with two 'B's or vice versa.

**Example 2:**

**Input:** s = "AABABBA", k = 1
**Output:** 4
**Explanation:** Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of only uppercase English letters.
- `0 <= k <= s.length`


# Brute
TC-> O(N²)
SC-> O(N)
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int n = s.length();
        int ans=0;
        for(int i=0;i<n;i++){
            int subLen=0;
            int maxFreq=0;
            HashMap<Character,Integer> mp = new HashMap<>();
            for(int j=i;j<n;j++){
                subLen++;
                char ele = s.charAt(j);
                mp.put(ele,mp.getOrDefault(ele,0)+1);
                maxFreq = Math.max(maxFreq,mp.get(ele));
                int rest = subLen-maxFreq;
                if(rest<=k) ans = Math.max(ans,j-i+1);
                else break;
            }
        }
        return ans;
    }
}
```
TC-> O(N²)
SC-> O(26)
Little better but still TLE
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int n = s.length();
        int ans=0;
        for(int i=0;i<n;i++){
            int subLen=0;
            int maxFreq=0;
            int hash[] = new int[26];
            for(int j=i;j<n;j++){
                subLen++;
                int ele = s.charAt(j)-'A';
                hash[ele]++;
                maxFreq = Math.max(maxFreq,hash[ele]);
                int rest = subLen-maxFreq;
                if(rest<=k) ans = Math.max(ans,j-i+1);
                else break;
            }
        }
        return ans;
    }
}
```

# Better
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int n = s.length();
        int j=0;
        int hash[]  = new int[26];
        int maxCnt = 0;
        int ans=0;
        for(int i=0;i<n;i++){
            int ele = s.charAt(i)-'A';
            hash[ele]++;
            maxCnt = Math.max(maxCnt,hash[ele]);
            if((i-j+1)-maxCnt>k){
                hash[s.charAt(j)-'A']--;
                j++;
            }
            ans  = Math.max(ans,i-j+1);
        }
        return ans;
    }
}
```

# Optimal

TC-> O(2N x 26)
SC-> O(26)
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int n = s.length();
        int ans=0;
        int hash[] = new int[26];
        int j=0;
        int maxFreq=0;
        for(int i=0;i<n;i++){
            int ele = s.charAt(i)-'A';
            hash[ele]++;
            maxFreq = Math.max(maxFreq,hash[ele]);
            int wildCards = (i-j+1)-maxFreq;
            while(wildCards>k){
                int ch = s.charAt(j)-'A';
                hash[ch]--;
                maxFreq=0;
                for(int t=0;t<26;t++){
                    maxFreq = Math.max(maxFreq,hash[t]);
                }
                j++;
                wildCards = (i-j+1)-maxFreq;
            }
            ans = Math.max(ans,i-j+1);
        }
        return ans;
    }
}
```

TC-> O(N X 26)
Giving best runtime
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int n = s.length();
        int ans=0;
        int hash[] = new int[26];
        int j=0;
        int maxFreq=0;
        for(int i=0;i<n;i++){
            int ele = s.charAt(i)-'A';
            hash[ele]++;
            maxFreq = Math.max(maxFreq,hash[ele]);
            if((i-j+1)-maxFreq>k){
                int ch = s.charAt(j)-'A';
                hash[ch]--;
                maxFreq=0;
                for(int t=0;t<26;t++){
                    maxFreq = Math.max(maxFreq,hash[t]);
                }
                j++;
            }
            else ans = Math.max(ans,i-j+1);
        }
        return ans;
    }
}
```


TC -> O(N)

```java
class Solution {
    public int characterReplacement(String s, int k) {
        int n = s.length();
        int ans=0;
        int hash[] = new int[26];
        int j=0;
        int maxFreq=0;
        for(int i=0;i<n;i++){
            hash[s.charAt(i)-'A']++;
            maxFreq = Math.max(maxFreq,hash[s.charAt(i)-'A']);
            if((i-j+1)-maxFreq>k){
                hash[s.charAt(j)-'A']--;
                maxFreq=0;
                j++;
            }
            else ans = Math.max(ans,i-j+1);
        }
        return ans;
    }
}
```