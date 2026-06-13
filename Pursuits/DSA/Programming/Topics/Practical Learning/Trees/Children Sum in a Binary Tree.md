[Link](https://www.geeksforgeeks.org/problems/children-sum-parent/1)

Given a binary tree having **n** nodes. Check whether all of its nodes have a value equal to the sum of their child nodes. Return 1 if all the nodes in the tree satisfy the given properties, else it returns 0. For every node, the data value must be equal to the sum of the data values in the left and right children. Consider the data value 0 for a NULL child. Also, leaves are considered to follow the property.

**Examples:**

**Input:  
**Binary tree
       35
      /  \
     20   15
    / \   / \
   15  5 10  5

**Output:** 1
**Explanation:** Here, every node is sum of its left and right child.

**Input:  
**Binary tree
       1
     /   \
    4     3
   /  
  5    
**Output:** 0
**Explanation:** Here, 1 is the root node and 4, 3 are its child nodes. 4 + 3 = 7 which is not equal to the value of root node. Hence, this tree does not satisfy the given condition.

**Input:**  
Binary tree
       10
      /  \
     4    6
    / \  / \
   1   3 2  4
  
**Output:** 1  
**Explanation:**   
Here, every node is a sum of its left and right child.

**Constraints:**  
1 <= number of nodes <= 105  
0 <= node->data <= 105


# Using DFS

```java
class Solution
{
    //Function to check whether all nodes of a tree have the value 
    //equal to the sum of their child nodes.
    private static int dfs(Node node){
        if(node==null)return 0;
        if(node.left==null && node.right==null){
            return node.data;
        }
        int left = dfs(node.left);
        int right = dfs(node.right);
        if(left==-1 || right==-1)return -1;
        if(node.data==left+right)return node.data;
        return -1;
    }
    public static int isSumProperty(Node root)
    {
        // add your code here
        if(dfs(root)==-1)return 0;
        return 1;
    }
    
}
```

# Optimal

```java
public class Solution {
    public static boolean isParentSum(Node root) {
        // Write your code here.
        if(root==null)return true;
        if(root.left==null && root.right==null){
            return true;
        }
        
        if(!isParentSum(root.left) || !isParentSum(root.right))return false;
        int sum=0;
        if(root.left!=null)sum+=root.left.data;
        if(root.right!=null)sum+=root.right.data;
        if(sum==root.data)return true;
        return false;
    }
}
```