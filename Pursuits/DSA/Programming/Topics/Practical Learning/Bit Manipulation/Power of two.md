[231. Power of Two](https://leetcode.com/problems/power-of-two/)

Given an integer `n`, return _`true` if it is a power of two. Otherwise, return `false`_.

An integer `n` is a power of two, if there exists an integer `x` such that `n == 2x`.

**Example 1:**

**Input:** n = 1
**Output:** true
**Explanation:** 20 = 1

**Example 2:**

**Input:** n = 16
**Output:** true
**Explanation:** 24 = 16

**Example 3:**

**Input:** n = 3
**Output:** false

**Constraints:**

- `-231 <= n <= 231 - 1`

Using Bit manipulation
```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n==0 || n == Integer.MIN_VALUE)return false;
        return (n & n-1) == 0;
    }
}
```

here loop run for constant time of 31 iterations.

```java
bool isPowerOfTwo(int n) {
    int k =1;
    for(int i=0;i<=30;i++) {
        if(n==k) {
            return true;
        }
        if(k < INT_MAX/2)
            k *= 2;
    }
    return false;
}
```


# Using while loop

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        int cnt = 0;
        while (n > 0) {
            cnt += (n & 1);
            n = n >> 1;
        }
        return cnt == 1;
    }
}
```
# Using 2s Complement
- In this all numbers are completely reversible.
- All basic arithmetic operator works.

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n==0 || n == Integer.MIN_VALUE)return false;
        return (n & -n) == n;
    }
}
```


![[Pasted image 20250905210236.png|300]]