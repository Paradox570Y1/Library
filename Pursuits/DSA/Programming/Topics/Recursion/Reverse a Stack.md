[Link](https://www.geeksforgeeks.org/problems/reverse-a-stack/1)
### Reverse a Stack

Difficulty: **Medium**Accuracy: **80.5%**Submissions: **93K+**Points: **4**

You are given a stack **St**. You have to reverse the stack using recursion.

**Example 1:**

**Input:**
St = {3,2,1,7,6}
**Output:**
{6,7,1,2,3}  
**Explanation:**  
Input stack after reversing will look like the stack in the output.

**Example 2:**

**Input:**
St = {4,3,9,6}
**Output:**
{6,9,3,4}  
**Explanation:  
**Input stack after reversing will look like the stack in the output.

**Your Task:**

You don't need to read input or print anything. Your task is to complete the function **Reverse()** which takes the stack **St** as input and reverses the given stack.

**Expected Time Complexity:** O(N2)  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
1 <= size of the stack <= 104  
-109 <= Each element of the stack <= 109  
Sum of N over all test cases doesn't exceeds 106  
Array may contain duplicate elements.


```java
class Solution
{ 
    static void insert(Stack<Integer> s,int ele){
        if(s.isEmpty()){
            s.push(ele);
            return;
        }
        int temp = s.pop();
        insert(s,ele);
        s.push(temp);
        return;
    }
    static void reverse(Stack<Integer> s)
    {
        // add your code here
        if(s.isEmpty())return;
        int ele = s.pop();
        reverse(s);
        insert(s,ele);
    }
}
```