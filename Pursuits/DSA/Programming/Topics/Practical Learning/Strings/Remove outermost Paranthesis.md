[1021. Remove Outermost Parentheses](https://leetcode.com/problems/remove-outermost-parentheses/)


A valid parentheses string is either empty `""`, `"(" + A + ")"`, or `A + B`, where `A` and `B` are valid parentheses strings, and `+` represents string concatenation.

- For example, `""`, `"()"`, `"(())()"`, and `"(()(()))"` are all valid parentheses strings.

A valid parentheses string `s` is primitive if it is nonempty, and there does not exist a way to split it into `s = A + B`, with `A` and `B` nonempty valid parentheses strings.

Given a valid parentheses string `s`, consider its primitive decomposition: `s = P1 + P2 + ... + Pk`, where `Pi` are primitive valid parentheses strings.

Return `s` _after removing the outermost parentheses of every primitive string in the primitive decomposition of_ `s`.

**Example 1:**

**Input:** s = "(()())(())"
**Output:** "()()()"
**Explanation:** 
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".

**Example 2:**

**Input:** s = "(()())(())(()(()))"
**Output:** "()()()()(())"
**Explanation:** 
The input string is "(()())(())(()(()))", with primitive decomposition "(()())" + "(())" + "(()(()))".
After removing outer parentheses of each part, this is "()()" + "()" + "()(())" = "()()()()(())".

**Example 3:**

**Input:** s = "()()"
**Output:** ""
**Explanation:** 
The input string is "()()", with primitive decomposition "()" + "()".
After removing outer parentheses of each part, this is "" + "" = "".

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is either `'('` or `')'`.
- `s` is a valid parentheses string.

TC=> O(N)
```cpp
class Solution {
public:
    string removeOuterParentheses(string s) {
        string ans="";
        int cnt=0;
        for(int i=0;i<s.length();i++){
            if(cnt==0){cnt=1;continue;}
            else ans+=s[i];
            if(s[i]=='(')cnt++;
            else cnt--;
            if(cnt==0) ans.pop_back();
        }
        return ans;
    }
};
```

Without using pop_back()
```cpp
class Solution {
public:
    string removeOuterParentheses(string s) {
        string ans="";
        int cnt=0;
        for(int i=0;i<s.length();i++){
            if(cnt==0){cnt=1;continue;}
            else if(cnt==1 && s[i]==')'){cnt=0;continue;}
            else ans+=s[i];
            if(s[i]=='(')cnt++;
            else cnt--;
        }
        return ans;
    }
};
```


In Java

```java
class Solution {
    public String removeOuterParentheses(String s) {
        StringBuilder sb = new StringBuilder();
        int cnt=0;
        for(char c:s.toCharArray()){
            if(cnt==0){cnt=1;continue;}
            else if(cnt==1 && c==')'){cnt=0;continue;}
            else sb.append(c);
            if(c=='(')cnt++;
            else cnt--;
        }
        return sb.toString();
    }
}
```

```java
class Solution {
    public String removeOuterParentheses(String s) {
        StringBuilder sb = new StringBuilder();
        int cnt=0;
        for(int i=0;i<s.length();i++){
            char c= s.charAt(i);
            if(cnt==0){cnt=1;continue;}
            else if(cnt==1 && c==')'){cnt=0;continue;}
            else sb.append(c);
            if(c=='(')cnt++;
            else cnt--;
        }
        return sb.toString();
    }
}
```

OR

```java
class Solution {
    public String removeOuterParentheses(String s) {
        StringBuilder sb = new StringBuilder();
        int cnt=0;
        for(char ch:s.toCharArray()){
            if(ch=='('){
                if(cnt!=0)sb.append(ch);
                cnt++;
            }
            else{
                cnt--;
                if(cnt!=0)sb.append(ch);
            }
        }
        return sb.toString();
    }
}
```