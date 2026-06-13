[Link](https://www.geeksforgeeks.org/problems/unique-binary-tree-requirements/1)

```txt
InOrder traversal is required in order to make a unique binary tree
along with either PreOrder or PostOrder.

You can make binary trees with only PreOrder and PostOrder but it will not be unique as multiple binary trees might be possible which satisfies both.
```


Geek wants to know the traversals required to construct a **unique binary tree**. Given a pair of traversal, return **true** if it is possible to construct unique binary tree from the given traversals otherwise return **false**.

Each traversal is represented with an integer: preorder - 1, inorder - 2, postorder - 3.   

**Example 1:**

**Input:**
a = 1, b=2
**Output:** 1
**Explanation:** We can construct binary tree using inorder traversal and preorder traversal. 

**Example 2:**

**Input:** a = 1, b=3
**Output:** 0 
**Explanation:** We cannot construct binary tree using preorder traversal and postorder traversal. 

**Constraints:**  
1 <= a,b <=3

**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **isPossible()** which takes **a** and **b** as input parameters and returns **true** or **false**.

**Expected Time Complexity:** O(1)  
**Expected Auxiliary Space:** O(1)


```java
class Solution{
    public static boolean isPossible(int a, int b){
        // Code here
        if(a==2 || b==2 )return !(a==b);
        return false;
    }
}
```
