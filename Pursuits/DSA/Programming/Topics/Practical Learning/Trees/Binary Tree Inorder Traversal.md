[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

Given the `root` of a binary tree, return _the inorder traversal of its nodes' values_.

**Example 1:**

**Input:** root = [1,null,2,3]

**Output:** [1,3,2]

**Explanation:**

![](https://assets.leetcode.com/uploads/2024/08/29/screenshot-2024-08-29-202743.png)

**Example 2:**

**Input:** root = [1,2,3,4,5,null,8,null,null,6,7,9]

**Output:** [4,2,6,5,7,1,3,9,8]

**Explanation:**

![](https://assets.leetcode.com/uploads/2024/08/29/tree_2.png)

**Example 3:**

**Input:** root = []

**Output:** []

**Example 4:**

**Input:** root = [1]

**Output:** [1]

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`


# Using Recursion

```java
class Solution {
    private List<Integer> inOrder(TreeNode node,List<Integer> li){
        if(node==null)return li;
        inOrder(node.left,li);
        li.add(node.val);
        inOrder(node.right,li);
        return li;
    }
    public List<Integer> inorderTraversal(TreeNode root) {
        return inOrder(root,new ArrayList<>());
    }
}
```


# Iterative Approach

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> inOrder = new ArrayList<>();
        if(root==null)return inOrder;
        Stack<TreeNode> st = new Stack<>();
        TreeNode node = root;
        while(true){
            if(node!=null){
                st.push(node);
                node = node.left;
            }
            else{
                if(st.isEmpty()){
                    break;
                }
                node = st.pop();
                inOrder.add(node.val);
                node = node.right;
            }
        }
        return inOrder;
    }
}
```

