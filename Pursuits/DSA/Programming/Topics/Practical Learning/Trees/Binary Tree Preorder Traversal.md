[144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

Given the `root` of a binary tree, return _the preorder traversal of its nodes' values_.

**Example 1:**

**Input:** root = [1,null,2,3]

**Output:** [1,2,3]

**Explanation:**

![](https://assets.leetcode.com/uploads/2024/08/29/screenshot-2024-08-29-202743.png)

**Example 2:**

**Input:** root = [1,2,3,4,5,null,8,null,null,6,7,9]

**Output:** [1,2,4,5,6,7,3,8,9]

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
    private List<Integer> preOrder(TreeNode root,List<Integer> li){
        if(root == null)return li;
        li.add(root.val);
        preOrder(root.left,li);
        preOrder(root.right,li);
        return li;
    }
    public List<Integer> preorderTraversal(TreeNode root) {
        return preOrder(root,new ArrayList<>());
    }
}
```


# Iterative approach

TC-> O(N)
SC-> O(Height of the binary tree)

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> st = new Stack<>();
        List<Integer> preOrder = new ArrayList<>();
        if(root==null)return preOrder;
        st.add(root);
        while(!st.isEmpty()){
            root = st.pop();
            preOrder.add(root.val);
            if(root.right!=null){
                st.add(root.right);
            }
            if(root.left!=null){
                st.add(root.left);
            }
        }
        return preOrder;
    }
}
```

![[Pasted image 20250325152244.png]]