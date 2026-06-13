[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** [[3],[9,20],[15,7]]

**Example 2:**

**Input:** root = [1]
**Output:** [[1]]

**Example 3:**

**Input:** root = []
**Output:** []

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-1000 <= Node.val <= 1000`



# Using Iterative Approach

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans  = new ArrayList<>();
        if(root == null)return ans;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while(!q.isEmpty()){
            int nodeCnt = q.size();
            List<Integer> temp = new ArrayList<>();
            for(int i=0;i<nodeCnt;i++){
                TreeNode cur = q.poll();
                if(cur.left!=null)q.offer(cur.left);
                if(cur.right!=null)q.offer(cur.right);
                temp.add(cur.val);
            }
            ans.add(temp);
        }
        return ans;
    }
}
```

# Using recursive Approach (Optimal)
Implementing BFS with DFS 
```java
class Solution {
    private void helper(TreeNode node,int level,List<List<Integer>> ans){
        if(node==null)return;
        if(level == ans.size()){
            ans.add(new ArrayList<>());
        }
        List<Integer> list = ans.get(level);
        list.add(node.val);
        helper(node.left,level+1,ans);
        helper(node.right,level+1,ans);
    }
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        helper(root,0,ans);
        return ans;
    }
}
```