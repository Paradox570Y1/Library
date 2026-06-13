[link](https://www.geeksforgeeks.org/problems/all-divisors-of-a-number/1?amp%3Butm_medium=collab_striver_ytdescription&amp%3Butm_campaign=all-divisors-of-a-number)

Difficulty: **Easy**Accuracy: **46.73%**Submissions: **43K+**Points: **2**

Given an integer **N,** print all the divisors of N in the **ascending** order.  
 

**Example 1:**

**Input :** 20
**Output:** 1 2 4 5 10 20
**Explanation:** 20 is completely 
divisible by 1, 2, 4, 5, 10 and 20.

**Example 2:**

**Input:** 21191
**Output:** 1 21191
**Explanation**: As 21191 is a prime number,
it has only 2 factors(1 and the number itself).

**Your Task:**

Your task is to complete the function **print_divisors()** which takes N as input parameter and prints all the factors of N as space seperated integers in sorted order. You don't have to print any new line after printing the desired output. It will be handled in driver code.  
 

**Expected Time Complexity:** O(sqrt(N))  
**Expected Space Complexity:** O(sqrt(N))  
 

**Constraints:**  
1 <= N <= 105
# Brute
TC-> O(N)
```java
class Solution {
    public static void print_divisors(int n) {
        // code here
        for(int i=1;i<=n;i++){
            if(n%i==0){
                System.out.print(i);
                if(n!=i)System.out.print(" ");
            }
            
        }
    }
}
```

# Better
TC -> O(√n)
SC-> O(√n)
```java
class Solution {
    public static void print_divisors(int n) {
        // code here
        List<Integer> li = new ArrayList<>();
        for(int i=1;i*i<=n;i++){
            if(n%i==0){
                System.out.print(i);
                if(n!=i)System.out.print(" ");
                if(n/i != i)li.add(n/i);
            }
        }
        if(li.size()==0)return;
        for(int i = li.size()-1;i>=0;i--){
            System.out.print(li.get(i));
            if(i!=0)System.out.print(" ");
        }
        return;
    }
}
```