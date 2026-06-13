An AVL tree defined as a self-balancing Binary Search Tree (BST) where the difference between heights of left and right subtrees for any node cannot be more than one. The values above the nodes in the below diagram show difference between left and right subtrees.

Balance Factor = left subtree height - right subtree height  
For a Balanced Tree(for every node): 
	-1 ≤ Balance Factor ≤ 1

## 🔹 Height convention (important)
- **Leaf node height = 0**
- **Null child height = -1**

![Example-of-an-AVL-Tree-11](https://media.geeksforgeeks.org/wp-content/uploads/20250703161306662411/Example-of-an-AVL-Tree-11.webp "Click to enlarge")

Basic operations on AVL Tree include, Insertion, search and delete


### Example of an AVL Tree:

The balance factors for different nodes are: 12 : +1,   8 : +1,   18 : +1,   5 : +1,   11 : 0,   17 : 0 and  4 : 0. Since all differences are lies between -1 to +1, so the tree is an AVL tree.

![Example-of-an-AVL-Tree-11](https://media.geeksforgeeks.org/wp-content/uploads/20250703161306662411/Example-of-an-AVL-Tree-11.webp "Click to enlarge")

### Example of a BST which is not an AVL Tree:

The Below Tree is ***not*** an AVL Tree as the balance factor for nodes ***8*** and ***12*** is more than ***1***.

![Example-of-an-AVL-Tree-22](https://media.geeksforgeeks.org/wp-content/uploads/20250703161407500927/Example-of-an-AVL-Tree-22.webp "Click to enlarge")

### Important Points about AVL Tree:

- ***Rotations***: rotations are designed to restore balance in ***O(1)*** time while ensuring the overall time complexity remains ***O(log n)***. AVL Trees use ***four cases*** to rebalance themselves after insertions and deletions: 
	- Left-Left (LL) 
	- Right-Right (RR)
	- Left-Right (LR) 
	- Right-Left (RL)
- ***Insertion and Deletion***: While insertion is followed by upward traversals to check balance and apply rotations, deletion can be more complex due to multiple rotations possibly being required. AVL Trees may require multiple rebalancing steps during deletion, unlike Red-Black Trees which limit this better.
- ***Use Cases***: AVL Trees are particularly useful when you need frequent and efficient lookups, like in database indexing, memory-intensive applications, or where predictable time complexity is crucial.
- ***Drawbacks Compared to Other Trees***: Although faster in lookups than Red-Black Trees, AVL Trees might incur slightly more overhead on insertions and deletions due to stricter balancing requirements. As a result, Red-Black Trees are more common in standard libraries like `TreeMap` or `TreeSet` in Java or `map` in C++ STL.
- ***In-order Traversal***: An in-order traversal of an AVL Tree still gives you elements in sorted order, just like any Binary Search Tree.

### Operations on an AVL Tree:

- ***Searching*** : It is same as normal Binary Search Tree (BST) as an AVL Tree is always a BST. So we can use the same implementation as BST. The advantage here is time complexity is O(log n)
- ***Insertion*** : It does rotations along with normal BST insertion to make sure that the balance factor of the impacted nodes is less than or equal to 1 after insertion
- ***Deletion*** : It also does rotations along with normal BST deletion to make sure that the balance factor of the impacted nodes is less than or equal to 1 after deletion.


### Insertion in AVL Trees

To make sure that the given tree remains AVL after every insertion, we must augment the standard BST insert operation to perform some re-balancing.  Following are two basic operations that can be performed to balance a BST without violating the BST property (keys(left) < key(root) < keys(right)). 

- Left Rotation 
- Right Rotation
![[Pasted image 20260209113859.png|400]]


```java
import java.util.*;

class Node { 
    int key; 
    Node left; 
    Node right; 
    int height; 

    Node(int k) { 
        key = k; 
        left = null; 
        right = null; 
        height = 1; 
    }
} 

class GfG {

    // A utility function to get the
    // height of the tree 
    static int height(Node N) { 
        if (N == null) 
            return 0; 
        return N.height; 
    } 

    // A utility function to right rotate
    // subtree rooted with y 
    static Node rightRotate(Node y) { 
        Node x = y.left; 
        Node T2 = x.right; 

        // Perform rotation 
        x.right = y; 
        y.left = T2; 

        // Update heights 
        y.height = 1 + Math.max(height(y.left), 
                                height(y.right)); 
        x.height = 1 + Math.max(height(x.left), 
                                height(x.right)); 

        // Return new root 
        return x; 
    } 

    // A utility function to left rotate 
    // subtree rooted with x 
    static Node leftRotate(Node x) { 
        Node y = x.right; 
        Node T2 = y.left; 

        // Perform rotation 
        y.left = x; 
        x.right = T2; 

        // Update heights 
        x.height = 1 + Math.max(height(x.left),
                                height(x.right)); 
        y.height = 1 + Math.max(height(y.left), 
                                height(y.right)); 

        // Return new root 
        return y; 
    } 

    // Get balance factor of node N 
    static int getBalance(Node N) { 
        if (N == null) 
            return 0; 
        return height(N.left) - height(N.right); 
    } 

    // Recursive function to insert a key in
    // the subtree rooted with node 
    static Node insert(Node node, int key) { 
      
        // Perform the normal BST insertion
        if (node == null) 
            return new Node(key); 

        if (key < node.key) 
            node.left = insert(node.left, key); 
        else if (key > node.key) 
            node.right = insert(node.right, key); 
        else // Equal keys are not allowed in BST 
            return node; 

        // Update height of this ancestor node 
        node.height = 1 + Math.max(height(node.left), 
                                   height(node.right)); 

        // Get the balance factor of this ancestor node 
        int balance = getBalance(node); 

        // If this node becomes unbalanced,
        // then there are 4 cases 

        // Left Left Case 
        if (balance > 1 && key < node.left.key) 
            return rightRotate(node); 

        // Right Right Case 
        if (balance < -1 && key > node.right.key) 
            return leftRotate(node); 

        // Left Right Case 
        if (balance > 1 && key > node.left.key) { 
            node.left = leftRotate(node.left); 
            return rightRotate(node); 
        } 

        // Right Left Case 
        if (balance < -1 && key < node.right.key) { 
            node.right = rightRotate(node.right); 
            return leftRotate(node); 
        } 

        // Return the (unchanged) node pointer 
        return node; 
    } 

    // A utility function to print preorder 
    // traversal of the tree 
    static void preOrder(Node root) { 
        if (root != null) { 
            System.out.print(root.key + " "); 
            preOrder(root.left); 
            preOrder(root.right); 
        } 
    } 

    // Driver code 
    public static void main(String[] args) { 
        Node root = null; 
        
        // Constructing tree given in the above figure 
        root = insert(root, 10); 
        root = insert(root, 20); 
        root = insert(root, 30); 
        root = insert(root, 40); 
        root = insert(root, 50); 
        root = insert(root, 25); 
        
        /* The constructed AVL Tree would be 
                  30 
                /   \ 
              20     40 
             /  \      \ 
           10   25     50 
        */
        
    // Preorder traversal
        preOrder(root); 
    } 
}
```


# Deletion in an AVL Tree

***Steps to follow for deletion***.   
To make sure that the given tree remains AVL after every deletion, we must augment the standard BST delete operation to perform some re-balancing. Following are two basic operations that can be performed to re-balance a BST without violating the BST property (keys(left) < key(root) < keys(right)). 

1. Left Rotation
2. Right Rotation
