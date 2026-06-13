[402. Remove K Digits](https://leetcode.com/problems/remove-k-digits/)

Given string num representing a non-negative integer `num`, and an integer `k`, return _the smallest possible integer after removing_ `k` _digits from_ `num`.

**Example 1:**

**Input:** num = "1432219", k = 3
**Output:** "1219"
**Explanation:** Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.

**Example 2:**

**Input:** num = "10200", k = 1
**Output:** "200"
**Explanation:** Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.

**Example 3:**

**Input:** num = "10", k = 2
**Output:** "0"
**Explanation:** Remove all the digits from the number and it is left with nothing which is 0.

**Constraints:**

- `1 <= k <= num.length <= 105`
- `num` consists of only digits.
- `num` does not have any leading zeros except for the zero itself.

# Brute

```java
class Solution {
    public String removeKdigits(String num, int k) {
        if(k>num.length())return "0";
        while(k-->0){
            int i=0;
            int n = num.length();
            while(i<n-1){
                if(num.charAt(i+1)<num.charAt(i))break;
                i++;
            }
            num = num.substring(0,i) + num.substring(i+1);
        }
        int i=0;
        for(char ch:num.toCharArray()){
            if(ch=='0')i++;
            else break;
        }
        String ans = num.substring(i);
        if(ans.length()==0)return "0";
        return ans;
    }
}
```
# Using Stack
TC => O(2N)
SC => O(N) + {O(N) (to return the answer)}
```java
class Solution {
    public String removeKdigits(String num, int k) {
        if(num.length()==k)return "0";
        Stack<Character> st = new Stack<>();
        int n = num.length();
        for(int i=0;i<n;i++){
            while(!st.isEmpty() && st.peek()>num.charAt(i) && k>0){
                st.pop();k--;
            }
            if(st.isEmpty() && num.charAt(i)=='0')continue;
            st.push(num.charAt(i));
        }
        if(st.isEmpty())return "0";
        StringBuilder sb = new StringBuilder();
        int sz = st.size();
        for(int i=0;i<sz;i++){
            char ele = st.pop();
            if(k>0){k--;continue;}
            sb.append(ele);
        }
        if(sb.length()==0)return "0";
        return sb.reverse().toString();
    }
}
```