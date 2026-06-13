[Link](https://www.interviewbit.com/problems/path-to-given-node/)

**Problem Description**  

Given a Binary Tree **A** containing **N** nodes.

You need to find the path from **Root** to a given node **B**.

**NOTE:**

- No two nodes in the tree have same data values.
- You can assume that **B** is present in the tree **A** and a path always exists.

**Problem Constraints**  

1 <= N <= 105
1 <= Data Values of Each Node <= N
1 <= B <= N

**Input Format**  
First Argument represents pointer to the root of binary tree **A**.
Second Argument is an integer **B** denoting the node number.

  
**Output Format**  
Return an one-dimensional array denoting the path from **Root** to the node **B** in order.

**Example Input**  

Input 1:

 A =  
           1
         /   \
        2     3
       / \   / \
      4   5 6   7 

B = 5

Input 2:

 A = 
            1
          /   \
         2     3
        / \ .   \
       4   5 .   6

B = 1

**Example Output**  
Output 1:
 [1, 2, 5]
Output 2:
 [1]


```java
public class Solution {
    public int[] solve(TreeNode A, int B) {
        List<Integer> list = new ArrayList<>();
        helper(A,B,list);
        int[] ans = new int[list.size()];
        for(int i=0;i<list.size();i++){
            ans[i] = list.get(i);
        }
        return ans;
    }
    private boolean helper(TreeNode A,int B,List<Integer> list){
        if(A==null)return false;
        list.add(A.val);
        if(A.val==B)return true;
        if(helper(A.left,B,list) || helper(A.right,B,list))return true;
        list.remove(list.size()-1);
        return false;
    }
}
```