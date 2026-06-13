[1922. Count Good Numbers](https://leetcode.com/problems/count-good-numbers/)

A digit string is **good** if the digits **(0-indexed)** at **even** indices are **even** and the digits at **odd** indices are **prime** (`2`, `3`, `5`, or `7`).

- For example, `"2582"` is good because the digits (`2` and `8`) at even positions are even and the digits (`5` and `2`) at odd positions are prime. However, `"3245"` is **not** good because `3` is at an even index but is not even.

Given an integer `n`, return _the **total** number of good digit strings of length_ `n`. Since the answer may be large, **return it modulo** `109 + 7`.

A **digit string** is a string consisting of digits `0` through `9` that may contain leading zeros.

**Example 1:**

**Input:** n = 1
**Output:** 5
**Explanation:** The good numbers of length 1 are "0", "2", "4", "6", "8".

**Example 2:**

**Input:** n = 4
**Output:** 400

**Example 3:**

**Input:** n = 50
**Output:** 564908303

**Constraints:**

- `1 <= n <= 1015`



# Brute

```java
class Solution {
    public int countGoodNumbers(long n) {
        long mod = 1_000_000_007;
        long odd = 0,even=0;
        if(n%2==0){
            odd = n/2;
            even = odd;
        }
        else{
            odd = n/2;
            even = odd+1;
        }
        long ans=1;
        for(int i=0;i<odd;i++){
            ans= (ans*4)%mod;
        }
        for(int i=0;i<even;i++){
            ans= (ans*5)%mod;
        }
        return (int)ans;
    }
}
```

OR
Will result in stack overflow as "`1_000_000_000` would require a billion recursive calls, which is impractical."
```java
class Solution {
    long ans;
    private long helper(long i){
        if(i<0)return ans;
        ans= (ans * ((i%2==0)?5:4))% 1_000_000_007;
        return helper(i-1);
    }
    public int countGoodNumbers(long n) {
        ans=1;
        return (int)helper(n-1);
    }
}
```

OR

```java
class Solution {
    public int countGoodNumbers(long n) {
        long ans = 1;
        long i = n-1;
        while (i >= 0) {
            ans = (ans * ((i % 2 == 0) ? 5 : 4)) % 1_000_000_007;
            i--;
        }
        return (int)ans;
    }
}
```
# Optimal

Using Recursion
```java
class Solution {
    public long countNum(long cnt,long mul){
        long mod = 1_000_000_007;
        if(cnt==0)return 1;
        if(cnt%2==0)return countNum(cnt/2,(mul*mul)%mod);
        else return (mul*countNum(cnt-1,mul))%mod;
    }
    public int countGoodNumbers(long n) {
        long mod = 1_000_000_007;
        long odd = 0,even=0;
        if(n%2==0){
            odd = n/2;
            even = odd;
        }
        else{
            odd = n/2;
            even = odd+1;
        }
        long ans=1;
        ans=countNum(even,5);
        ans=(ans*countNum(odd,4))%mod;
        return (int)ans;
    }
}
```


```java
class Solution {
    public int countGoodNumbers(long n) {
        long mod = 1_000_000_007;
        long odd = 0,even=0;
        if(n%2==0){
            odd = n/2;
            even = odd;
        }
        else{
            odd = n/2;
            even = odd+1;
        }
        long ans=1;
        long mul = 4;
        while(odd>0){
            if(odd%2==0){
                mul=(mul*mul)%mod;
                odd/=2;
            }
            else{
                ans = (ans*mul)%mod;
                odd--;
            }
        }
        mul = 5;
        while(even>0){
            if(even%2==0){
                mul=(mul*mul)%mod;
                even/=2;
            }
            else{
                ans = (ans*mul)%mod;
                even--;
            }
        }
        return (int)ans;
    }
}
```

OR

```java
class Solution {
    private long mul(long cnt,int ele){
        long ans = 1;
        long base = ele;
        while(cnt>0){
            if(cnt%2==0){
                base= (base*base)%1_000_000_007;
                cnt/=2;
            }
            else{
                ans= (ans*base)%1_000_000_007;
                cnt--;
            }
        }
        return ans;
    }
    public int countGoodNumbers(long n) {
        long odd = n/2;
        long even = n-odd;
        return (int)((mul(even,5) * mul(odd,4))%1_000_000_007);
    }
}
```