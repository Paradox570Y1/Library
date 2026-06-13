[1358. Number of Substrings Containing All Three Characters](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/)

Given a string `s` consisting only of characters _a_, _b_ and _c_.

Return the number of substrings containing **at least** one occurrence of all these characters _a_, _b_ and _c_.

**Example 1:**

**Input:** s = "abcabc"
**Output:** 10
**Explanation:** The substrings containing at least one occurrence of the characters _a_, _b_ and _c are "_abc_", "_abca_", "_abcab_", "_abcabc_", "_bca_", "_bcab_", "_bcabc_", "_cab_", "_cabc_"_ and _"_abc_"_ (**again**)_._ 

**Example 2:**

**Input:** s = "aaacb"
**Output:** 3
**Explanation:** The substrings containing at least one occurrence of the characters _a_, _b_ and _c are "_aaacb_", "_aacb_"_ and _"_acb_"._ 

**Example 3:**

**Input:** s = "abc"
**Output:** 1

**Constraints:**

- `3 <= s.length <= 5 x 10^4`
- `s` only consists of _a_, _b_ or _c_ characters.

# Brute
TC-> O(N²)
SC-> O(1)
```java
class Solution {
    public int numberOfSubstrings(String s) {
        int n = s.length();
        int ans=0;
        for(int i=0;i<n;i++){
            int hash[] = new int[3];
            for(int j=i;j<n;j++){
                int ele = s.charAt(j)-'a';
                hash[ele]++;
                if(hash[0]>0 && hash[1]>0 && hash[2]>0)ans++;
            }
        }
        return ans;
    }
}
```

# Better Brute
TC-> O(N²)
SC-> O(1)
```java
class Solution {
    public int numberOfSubstrings(String s) {
        int n = s.length();
        int ans=0;
        for(int i=0;i<n;i++){
            int hash[] = new int[3];
            for(int j=i;j<n;j++){
                int ele = s.charAt(j)-'a';
                hash[ele]++;
                if(hash[0]>0 && hash[1]>0 && hash[2]>0){
                    ans+= (n-j);
                    break;
                }
            }
        }
        return ans;
    }
}
```

# Better
TC-> O(2N)
SC-> O(1)

```java
class Solution {
    public int numberOfSubstrings(String s) {
        int n = s.length();
        int ans=0;
        int hash[] = new int[3];
        int j=0;
        for(int i=0;i<n;i++){
            hash[s.charAt(i)-'a']++;
            while(hash[0]>0 && hash[1]>0 && hash[2]>0){
                ans+=n-i;
                hash[s.charAt(j++)-'a']--;
            }
        }
        return ans;
    }
}
```
here we are counting no. of subarrays to right of window

```java
class Solution {
    public int numberOfSubstrings(String s) {
        int n = s.length();
        int ans=0;
        int hash[] = new int[3];
        int j=0;
        for(int i=0;i<n;i++){
            hash[s.charAt(i)-'a']++;
            while(hash[0]>0 && hash[1]>0 && hash[2]>0){
                hash[s.charAt(j++)-'a']--;
            }
            ans+= j;
        }
        return ans;
    }
}
```

# Optimal
TC-> O(N)
SC-> O(1)
```java
class Solution {
    public int numberOfSubstrings(String s) {
        int ans=0;
        int hash[] = new int[3];
        hash[0] = hash[1] = hash[2] = -1;
        for(int i=0;i<s.length();i++){
            hash[s.charAt(i)-'a']= i;
            if(hash[0] != -1 && hash[1] != -1 && hash[2] !=-1){
                ans += 1 + Math.min(hash[0],Math.min(hash[1],hash[2]));
            }
        }
        return ans;
    }
}
```
counting no. of subarrays to the left of the window
# Best Runtime
TC-> O(N)
SC-> O(1)
```java
class Solution {
    public int numberOfSubstrings(String s) {
        int ans=0;
        int lastIndex[] = new int[3];
        for(int i=0;i<3;i++)lastIndex[i]=-1;
        for(int i=0;i<s.length();i++){
            lastIndex[s.charAt(i)-'a']= i;
            int mini=Integer.MAX_VALUE;
            for(int k=0;k<3;k++){
                mini = Math.min(mini,lastIndex[k]);
            }
            ans+=mini+1;
        }
        return ans;
    }
}
```

```java
class Solution {
    public int numberOfSubstrings(String s) {
        int hash[] = new int[3];
        int ans=0;
        for(int i=0;i<s.length();i++){
            hash[s.charAt(i)-'a']= i+1;
            int mini=hash[0];
            for(int j=1;j<3;j++)mini = Math.min(hash[j],mini);
            ans+=mini;
        }
        return ans;
    }
}
```