[link](https://www.geeksforgeeks.org/problems/prime-factorization-using-sieve/1)
### Prime Factorization using Sieve

Difficulty: **Medium**Accuracy: **47.01%**Submissions: **23K+**Points: **4**

You are given a positive number N. Using the concept of Sieve, compute its prime factorisation.

**Example:**

**Input:** 
N = 12246
**Output:** 
2 3 13 157
**Explanation:** 
2*3*13*157 = 12246 = N.

**Your Task:**

Comple the function **findPrimeFactors**(), which takes a positive number N as input and returns a vector consisting of prime factors. You should implement Sieve algorithm to solve this problem.

**Expected Time Complexity:** O(Nlog(log(N)).

**Expected Auxiliary Space:** O(N).

**Constraints:**

2<=N<=2*105


# Optimal
TC-> O(√n \* log n)

```java
class Solution {
    static List<Integer> findPrimeFactors(int N) {
        // code here
        List<Integer> ans = new ArrayList<>();
        int i=2;
        while(i<=N){
            while(N%i==0){
                ans.add(i);
                N/=i;
            }
            i++;
        }
        return ans;
    }
}
```




# What if question gives you multiple queries then the optimal will be following( using sieve)
- This is because for multiple queries sieve can be reused.
- We are going to use `SPF (Smallest Prime Factor)`
-  Sieve obj will be created only once then `spf` array will be used for all the queries processed in `findPrimeFactors()`.
```java
class Solution {
    // You must implement this function
    static int N = 200000;
    static int[] spf = new int[N+1];
    //takes N log (log N)
    static void sieve() {
        for(int i=0;i<N+1;i++){
            spf[i] = i;
        }
        for(int i=2;i*i<N;i++){
            if(spf[i]==i){
                for(int j=i*2;j<=N;j+=i){
                    if(spf[j]==j)spf[j] = i;
                }
            }
        }
    }

    static List<Integer> findPrimeFactors(int N) {
        // code here
        List<Integer> ans = new ArrayList<>();
        //takes log N
        while(N!=1){
            ans.add(spf[N]);
            N/=spf[N];
        }
        return ans;
    }
}
```