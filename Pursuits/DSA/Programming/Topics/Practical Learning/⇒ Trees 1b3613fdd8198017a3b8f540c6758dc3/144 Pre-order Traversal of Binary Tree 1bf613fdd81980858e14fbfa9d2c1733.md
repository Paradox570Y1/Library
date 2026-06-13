# 144. Pre-order Traversal of Binary Tree

<aside>
❓

Given the `root` of a binary tree, return *the preorder traversal of its nodes' values*.

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

</aside>

---

<aside>
💡

Iterative Approach With Stack:

```cpp
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) 
    {
        List<Integer> out = new ArrayList<>();
        if(root==null) return out;
        Stack<TreeNode> st = new Stack<>();
        st.push(root);

        while(!st.isEmpty()){
            int n = st.size();
            for(int i = 0; i<n; i++){
                TreeNode inner = st.pop();
                if(inner.right!=null){
                    st.push(inner.right);
                }
                if(inner.left!=null){
                    st.push(inner.left);
                }
                out.add(inner.val);
            }
        }

        return out;
    }
}
```

⇒ Recursive Code:

```cpp
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) 
    {
        List<Integer> out = new ArrayList<>();
        helper(root, out);  
        return out;  
    }

    public void helper(TreeNode trav, List<Integer> out){
        if(trav==null){
            return;
        }

        out.add(trav.val);
        helper(trav.left, out);
        helper(trav.right, out);

        return;
    }
}
```

</aside>