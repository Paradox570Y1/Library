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

# Optimal without extra space

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> preorder = new ArrayList<>();
        TreeNode cur = root;
        while(cur!=null){
            if(cur.left==null){
                preorder.add(cur.val);
                cur = cur.right;
            }
            else{
                TreeNode connect = cur.left;
                while(connect.right!=null && connect.right!=cur){
                    connect = connect.right;
                }
                if(connect.right==null){
                    connect.right = cur;
                    preorder.add(cur.val);
                    cur=cur.left;
                }
                else{
                    connect.right=null;
                    cur = cur.right;
                }
            }
        }
        return preorder;
    }
}
```