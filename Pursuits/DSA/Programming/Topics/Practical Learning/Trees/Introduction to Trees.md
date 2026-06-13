[Link](https://www.geeksforgeeks.org/problems/introduction-to-trees/1)
Difficulty: **Easy**Accuracy: **82.66%**Submissions: **48K+**Points: **2**Average Time: **15m**

Given an integer **i**. Print the **maximum number of nodes** on level i of a binary tree.

**Example 1:**

**Input:** 5
**Output:** 16

**Example 2:**

**Input:** 1
**Output:** 1

**Your Task:**

Complete the function **countNode()** which takes an integer i as input and prints the count of maximum number of nodes at that level.

**Expected Time Complexity:** O(1)

**Expected Space Complexity:** O(1)

**Constraints:**

1<=i<=20

# Better 
TC-> O(logN)
SC-> O(1)
```java
class Solution {
    static int countNodes(int i) {
        // code here
        int h = i-1;
        int ans=1;
        int num = 2;
        while(h>0){
            if(h%2==1){
                ans*= num;
                h--;
            }
            else{
                num*=num;
                h/=2;
            }
        }
        return ans;
    }
}
```


# Optimal
Using Bitwise
```java
class Solution {
    static int countNodes(int i) {
        // code here
        return 1<<(i-1);
    }
}
```