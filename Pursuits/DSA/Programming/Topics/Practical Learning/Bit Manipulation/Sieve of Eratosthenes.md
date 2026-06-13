[204. Count Primes](https://leetcode.com/problems/count-primes/)

Given an integer `n`, return _the number of prime numbers that are strictly less than_ `n`.

**Example 1:**

**Input:** n = 10
**Output:** 4
**Explanation:** There are 4 prime numbers less than 10, they are 2, 3, 5, 7.

**Example 2:**

**Input:** n = 0
**Output:** 0

**Example 3:**

**Input:** n = 1
**Output:** 0

**Constraints:**

- `0 <= n <= 5 * 106`
# Brute
TC(O(N\*√N))
```java
class Solution {
    boolean isPrime(int n){
        for(int i=2;i*i<=n;i++){
            if(n%i==0)return false;
        }
        return true;
    }
    public int countPrimes(int n) {
        int cnt=0;
        for(int i=2; i<n;i++){
            if(isPrime(i))cnt++;
        }
        return cnt;
    }
}
```


# Better
TC-> O(n\* log (log n)) + O(n)

```java
class Solution {

    public int countPrimes(int n) {
        int cnt=0;
        boolean[] isMarked = new boolean[n];
        //pre computation
        for(int i=2;i<n;i++){
            if(!isMarked[i]){
                for(int j=i*2;j<n;j+=i){
                    isMarked[j] = true;
                }
            }
        }
        for(int i=2;i<n;i++){
            if(isMarked[i]){
                continue;
            }
            cnt++;

        }
        return cnt;
    }
}
```

# Optimal

```java
class Solution {

    public int countPrimes(int n) {
        int cnt=0;
        boolean[] isMarked = new boolean[n];
        //pre computation
        for(int i=2;i*i<n;i++){
            if(!isMarked[i]){
                for(int j=i*i;j<n;j+=i){
                    isMarked[j] = true;
                }
            }
        }
        for(int i=2;i<n;i++){
            if(isMarked[i]){
                continue;
            }
            cnt++;

        }
        return cnt;
    }
}
```

