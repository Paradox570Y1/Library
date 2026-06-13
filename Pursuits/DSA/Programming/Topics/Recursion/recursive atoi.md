[8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer.

The algorithm for `myAtoi(string s)` is as follows:

1. **Whitespace**: Ignore any leading whitespace (`" "`).
2. **Signedness**: Determine the sign by checking if the next character is `'-'` or `'+'`, assuming positivity if neither present.
3. **Conversion**: Read the integer by skipping leading zeros until a non-digit character is encountered or the end of the string is reached. If no digits were read, then the result is 0.
4. **Rounding**: If the integer is out of the 32-bit signed integer range `[-231, 231 - 1]`, then round the integer to remain in the range. Specifically, integers less than `-231` should be rounded to `-231`, and integers greater than `231 - 1` should be rounded to `231 - 1`.

Return the integer as the final result.

**Example 1:**

**Input:** s = "42"

**Output:** 42

**Explanation:**

The underlined characters are what is read in and the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^

**Example 2:**

**Input:** s = " -042"

**Output:** -42

**Explanation:**

Step 1: "   -042" (leading whitespace is read and ignored)
            ^
Step 2: "   -042" ('-' is read, so the result should be negative)
             ^
Step 3: "   -042" ("042" is read in, leading zeros ignored in the result)
               ^

**Example 3:**

**Input:** s = "1337c0d3"

**Output:** 1337

**Explanation:**

Step 1: "1337c0d3" (no characters read because there is no leading whitespace)
         ^
Step 2: "1337c0d3" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "1337c0d3" ("1337" is read in; reading stops because the next character is a non-digit)
             ^

**Example 4:**

**Input:** s = "0-1"

**Output:** 0

**Explanation:**

Step 1: "0-1" (no characters read because there is no leading whitespace)
         ^
Step 2: "0-1" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "0-1" ("0" is read in; reading stops because the next character is a non-digit)
          ^

**Example 5:**

**Input:** s = "words and 987"

**Output:** 0

**Explanation:**

Reading stops at the first non-digit character 'w'.

**Constraints:**

- `0 <= s.length <= 200`
- `s` consists of English letters (lower-case and upper-case), digits (`0-9`), `' '`, `'+'`, `'-'`, and `'.'`.


Using Recursion
```java
class Solution {
    int eval(String t){
        int n =t.length()-1;
        int res = 1;
        for(int i=0;i<n;i++){
            res*=10;
        }
        return res;
    }
    int generate(String s,int i,boolean isNeg,int val){
        if(s.length() == i){
            return val;
        }
        char ch = s.charAt(i);
        if(ch == ' '){
            if(val==0 && (i-1<0 || s.charAt(i-1) ==' '))return generate(s,i+1,isNeg,val);
            return val;
        }
        if(ch =='-' && val==0 && (i-1<0 || s.charAt(i-1) == ' '))return generate(s,i+1,true,val);
        if(ch =='+' && val==0 && (i-1<0 || s.charAt(i-1) == ' '))return generate(s,i+1,false,val);
        if(ch>'9' || ch<'0')return val;
        int digit = ch-'0';
        
        if(isNeg){
            if((Integer.MIN_VALUE+digit)/10>val)return Integer.MIN_VALUE;
            val = val*10 - digit;
        }
        else {
            if((Integer.MAX_VALUE-digit)/10<val)return Integer.MAX_VALUE;
            val= val*10 + digit;
        }
        return generate(s,i+1,isNeg,val);
    }
    public int myAtoi(String s) {
       return generate(s,0,false,0);
    }
}
```

OR

```java
class Solution {
    boolean pos;
    boolean buildStarted;
    int ans;
    private int atoi(String s,int i){
        if(i==s.length())return ans;
        char ch = s.charAt(i);
        if(ch == ' ' && !buildStarted)return atoi(s,i+1);
        if(!buildStarted && (ch == '+' || ch == '-' || (ch>='0' && ch<='9'))){
            pos = (ch != '-');
            buildStarted=true;
            if(pos && ch != '+')return atoi(s,i);
            return atoi(s,i+1);
        }
        if(ch < '0' || ch > '9')return ans;
        int digit = ch - '0';
        if(pos){
            if(ans <= (Integer.MAX_VALUE - digit)/10){
                ans = ans*10 + digit;
            }
            else return Integer.MAX_VALUE;
        }
        else{
            if(ans >= (Integer.MIN_VALUE + digit)/10){
                ans = ans*10 - digit;
            }
            else return Integer.MIN_VALUE;
        }
        return atoi(s,i+1);
    }
    public int myAtoi(String s) {
        pos=true;
        buildStarted = false;
        ans=0;
        return atoi(s,0);
    }
}
```