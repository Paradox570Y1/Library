[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

**Input:** s = "()"

**Output:** true

**Example 2:**

**Input:** s = "()[]{}"

**Output:** true

**Example 3:**

**Input:** s = "(]"

**Output:** false

**Example 4:**

**Input:** s = "([])"

**Output:** true

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of parentheses only `'()[]{}'`.


```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st  = new Stack();
        for(int i=0;i<s.length();i++){
            char ele = s.charAt(i);
            if(ele == '(' || ele == '[' || ele == '{')st.push(ele);
            else if(st.size()==0)return false;
            else if(ele == ')' && st.peek() == '(' || ele == ']' && st.peek() == '[' || ele == '}' && st.peek() == '{')st.pop();
            else return false;
        }
        return st.isEmpty();
    }
}
```

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Integer> st  = new Stack();
        for(int i=0;i<s.length();i++){
            char ele = s.charAt(i);
            if(ele == '(')st.push(0);
            else if(ele=='[')st.push(1);
            else if(ele=='{')st.push(2);
            else if(st.size()==0)return false;
            else if(ele == ')'){
                if(st.peek() == 0)st.pop();
                else return false;
            }
            else if(ele==']'){
                if(st.peek() == 1)st.pop();
                else return false;
            }
            else if(ele =='}'){
                if(st.peek() == 2)st.pop();
                else return false;
            }
        }
        return st.isEmpty();
    }
}
```