[Link](https://geeksforgeeks.org/problems/check-whether-k-th-bit-is-set-or-not-1587115620/1)
### K-th Bit is Set or Not

Difficulty: **Easy**Accuracy: **52.75%**Submissions: **214K+**Points: **2**

Given a number **n** and a bit number **k**, check if the **kth** index bit of **n** is set or not. A bit is called set if it is 1. The position of set bit '1' should be indexed starting with 0 from the LSB side in the binary representation of the number.  
Note: Index is starting from 0. You just need to return **true** or **false.**

**Examples :** 

**Input**: n = 4, k = 0
**Output**: false
**Explanation**: Binary representation of 4 is 100, in which 0th index bit from LSB is not set. So, return false.

**Input**: n = 4, k = 2
**Output**: true
**Explanation**: Binary representation of 4 is 100, in which 2nd index bit from LSB is set. So, return true.

**Input**: n = 500, k = 3  
**Output**: false  
**Explanation**: Binary representation of 500 is 111110100, in which 3rd index bit from LSB is not set. So, return false.

**Constraints:**  
1 ≤ n ≤ 109  
0 ≤ k ≤ 31

# Using left shift

```java
class CheckBit {
    // Function to check if Kth bit is set or not.
    static boolean checkKthBit(int n, int k) {
        // Your code here
        int helper = 1<<k;
        if((helper&n)==0)return false;
        return true;
    }
}
```

# Using right shift

```java
class CheckBit {
    // Function to check if Kth bit is set or not.
    static boolean checkKthBit(int n, int k) {
        // Your code here
        if(((n>>k)& 1)==1)return true;
        return false;
    }
}
```