[Coding Ninjas](https://www.naukri.com/code360/problems/boundary-traversal_790725)

## Problem statement

You are given a binary tree having _**'n'**_ nodes.

The boundary nodes of a binary tree include the nodes from the left and right boundaries and the leaf nodes, each node considered once.

Figure out the boundary nodes of this binary tree in an Anti-Clockwise direction starting from the root node.
**Example :**

```
Input: Consider the binary tree A as shown in the figure:
```

![alt text](https://files.codingninjas.in/boundarytraversal-5149.png)

```
Output: [10, 5, 3, 7, 18, 25, 20]
```


# Striver Code

```java
public class Solution {
    boolean isLeaf(Node root) {
        return root.left == null && root.right == null;
    }
    void addLeftBoundary(Node root, List<Integer> res) {
        Node curr = root.left;
        while (curr != null) {
            if (!isLeaf(curr)) {
                res.add(curr.data);
            }
            if (curr.left != null) {
                curr = curr.left;
            } else {
                curr = curr.right;
            }
        }
    }
    void addRightBoundary(Node root, List<Integer> res) {
        Node curr = root.right;
        List<Integer> temp = new ArrayList<>();
        while (curr != null) {
            if (!isLeaf(curr)) {
                temp.add(curr.data);
            }
            if (curr.right != null) {
                curr = curr.right;
            } else {
                curr = curr.left;
            }
        for (int i = temp.size() - 1; i >= 0; --i) {
            res.add(temp.get(i));
        }
    }
    void addLeaves(Node root, List<Integer> res) {
        if (isLeaf(root)) {
            res.add(root.data);
            return;
        }
        if (root.left != null) {
            addLeaves(root.left, res);
        }
        if (root.right != null) {
            addLeaves(root.right, res);
        }
    }

    List<Integer> printBoundary(Node root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        if (!isLeaf(root)) {
            res.add(root.data);
        }
        addLeftBoundary(root, res);
        addLeaves(root, res);
        addRightBoundary(root, res);
        return res;
    }
}
```

# Mine Code

```java
import java.util.List;
import java.util.ArrayList;
public class Solution {
    private static boolean isLeaf(TreeNode node){
        return (node.left==null && node.right==null);
    }
    private static void traverseLeft(TreeNode node,List<Integer> list){
        if(node==null || isLeaf(node))return;
        list.add(node.data);
        if(node.left!=null)node = node.left;
        else node = node.right;
        traverseLeft(node,list);
    }
    private static void traverseLeafNodes(TreeNode node,List<Integer> list){
        if(node==null)return;
        if(isLeaf(node)){
            list.add(node.data);
            return;
        }
        traverseLeafNodes(node.left,list);
        traverseLeafNodes(node.right,list);
    }
    private static void traverseRight(TreeNode node,List<Integer> list){
        if(node == null || isLeaf(node))return;
        List<Integer> temp = new ArrayList<>();
        while(node!=null){
            temp.add(node.data);
            if(node.right!=null)node = node.right;
            else node = node.left;
        }
        int n = temp.size();
        for(int i=n-2;i>=0;i--){
            list.add(temp.get(i));
        }
    }
    public static List<Integer> traverseBoundary(TreeNode root){
        // Write your code here.
        List<Integer> ans = new ArrayList<>();
        ans.add(root.data);
        traverseLeft(root.left,ans);
        traverseLeafNodes(root,ans);
        traverseRight(root.right,ans);
        return ans;
    }
}
```