[145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)
Given the `root` of a binary tree, return _the postorder traversal of its nodes' values_.

**Example 1:**

**Input:** root = [1,null,2,3]

**Output:** [3,2,1]

**Explanation:**

![](https://assets.leetcode.com/uploads/2024/08/29/screenshot-2024-08-29-202743.png)

**Example 2:**

**Input:** root = [1,2,3,4,5,null,8,null,null,6,7,9]

**Output:** [4,6,7,5,2,9,8,3,1]

**Explanation:**

![](https://assets.leetcode.com/uploads/2024/08/29/tree_2.png)

**Example 3:**

**Input:** root = []

**Output:** []

**Example 4:**

**Input:** root = [1]

**Output:** [1]

**Constraints:**

- The number of the nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`


# Using recursion

```java
class Solution {
    private List<Integer> postOrder(TreeNode node,List<Integer> li){
        if(node == null)return li;
        postOrder(node.left,li);
        postOrder(node.right,li);
        li.add(node.val);
        return li;
    }
    public List<Integer> postorderTraversal(TreeNode root) {
        return postOrder(root,new ArrayList<>());
    }
}
```


# Using Iterative approach

Using 2 stacks
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if(root==null)return ans;
        Stack<TreeNode> st1 = new Stack<>();
        Stack<TreeNode> st2 = new Stack<>();
        st1.push(root);
        while(!st1.isEmpty()){
            TreeNode node = st1.pop();
            st2.push(node);
            if(node.left!=null){
                st1.push(node.left);
            }
            if(node.right!=null){
                st1.push(node.right);
            }
        }
        while(!st2.isEmpty()){
            ans.add(st2.pop().val);
        }
        return ans;
    }
}
```


Using 1 stack

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> postOrder = new ArrayList<>();
        if(root == null)return postOrder;
        Stack<TreeNode> st = new Stack<>();
        TreeNode cur = root;
        while(cur!=null || !st.isEmpty()){
            if(cur!=null){
                st.push(cur);
                cur = cur.left;
            }
            else{
                TreeNode temp = st.peek().right;
                if(temp==null){
                    temp = st.pop();
                    postOrder.add(temp.val);
                    while(!st.isEmpty() && temp == st.peek().right){
                        temp = st.pop();
                        postOrder.add(temp.val);
                    }
                }
                else cur = temp;
            }
        }
        return postOrder;
    }
}
```