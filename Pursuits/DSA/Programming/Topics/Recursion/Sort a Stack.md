[Link](https://www.geeksforgeeks.org/problems/sort-a-stack/1)
Difficulty: **Medium**Accuracy: **69.19%**Submissions: **133K+**Points: **4**

Given a stack, the task is to sort it such that the top of the stack has the greatest element.

**Example 1:**

**Input:**
Stack: 3 2 1
**Output:** 3 2 1

**Example 2:**

**Input:**
Stack: 11 2 32 3 41
**Output:** 41 32 11 3 2

**Your Task:**   
You don't have to read input or print anything. Your task is to complete the function **sort()** which sorts the elements present in the given stack. (The sorted stack is printed by the driver's code by popping the elements of the stack.)

**Expected Time Complexity**: O(N*N)  
**Expected Auxilliary Space**: O(N) recursive.

**Constraints:**  
1<=N<=100

# Optimal
```java
class GfG {
    public Stack<Integer> insert(Stack<Integer> s,int ele){
        if(s.size()==0 || s.peek()<ele){
            s.push(ele);
        }
        else{
            int temp = s.pop();
            s = insert(s,ele);
            s.push(temp);
        }
        return s;
    }
    public Stack<Integer> sort(Stack<Integer> s) {
        // add code here.
        if(s.isEmpty())return s;
        int ele = s.pop();
        s= sort(s);
        s=insert(s,ele);
        return s;
    }
}
```

OR

```java
/*Complete the function below*/
class GfG {
    private void putEle(Stack<Integer> s, int ele){
        if(s.isEmpty() || s.peek()<ele){
            s.push(ele);
            return;
        }
        int k = s.pop();
        putEle(s,ele);
        s.push(k);
    }
    public Stack<Integer> sort(Stack<Integer> s) {
        // add code here.
        if(s.isEmpty())return s;
        int ele = s.pop();
        sort(s);
        putEle(s,ele);
        return s;
    }
}
```