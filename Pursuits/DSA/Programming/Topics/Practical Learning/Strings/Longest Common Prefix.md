[14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

**Input:** strs = ["flower","flow","flight"]
**Output:** "fl"

**Example 2:**

**Input:** strs = ["dog","racecar","car"]
**Output:** ""
**Explanation:** There is no common prefix among the input strings.

**Constraints:**

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters.

TC=> O(n\*m)
Others Solution
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs==null || strs.length==0) return "";
        String ans = strs[0];
        for(int i=0;i<strs.length;i++){
            while(strs[i].indexOf(ans)!=0)
            ans = ans.substring(0,ans.length()-1);
        }
        return ans;
    }
}
```

Mine Solution
```cpp
class Solution {
    public String longestCommonPrefix(String[] strs) {
        int n = strs.length;
        int m=strs[0].length();
        int k=m-1;
        for(int i=1;i<n;i++){
            m = Math.min(m,strs[i].length());
            if(m==0) return "";
            for(int j=0;j<m;j++){
                if(strs[i].charAt(j)!=strs[0].charAt(j)){k= Math.min(j-1,k);break;}
                else if(j==m-1) k=Math.min(k,j);
            }

        }
        return strs[0].substring(0,k+1);
    }
}
```