[1903. Largest Odd Number in String](https://leetcode.com/problems/largest-odd-number-in-string/)

You are given a string `num`, representing a large integer. Return _the **largest-valued odd** integer (as a string) that is a **non-empty substring** of_ `num`_, or an empty string_ `""` _if no odd integer exists_.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

**Input:** num = "52"
**Output:** "5"
**Explanation:** The only non-empty substrings are "5", "2", and "52". "5" is the only odd number.

**Example 2:**

**Input:** num = "4206"
**Output:** ""
**Explanation:** There are no odd numbers in "4206".

**Example 3:**

**Input:** num = "35427"
**Output:** "35427"
**Explanation:** "35427" is already an odd number.

TC=> O(N)
```java
class Solution {
    public String largestOddNumber(String num) {
        int n = num.length();
        int i=n-1;
        while(i>=0){
            int c=num.charAt(i)-'0';
            if(c%2==1) break;
            i--;
        }
        if(i<0) return "";
        return num.substring(0,i+1);
    }
}
```
