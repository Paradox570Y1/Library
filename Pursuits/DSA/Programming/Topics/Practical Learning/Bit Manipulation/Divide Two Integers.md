[29. Divide Two Integers](https://leetcode.com/problems/divide-two-integers/)

Given two integers `dividend` and `divisor`, divide two integers **without** using multiplication, division, and mod operator.

The integer division should truncate toward zero, which means losing its fractional part. For example, `8.345` would be truncated to `8`, and `-2.7335` would be truncated to `-2`.

Return _the **quotient** after dividing_ `dividend` _by_ `divisor`.

**Note:** Assume we are dealing with an environment that could only store integers within the **32-bit** signed integer range: `[−231, 231 − 1]`. For this problem, if the quotient is **strictly greater than** `231 - 1`, then return `231 - 1`, and if the quotient is **strictly less than** `-231`, then return `-231`.

**Example 1:**

**Input:** dividend = 10, divisor = 3
**Output:** 3
**Explanation:** 10/3 = 3.33333.. which is truncated to 3.

**Example 2:**

**Input:** dividend = 7, divisor = -3
**Output:** -2
**Explanation:** 7/-3 = -2.33333.. which is truncated to -2.

**Constraints:**

- `-231 <= dividend, divisor <= 231 - 1`
- `divisor != 0`

# Optimal
TC -> O(logn)²
SC->O(1)
```java
class Solution {
    
    public int divide(int dividend, int divisor) {
        if(dividend==divisor)return 1;
        boolean sign = false;
        if(dividend<0 && divisor>0)sign =true;
        if(dividend>0 && divisor<0)sign=true;
        long n = Math.abs((long)dividend);
        long d = Math.abs((long)divisor);
        int quotient=0;
        while(n>=d){
            int cnt=0;
            while(n>=(d<<(cnt+1)))cnt++;
            quotient+=(1<<cnt);
            n-=(d<<cnt);
        }
        if(quotient == (1<<31)){
            if(sign)return Integer.MIN_VALUE;
            else return Integer.MAX_VALUE;
        }
        return sign?-quotient:quotient;
    }
}
```

