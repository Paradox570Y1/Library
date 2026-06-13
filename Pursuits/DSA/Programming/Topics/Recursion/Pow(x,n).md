[50. Pow(x, n)](https://leetcode.com/problems/powx-n/)
Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., `xn`).

**Example 1:**

**Input:** x = 2.00000, n = 10
**Output:** 1024.00000

**Example 2:**

**Input:** x = 2.10000, n = 3
**Output:** 9.26100

**Example 3:**

**Input:** x = 2.00000, n = -2
**Output:** 0.25000
**Explanation:** 2-2 = 1/22 = 1/4 = 0.25

**Constraints:**

- `-100.0 < x < 100.0`
- `-231 <= n <= 231-1`
- `n` is an integer.
- Either `x` is not zero or `n > 0`.
- `-104 <= xn <= 104`


# Brute

```java
class Solution {
public:
    double myPow(double x, int n) {
        double ans=1;
        for(int i=0;i<abs(n);i++){
            if(n>=0)ans *=x;
            if(n<0)ans /=x;
        }
        return ans;
    }
};
```

OR

```java
class Solution {
    public double myPow(double x, int n) {
        if()
        double ans = 1.0;
        int c = n;
        while(c!=0){
            ans*= x;
            if(c<0)c++;
            else c--;
        }
        if(n<0)return 1/ans;
        return ans;
    }
}
```
# Better

```java
class Solution {
public:
    double myPow(double x, int n) {
        double ans=1;
        int i = n;
        //if n is positive
        while(i>0){
            if(i%2==0){
                x*=x;
                i/=2;
            }
            else {
                ans*=x;
                i--;
            }
        }
        //if n is negative
        while(i<0){
            if(i%2==0){
                x*=x;
                i/=2;
            }
            else {
                ans/=x;
                i++;
            }
        }
        return ans;
    }
};
```


# Optimal

```java
class Solution {

    public double myPow(double x, int n) {
        double ans=1;
        double i = n;
        if(i<0){
            x = 1/x;
            i = -i;
        }
        while(i>0){
            if(i%2==0){
                x*=x;
                i/=2;
            }
            else{
                ans*=x;
                i--;
            }
        }
        return ans;
    }
}
```

OR
```java
class Solution {

    public double myPow(double x, int n) {
        double ans=1;
        double i = n;
        if(i<0)i=-i;
        while(i>0){
            if(i%2==0){
                x*=x;
                i/=2;
            }
            else{
                ans*=x;
                i--;
            }
        }
        if(n<0)return 1/ans;
        return ans;
    }
}
```

Using Recursion
```java
class Solution {
    public double findPow(double x,double n){

        if(n==0)return 1.0;
        if(n%2==0){
            return findPow(x*x,n/2);
        }
        else{
            return x * findPow(x,n-1);
        }
    }
    public double myPow(double x, int n) {
        double N = n;
        if(N<0)N=-N;
        double ans = findPow(x,N);
        if(n<0)return 1/ans;
        return ans;
    }
}
```