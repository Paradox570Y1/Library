# 104. Maximum Depth Of A Binary Tree

<aside>
❓

Given the `root` of a binary tree, return *its maximum depth*.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: 3

```

**Example 2:**

```
Input: root = [1,null,2]
Output: 2

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `100 <= Node.val <= 100`
</aside>

---

<aside>
💡

⇒ Self-Approach:

```cpp
class Solution {
    public int maxDepth(TreeNode root) {
        if(root==null) return 0;
        
        int height = helper(root, 1);
        return height;
    }

    public int helper(TreeNode trav, int height){
        if(trav.left==null && trav.right==null){
            return height;
        }

        int left = 0;
        int right = 0;

        if(trav.left!=null) left = helper(trav.left, height+1);
        if(trav.right!=null) right = helper(trav.right, height+1);

        return(left>=right)?left:right;
    }
}
```

</aside>