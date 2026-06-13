[Largest BST](https://www.geeksforgeeks.org/problems/largest-bst/1)

Difficulty: **Medium**Accuracy: **29.73%**Submissions: **169K+**Points: **4**Average Time: **40m**

You're given a binary tree. Your task is to find the **size** of the largest subtree within this binary tree that also satisfies the properties of a Binary Search Tree (BST). The size of a subtree is defined as the number of nodes it contains.

**Note:** A subtree of the binary tree is considered a BST if for every node in that subtree, the left child is less than the node, and the right child is greater than the node, without any duplicate values in the subtree.

**Examples :**

**Input**: root = [5, 2, 4, 1, 3]  
![Root-to-leaf-path-sum-equal-to-a-given-number-copy](https://media.geeksforgeeks.org/wp-content/uploads/20241007154946544659/Root-to-leaf-path-sum-equal-to-a-given-number-copy.webp)  
**Output**: 3  
**Explanation**:The following sub-tree is a BST of size 3  
![Balance-a-Binary-Search-Tree-3-copy](https://media.geeksforgeeks.org/wp-content/uploads/20241008164418969970/Balance-a-Binary-Search-Tree-3-copy.webp)

**Input**: root = [6, 7, 3, N, 2, 2, 4]  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700351/Web/Other/blobid0_1732253153.png)  
**Output**: 3  
**Explanation**: The following sub-tree is a BST of size 3:  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700351/Web/Other/blobid1_1732253193.png)  

**Constraints:**  
1 ≤ number of nodes ≤ 105  
1 ≤ node->data ≤ 105


```java
class Solution{
    
    // Return the size of the largest sub-tree which is also a BST
    private static class container{
        int size,max,min;
        container(int size,int max,int min){
            this.size=size;
            this.max = max;
            this.min = min;
        }
    }
    private static container helper(Node node){
        if(node==null)return new container(0,Integer.MIN_VALUE,Integer.MAX_VALUE);
        container left = helper(node.left);
        container right = helper(node.right);
        if(left.max<node.data && right.min>node.data){
            return new container(left.size+right.size+1,Math.max(right.max,node.data),Math.min(left.min,node.data));
        }
        return new container(Math.max(left.size,right.size),Integer.MAX_VALUE,Integer.MIN_VALUE);
    }
    static int largestBst(Node root)
    {
        // Write your code here
        return helper(root).size;
    }
```

OR

```java
class Solution {
    static class Range{
        int min;
        int max;
        int size;
        Range(int min, int max , int size) {
            this.min = min;
            this.max = max;
            this.size = size;
        }
    }
    // Return the size of the largest sub-tree which is also a BST
    static int largestBst(Node root) {
        // Write your code here
        return helper(root).size;
    }
    static Range helper(Node root) {
        if(root == null) return new Range(Integer.MAX_VALUE, 0, 0);
        Range left = helper(root.left);
        Range right = helper(root.right);
        
        if(left.max < root.data && root.data < right.min) {
            return new Range(Math.min(left.min, root.data), Math.max(right.max, root.data), 1 + left.size + right.size);
        }
        return new Range(Integer.MIN_VALUE, Integer.MAX_VALUE, Math.max(left.size, right.size));
    }
}
```