Given the root node of a binary search tree (BST) and an integer key. Return the **Inorder predecessor** and **successor** of the given key from the provided BST.

If predecessor or successor is missing then return -1.

Examples:

**Input :** root = [5, 2, 10, 1, 4, 7, 12] , key = 10

**Output :** [7, 12]

**Explanation :**

![](https://static.takeuforward.org/content/ProblemSetter-8D_p20dq)

**Input :** root = [5, 2, 10, 1, 4, 7, 12] , key = 12

**Output :** [10, -1]

**Explanation :**

![](https://static.takeuforward.org/content/ProblemSetter-copgO0cS)

# Brute
TC-> O(N)
```java
class Solution {
    List<Integer> inorder;
    List<Integer> succPredBST(TreeNode root, int key) {
        //your code goes here
        inorder=new ArrayList<>();
        dfs(root);
        int n = inorder.size();
        int predecessor = -1;
        int successor = -1;
        for(int i=0;i<n;i++){
            if(inorder.get(i) == key){
                if(i-1>=0)predecessor = inorder.get(i-1);
                if(i+1<n)successor = inorder.get(i+1);
                break;
            }
        }
        return new ArrayList<>(List.of(predecessor,successor));
    }
    private void dfs(TreeNode root){
        if(root==null)return;
        dfs(root.left);
        inorder.add(root.data);
        dfs(root.right);
    }
}
```


# Optimal

TC-> O(height of the tree)
```java
class Solution {
    List<Integer> succPredBST(TreeNode root, int key) {
        //your code goes here
        int successor=-1;
        int predecessor=-1;
        TreeNode trav=root;
        while(trav!=null){
            if(trav.data==key){
                TreeNode left = trav.left;
                TreeNode right = trav.right;
                while(left!=null){
                    predecessor=left.data;
                    left=left.right;
                }
                while(right!=null){
                    successor=right.data;
                    right=right.left;
                }
                break;
            }
            else if(trav.data>key){
                successor=trav.data;
                trav=trav.left;
            }
            else{
                predecessor=trav.data;
                trav=trav.right;
            }
        }
        return new ArrayList<>(List.of(predecessor,successor));
    }
}
```


# Similar question

[Link](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1)
```java

class Solution {
    public ArrayList<Node> findPreSuc(Node root, int key) {
        // code here
        if(root == null) return new ArrayList<>(Arrays.asList(null, null));
        Node p = null, s = null;
        Node trav = root;
        while (trav != null && trav.data != key) {
            if (trav.data < key) {
                p = trav;
                trav = trav.right;
            } else {
                s = trav;
                trav = trav.left;
            }
        }
        if(trav == null) return new ArrayList<>(Arrays.asList(p, s));
        Node left = trav.left;
        Node right = trav.right;
        while(left != null) {
            p = left;
            left = left.right;
        }
        while(right != null) {
            s = right;
            right = right.left;
        }
        return new ArrayList<>(Arrays.asList(p, s));
    }
}
```