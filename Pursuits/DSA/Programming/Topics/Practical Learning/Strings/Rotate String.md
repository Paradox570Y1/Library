[796. Rotate String](https://leetcode.com/problems/rotate-string/)

Given two strings `s` and `goal`, return `true` _if and only if_ `s` _can become_ `goal` _after some number of **shifts** on_ `s`.

A **shift** on `s` consists of moving the leftmost character of `s` to the rightmost position.

- For example, if `s = "abcde"`, then it will be `"bcdea"` after one shift.

**Example 1:**

**Input:** s = "abcde", goal = "cdeab"
**Output:** true

**Example 2:**

**Input:** s = "abcde", goal = "abced"
**Output:** false

**Constraints:**

- `1 <= s.length, goal.length <= 100`
- `s` and `goal` consist of lowercase English letters.

# Brute
TC-> O(N²)
```java
class Solution {
    public boolean rotateString(String s, String goal) {
        if(s.length() != goal.length())return false;
        String doubled = s+s;
        for(int i=0;i<doubled.length();i++){
            char ele = doubled.charAt(i);
            int j=0;
            if(ele != goal.charAt(j))continue;
            int k=i;
            while(k<doubled.length() && j<goal.length() && doubled.charAt(k)==goal.charAt(j)){
                k++;j++;
            }
            if(j==goal.length())return true;
            else j=0;
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean rotateString(String s, String goal) {
        
        StringBuilder sb = new StringBuilder(s);
        if(s.equals(goal))return true;
        for(int k=1;k<s.length();k++){
            char temp = sb.charAt(0);
            for(int i=1;i<s.length();i++){
                sb.setCharAt(i-1,sb.charAt(i));
            }
            sb.setCharAt(s.length()-1,temp);
            if(sb.toString().equals(goal))return true;
        }
        return false;
    }
}
```

# Optimal
TC-> O(N)
```java
class Solution {
    public boolean rotateString(String s, String goal) {
        if (s.length() != goal.length()) return false;
        String doubled = s + s;
        return doubled.contains(goal);
    }
}
```