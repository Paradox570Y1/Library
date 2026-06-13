[Link](https://www.geeksforgeeks.org/problems/set-the-rightmost-unset-bit4436/1)
### Set the rightmost unset bit

Difficulty: **Basic**Accuracy: **47.64%**Submissions: **50K+**Points: **1**

Given a non-negative number **n** . The problem is to set the rightmost unset bit in the binary representation of **n**.

**Examples :**

**Input:** n = 6
**Output:** 7
**Explanation:** The binary representation of 6 is 110. After setting right most bit it becomes 111 which is 7.

**Input:** n = 15
**Output:** 31
**Explanation:** The binary representation of 15 is 01111. After setting right most bit it becomes 11111 which is 31.

**Expected Time Complexity:** O(Logn)  
**Expected Auxiliary Space:** O(1)

  
**Constraints:**  
1 <= n <= 109

```java
class Solution {
    static int setBit(int n) {
        // code here
        int cpy = n;
        int bit=0;
        while(cpy!=0){
            if((cpy&1)==0){
                break;
            }
            cpy>>=1;
            bit++;
        }
        return n|(1<<bit);
    }
}
```