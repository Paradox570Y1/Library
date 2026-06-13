[Link](https://www.geeksforgeeks.org/problems/binary-tree-representation/1)

Difficulty: **Easy**Accuracy: **75.76%**Submissions: **37K+**Points: **2**Average Time: **15m**

You are given an array nodes. It contains 7 integers, which represents the value of nodes of the binary tree in level order traversal. You are also given a root of the tree which has a value equal to nodes[0].

Your task to construct a binary tree by creating nodes for the remaining 6 nodes.

**Example:**

**Input:** 
nodes = [1 2 3 4 5 6 7]
**Output:** 
        1
        /   \     
       2       3  
     /  \     /  \
    4  5    6   7
**Explanation:** 
The 7 node binary tree is represented above.

**Your Task:**

Complete the function v**oid create_tree(node* root0, vector &vec)**, which takes a root of a Binary tree and vector array vec containing the values of nodes.

**Expected Time Complexity:** O(1).

**Expected Auxiliary Space:** O(1).

**Constraints:**

vec.length = 7

1<=vec[i]<=100



```java
class Solution{
    public static void createTree(Node root0, ArrayList<Integer> v ){
        // Code here
        Queue<Node> q = new LinkedList<Node>();
        int i=1;
        q.offer(root0);
        while(!q.isEmpty() && i<v.size()){
            Node cur = q.poll();
            cur.left = new Node(v.get(i));
            i++;
            q.offer(cur.left);
            if(i<v.size()){
                cur.right = new Node(v.get(i));
                i++;
                q.offer(cur.right);
            }
        }
    }
}
```


OR

```java
// User function Template for Java

class Solution {
    private static Node helper(Node root, ArrayList<Integer> v, int i) {
        if (i >= v.size()) return null;
        Node node = new Node(v.get(i));
        if (i == 0) node = root;
        node.left = helper(root, v, 2*i + 1);
        node.right = helper(root, v, 2*i + 2);
        return node;
    }
    public static void createTree(Node root0, ArrayList<Integer> v) {
        // Code here
        helper(root0, v, 0);
    }
}
```


OR

```java
// User function Template for Java

class Solution {
    private static Node root;
    private static Node helper(ArrayList<Integer> v, int i) {
        if (i >= v.size()) return null;
        Node node = new Node(v.get(i));
        if (i == 0) node = root;
        node.left = helper(v, 2*i + 1);
        node.right = helper(v, 2*i + 2);
        return node;
    }
    public static void createTree(Node root0, ArrayList<Integer> v) {
        // Code here
        root = root0;
        helper(v, 0);
    }
}
```