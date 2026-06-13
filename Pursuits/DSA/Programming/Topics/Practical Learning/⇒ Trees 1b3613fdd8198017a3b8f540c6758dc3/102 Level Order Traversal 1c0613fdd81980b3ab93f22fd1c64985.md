# 102. Level Order Traversal

<aside>
❓

Given the `root` of a binary tree, return *the level order traversal of its nodes' values*. (i.e., from left to right, level by level).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]

```

**Example 2:**

```
Input: root = [1]
Output: [[1]]

```

**Example 3:**

```
Input: root = []
Output: []

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `1000 <= Node.val <= 1000`
</aside>

---

<aside>
💡

⇒ Recursive Approach:

```cpp
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> out = new ArrayList<>();
        helper(out, 0, root);
        return out;
    }

    public void helper(List<List<Integer>> out, int level, TreeNode trav){
        if(trav==null){
            return;
        }

        if(out.size()<level+1) out.add(new ArrayList<>());
        out.get(level).add(trav.val);
        
        helper(out, level+1, trav.left);
        helper(out, level+1, trav.right);
    }
}
```

⇒ Iterative Approach Using Queue:

```cpp
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        var out = new ArrayList<List<Integer>>();
        if(root==null) return out;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        
        while(!q.isEmpty()){
            List<Integer> inner = new ArrayList<>();
            int n = q.size();
            for(int i = 0; i<n; i++){
                if(q.peek().left!=null){
                    q.add(q.peek().left);
                }
                if(q.peek().right!=null){
                    q.add(q.peek().right);
                }
                
                inner.add(q.remove().val);
            }
            
            out.add(inner);
        }

        return out;
    }
}
```

</aside>