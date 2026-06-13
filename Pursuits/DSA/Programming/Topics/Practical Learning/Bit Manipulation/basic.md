[Link](https://www.geeksforgeeks.org/problems/bit-manipulation-1666686020/1)
### Bit Manipulation

Difficulty: **Easy**Accuracy: **49.84%**Submissions: **52K+**Points: **2**

Given a 32 bit unsigned integer **num** and an integer **i**. Perform following operations on the number - 

1. **Get** ith bit

2. **Set** ith bit

3. **Clear** ith bit

**Note :** For better understanding, we are starting bits from 1 instead 0. (1-based). You have to print space three space seperated values ( as shown in output without a line break) and do not have to return anything.

**Examples :**

**Input:** 70 3
**Output:** 1 70 66
**Explanation:** Bit at the 3rd position from LSB is 1. (1 0 0 0 **1** 1 0) .The value of the given number after setting the 3rd bit is 70. The value of the given number after clearing 3rd bit is 66. (1 0 0 0 **0** 1 0)

**Input:** 8 1
**Output:** 0 9 8
**Explanation:** Bit at the first position from LSB is 0. (1 0 0 **0**)  .The value of the given number after setting the 1st bit is 9. (1 0 0 **1**).  The value of the given number after clearing 1st bit is 8. (1 0 0 **0**)

**Constraints:**

0<=num<=109

1<=i<=32


# Brute

```java
class Solution {
    static void bitManipulation(int num, int i) {
        // code here
        int helper = 1<<i-1;
        if((num & helper) >0)System.out.print(1+" ");
        else System.out.print(0+" ");
        System.out.print((num|helper)+" ");
        System.out.print(num&~helper);
    }
}
```

```java
class Solution {
    static void bitManipulation(int num, int i) {
        // code here
        int helper = 1<<i-1;
        int check = num & helper;
        if(check >0)System.out.print(1+" ");
        else {
            System.out.print(0+" ");
            num^=helper;
        }
        System.out.print(num+" ");
        num^=helper;
        System.out.print(num);
    }
}
```