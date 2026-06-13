[224. Basic Calculator](https://leetcode.com/problems/basic-calculator/)

Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return _the result of the evaluation_.

**Note:** You are **not** allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

**Example 1:**

**Input:** s = "1 + 1"
**Output:** 2

**Example 2:**

**Input:** s = " 2-1 + 2 "
**Output:** 3

**Example 3:**

**Input:** s = "(1+(4+5+2)-3)+(6+8)"
**Output:** 23

**Constraints:**

- `1 <= s.length <= 3 * 105`
- `s` consists of digits, `'+'`, `'-'`, `'('`, `')'`, and `' '`.
- `s` represents a valid expression.
- `'+'` is **not** used as a unary operation (i.e., `"+1"` and `"+(2 + 3)"` is invalid).
- `'-'` could be used as a unary operation (i.e., `"-1"` and `"-(2 + 3)"` is valid).
- There will be no two consecutive operators in the input.
- Every number and running calculation will fit in a signed 32-bit integer.



# Better

Using Stack

```java
class Solution {
    public int calculate(String s) {
        int n  = s.length();
        int res = 0;
        int num = 0;
        int sign = 1;
        Stack<Integer> st = new Stack();
        st.push(sign);
        for(int i=0;i<n;i++){
            char ch = s.charAt(i);
            if(ch>='0' && ch<='9'){
                num = num*10+(ch-'0');
            }
            else if(ch == '+' || ch == '-'){
                res += sign*num;
                sign = st.peek()* (ch=='+'?1:-1);
                num=0;
            }
            else if(ch=='(')st.push(sign);
            else if(ch==')')st.pop();
        }
        if(num!=0)res+=num*sign;
        return res;
    }
}
```

Stack using array
90% runtime
```java
class Solution {
    public int calculate(String s) {
        int n  = s.length();
        int res = 0;
        int num = 0;
        int sign = 1;
        int st[] = new int[n/2 + 1];
        st[0] = sign;
        int top = 0;
        for(int i=0;i<n;i++){
            char ch = s.charAt(i);
            if(ch>='0' && ch<='9'){
                num = num*10+(ch-'0');
            }
            else if(ch == '+' || ch == '-'){
                res += sign*num;
                sign = st[top]* (ch=='+'?1:-1);
                num=0;
            }
            else if(ch=='(')st[++top] = sign;
            else if(ch==')')top--;
        }
        if(num!=0)res+=num*sign;
        return res;
    }
}
```


# Optimal 

Using recursion
```java
class Solution {
    public int calculate(String s) {
        return helper(s);
    }
    int i=0;
    int helper(String s){
        int num=0;
        int res = 0;
        int sign = 1;
        while(i<s.length()){
            char ch= s.charAt(i);
            i++;
            if(ch>='0' && ch<='9'){
                num = num*10 + (ch-'0');
            }
            else if(ch=='+'){
                res += sign*num;
                sign = 1;
                num=0;
            }
            else if(ch=='-'){
                res+=sign*num;
                sign=-1;
                num=0;
            }
            else if(ch=='('){
                num = helper(s);
            }
            else if(ch==')'){
                res += num*sign;
                return res;
            }
        }
        res+=num*sign;
        return res;
    }
}
```

More about above recursion technique

![[Pasted image 20250301173623.png]]

![[Pasted image 20250301173740.png|300]]
