# Binary tree representation in CPP

![[Pasted image 20250325111226.png|400]]


```java
#include <iostream>
using namespace std;
struct Node{
    int data;
    struct Node* left;
    struct Node* right;
    Node(int data){
        this->data = data;
        left = right = NULL;
    }
};
int main() {
    // Write C++ code here
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->right = new Node(5);
    return 0;
}
```


# Binary representation of Tree in Java

![[Pasted image 20250325111353.png]]


```java
class Main {
    static class Node{
        int data;
        Node left;
        Node right;
        Node(int data){
            this.data = data;
        }
    }
    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.right = new Node(4);
    }
}
```


# Traversal Techniques
- To solve any problem you must learn to traverse the trees.
- For traversal there are two techniques that we use:
	- BFS -> Breadth First Search
		- **Breadth-First Search (BFS)** is a tree/graph traversal algorithm that explores all neighbors of a node before moving to the next level. It is particularly useful for finding the shortest path in an **unweighted graph**.
		- It searches level wise
		- ![[Pasted image 20250325112746.png]]
		- BFS traversal starting from node `1`: 1 → 2 → 3 → 4 → 5 → 6
	- DFS -> Depth First Search
		- ![[Pasted image 20250325112238.png|200]]
		- In-order traversal technique (left root right)
			- Order -> 4 2 5 1 6 3 7
		- Pre-order traversal technique (root left right)
			- Order -> 1 2 4 5 3 6 7
		- Post-order traversal technique (left right root)
			- Order -> 4 5 2 6 7 3 1



# Pre-Order Traversal

![[Pasted image 20250325113239.png]]


# In-Order Traversal

![[Pasted image 20250325113815.png]]

# Post-Order Traversal

![[Pasted image 20250325114153.png]]

To do all traversals in one go

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Stack;
import java.util.Arrays;
public class Solution {
    static class Element{
        TreeNode node;
        int pos;
        Element(TreeNode node,int pos){
            this.node = node;
            this.pos = pos;
        }
    }
    public static List<List<Integer>> getTreeTraversal(TreeNode root) {
        // Write your code here.
        List<Integer> preOrder = new ArrayList<>();
        List<Integer> inOrder = new ArrayList<>();
        List<Integer> postOrder = new ArrayList<>();
        Stack<Element> st = new Stack<>();
        st.add(new Element(root,1));
        while(!st.isEmpty()){
            Element cur = st.pop();
            if(cur.pos == 1){
                preOrder.add(cur.node.data);
                cur.pos++;
                st.push(cur);
                if(cur.node.left!=null)st.push(new Element(cur.node.left,1));
            }
            else if(cur.pos == 2){
                inOrder.add(cur.node.data);
                cur.pos++;
                st.push(cur);
                if(cur.node.right!=null)st.push(new Element(cur.node.right,1));
            }
            else{
                postOrder.add(cur.node.data);
            }
        }
        List<List<Integer>> ans = new ArrayList<>(Arrays.asList(inOrder,postOrder,preOrder));
        return ans;
    }
}
```

# Level Order Traversal (BFS)

![[Pasted image 20250325114952.png]]


Recursive Approach
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


Iterative Approach
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

# Modified BFS
**"Level Order Traversal with Indexing"** or **"BFS with Index Mapping"**

You can put any number as first index while inserting root
```java
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        Queue<Pair<TreeNode,Integer>> q = new LinkedList<>();
        q.add(new Pair<>(root,0));
        int maxWidth=0;
        while(!q.isEmpty()){
            int size = q.size();
            int start = q.peek().getValue();
            int end=start;
            for(int i=0;i<size;i++){
                Pair<TreeNode,Integer> cur = q.poll();
                TreeNode curNode = cur.getKey();
                end = cur.getValue();
                if(curNode.left!=null)q.offer(new Pair<>(curNode.left,2*end));
                if(curNode.right!=null)q.offer(new Pair<>(curNode.right,2*end + 1));
            }
            maxWidth = Math.max(maxWidth,end-start+1);
        }
        return maxWidth;
    }
}
```

Much better time complexity 99% beating

```java
class Solution {
    class Pair{
        TreeNode node;
        int index;
        Pair(TreeNode node,int index){
            this.node = node;
            this.index = index;
        }
    }
    public int widthOfBinaryTree(TreeNode root) {
        Queue<Pair> q = new LinkedList<>();
        q.add(new Pair(root,0));
        int maxWidth=0;
        while(!q.isEmpty()){
            int size = q.size();
            int start = q.peek().index;
            int end=start;
            for(int i=0;i<size;i++){
                Pair cur = q.poll();
                TreeNode curNode = cur.node;
                end = cur.index;
                if(curNode.left!=null)q.offer(new Pair(curNode.left,2*end));
                if(curNode.right!=null)q.offer(new Pair(curNode.right,2*end + 1));
            }
            maxWidth = Math.max(maxWidth,end-start+1);
        }
        return maxWidth;
    }
}
```