# ⇒ Trees

# BT Questions(Strivers):

## ⇒ Traversals:

[Introduction To Trees](Introduction%20To%20Trees%201bd613fdd81980a1b25fdcff15ca857c.md)

[144. Pre-order Traversal of Binary Tree](144%20Pre-order%20Traversal%20of%20Binary%20Tree%201bf613fdd81980858e14fbfa9d2c1733.md)

[94. In-Order Traversal](94%20In-Order%20Traversal%201bf613fdd81980c4841bf1d0d6831020.md)

[145. Post-order Traversal](145%20Post-order%20Traversal%201bf613fdd819803b9e5be7be34e7c207.md)

[102. Level Order Traversal](102%20Level%20Order%20Traversal%201c0613fdd81980b3ab93f22fd1c64985.md)

## ⇒ Medium Problems:

[104. Maximum Depth Of A Binary Tree](104%20Maximum%20Depth%20Of%20A%20Binary%20Tree%201bd613fdd819809b9dc8ff121370878b.md)

[111. Minimum Depth Of A Binary Tree](111%20Minimum%20Depth%20Of%20A%20Binary%20Tree%201c0613fdd8198002a4a6d6a975c330b1.md)

# BST Questions(Strivers):

## ⇒ Concepts

[700. Search In A BST](700%20Search%20In%20A%20BST%201bf613fdd81980859f79f3f39b165b32.md)

## ⇒ Practice Problems:

[701. Insert Into A BST](701%20Insert%20Into%20A%20BST%201bf613fdd81980918dcceceee6018033.md)

<aside>
💡

⇒ Why do we study Trees?

Advantages⇒ 

1. We study trees because they have O(Log n) time complexity for insertion/deletion and searching an element. They are comparatively efficient…
2. Here items are stored in order depending on the type of tree used…
3. Binary trees are cost efficient. System that are slower benefit from use of tree data structure.

Disadvantages⇒ 

1. When searching in an unbalanced Binary tree, it takes O(N) time complexity to search for an element in worst case. 
    1. How to solve?
    
    ⇒ Self-balancing Binary Trees like AVL (Adelson-Velsky and Landis Tree)
    
2. While working with sorted data, binary search trees are relatively inefficient.
</aside>

---

<aside>
💡

Where is it used?

⇒ File systems, databases,  network routing algorithms,  maths, decision trees(ML Algorithms), compression of files, B.T. are used in Heaps and Graphs…

</aside>

---

## Implementation And Properties Of Trees:

<aside>
💡

### ⇒ Structure:

```cpp
Node:
	int val;
	Node left;
	Node right;
```

### ⇒ Properties:

1. Size = Total no. of nodes.
2. Child-parent relationship.
3. If any two nodes have same parent then they are called sibling nodes. 
4. Edge is a line that connects two nodes.
5. Height of a B.T. is the maximum number of edges between the current node and leaf nodes of a Binary tree (counting from top-down).
6. Leaf Nodes are the terminating nodes of a tree. 
7. Difference between the height of the root node and height of the current node is called the depth of the tree.
8. If there is a path between two nodes then they have an ancestor-descendant relationship between them 
</aside>

---

<aside>
💡

### ⇒ Types of Binary Trees:

### 1. Complete Binary Tree:

⇒ A complete binary tree is a special type of binary tree where all the levels of the tree are filled completely except the lowest level nodes which are filled from as left as possible.

![](https://media.geeksforgeeks.org/wp-content/uploads/20220414154428/complete-200x132.jpg)

---

### 2. Full Binary Tree/Strict Binary Tree:

⇒ Each node has either two children or zero child. These are primarily used in segment trees and compression algos(Huffman coding).

![Screenshot 2025-03-21 at 2.18.10 PM.png](Screenshot_2025-03-21_at_2.18.10_PM.png)

---

### 3. Perfect Binary Tree:

⇒ All levels are filled…

![Screenshot 2025-03-21 at 2.19.26 PM.png](Screenshot_2025-03-21_at_2.19.26_PM.png)

---

### 4. Height Balanced Binary Trees:

⇒ Average height of these trees is O(log N)

---

### 5. Skewed Binary Tree:

⇒ Average height of such trees is O(N);

⇒ They basically act like Linked Lists…

![Screenshot 2025-03-21 at 2.22.20 PM.png](Screenshot_2025-03-21_at_2.22.20_PM.png)

---

### 6. Ordered Binary Tree:

⇒ Every node has some properties or conditions that it follows. Eg:- BST

</aside>

---

<aside>
💡

## Strivers definitions:

**Binary Tree: Binary tree is a fundamental hierarchical data structure in computer science that comprises nodes arranged in a tree-like structure. It consists of nodes, where each node can have at most two children nodes, known as the left child and the right child.**

**Nodes: Each node in a binary tree contains a piece of data, often referred to as the node’s value or key. This node also contains references and pointers to its left and right children so that we can traverse from one node to another in a hierarchical order.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2010.24.03%20PM-BBG163mj)

**Root Node: is the topmost node of a binary tree from which all other nodes stem out. This serves as the entry point for traversing the tree structure.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2010.32.28%20PM-v-X5--Te)

**Children Nodes are the nodes directly connected to a parent node. In a binary tree, a parent node can have zero, one or two children nodes, each situated to the left or right of the parent node.**

**Leaf Nodes are the nodes that do not have any children. These nodes lie on the outermost ends of the tree branches and are the terminal points of the traversal.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2010.38.14%20PM-KJLT1c4K)

**Ancestors in a Binary Tree are those nodes that lie on the path from a particular node to the root node. They are the nodes encountered while moving upwards from a specific node through its parent nodes until reaching the root of the tree.**

# **Full Binary Tree:**

**A Full Binary Tree, also known as a Strict Binary Tree, adheres to the structural property where every node has either zero or two children.**

**No node of this tree has just a single child, all internal nodes have exactly two children or in the case of leaf nodes, no children.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2010.50.34%20PM-ZOxI9m7m)

**The property that each node has either 2 or 0 children contributes significantly to the tree’s balance, making traversal, searching and insertion options more predictable and efficient.**

**The emphasis that the internal nodes must have exactly two children optimises the tree’s space utilisation and makes it more balanced.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2010.58.33%20PM-f0ArioLS)

# **Complete Binary Tree:**

**A Complete Binary Tree is a specialised form of Binary Tree where all levels are filled completely except possibly the last level, which is filled from left to right.**

**All levels of the tree, except possibly the last one, are fully filled. If the last level is not completely filled, it is filled from left to right, ensuring that nodes are positioned as far left as possible.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2011.07.37%20PM-TYfV3843)

**In a complete binary tree, all leaf nodes are in the last level or the second-to-last level, and they are positioned towards the leftmost side.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2011.20.00%20PM-DAsiUGEt)

**This structure is particularly useful for storing data in structures like heaps, where efficient access to the top element (root) or certain properties (e.g., maximum or minimum values in a heap) is crucial. The completeness property of a complete binary tree aids in achieving balanced structures, making it easier to implement algorithms and ensuring reasonably consistent performance.**

**One important aspect to note is that although it might seem similar to a full binary tree, a complete binary tree doesn't require all nodes to have two children; it's about the positioning and arrangement of nodes.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2011.21.45%20PM-WTpYIRNI)

# **Perfect Binary Tree:**

**A Perfect Binary tree is a type of Binary Tree where all leaf nodes are at the same level and the number of leaf nodes is maximised for that level.**

**Every node in a perfect binary tree has either zero or two children. This means that every internal node (non-leaf node) has exactly two children and all leaf nodes are at the same level.**

**All levels of this tree are fully filled with nodes including the last level. Perfect Binary Trees have a balanced structure that maximises the number of nodes for a given height, creating a dense structure where the number of nodes doubles as we move down each level of the tree.**

**Properties of perfect binary trees make them efficient for certain operations like searching and sorting due to their balanced nature. However, achieving and maintaining perfect balance, especially when the number of nodes is not a power of two, might not be feasible in many practical applications.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-06%20at%2011.30.33%20PM-yGediDDP)

**All levels of this tree are fully filled with nodes including the last level. Perfect Binary Trees have a balanced structure that maximises the number of nodes for a given height, creating a dense structure where the number of nodes doubles as we move down each level of the tree.**

**Properties of perfect binary trees make them efficient for certain operations like searching and sorting due to their balanced nature. However, achieving and maintaining perfect balance, especially when the number of nodes is not a power of two, might not be feasible in many practical applications.**

# **Balanced Binary Tree:**

**A Balanced Binary tree is a type of Binary Tree where the heights of the two subtrees of any node differ by at most one. This property ensures that the tree remains relatively well-balanced, preventing the tree from becoming highly skewed or degenerate.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-07%20at%205.04.25%20PM-VWCvKhF_)

**In a balanced binary tree, the height of the tree should be log2N at maximum, where N is the number of nodes. This ensures that the tree does not become heavily skewed or imbalanced. The distribution of nodes of both the left and right subtrees remains relatively even throughout the tree.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-07%20at%205.10.05%20PM-y2CpXcgt)

# **Degenerate Tree:**

**A Degenerate Tree is a Binary Tree where the nodes are arranged in a single path leaning to the right or left. The tree resembles a linked list in its structure where each node points to the next node in a linear fashion.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-07%20at%205.20.06%20PM-Qiy8o0-M)

**There’s a lot of imbalance in the tree structure due to the sequential arrangement of nodes. This lack of balance results in a tree that resembles a singly linked list rather than a branching structure.**

**Each level of this tree only has one node. The height of tree reaches ‘n’ ie. the number of nodes in the tree, resulting in inefficient search operations. Though degenerate trees are not commonly used intentionally due to their inefficient nature for most operations, they may occur inadvertently in scenarios where nodes are inserted in a specific order (e.g., always to the right or left), causing the tree to lose its balanced properties.**

[](https://static.takeuforward.org/content/Screenshot%202024-01-04%20at%202.04.32%20PM-p6J1o2lA)

**Understanding degenerate trees is essential in analysing the worst-case time complexity of algorithms in scenarios where the tree structure degrades to this linear form, as it can help in optimising algorithms for these situations.**

# **In Summary:**

[](https://static.takeuforward.org/content/Screenshot%202024-01-07%20at%205.20.06%20PM-x15SJzOS)

**In summary, Binary Trees introduce a hierarchical arrangement taking a step ahead of the linear structure we have studied so far.**

**Binary Trees comprise of nodes, each capable of hosting at most two children hence the predecessor ‘Binary”. These structures mirror the hierarchical oraganisation seen in file systems.**

**Full Binary Trees impose the constraint that each node possesses either zero or two children, promoting a well-balanced structure and enhancing predictability in operations like traversal and insertion.**

**Complete Binary Trees, on the other hand, embrace a specialized form where all levels, save possibly the last, are completely filled. Their design, ensuring nodes are positioned leftmost on the last level, proves valuable for efficient data storage and access, resembling the organized arrangement of folders and files in a computer system.**

**Perfect Binary Trees take this hierarchical order a step further, showcasing a balanced structure where all leaf nodes align at the same level. Such trees optimize space by filling all levels with nodes, creating a dense structure.**

**Balanced Binary Trees ensure the difference in heights between subtrees of any node remains minimal, preventing significant skewing or imbalance.**

**Degenerate Trees represent a case where nodes arrange linearly, akin to a linked list, posing inefficiencies in search operations due to the lack of balance.**

</aside>

---

<aside>
💡

## ***Properties useful in Problem-solving***:

### 1. Total number of nodes in perfect binary tree, height = h but total number of nodes (2^(h+1))-1…

### 2. Leaf nodes in perfect binary tree is equivalent to 2^height…

### 3. (Perfect trees applicable)

### If n = no. of leaves, then minimum height is log(N)

### If n = no. of nodes, then the minimum number of levels we will have is equivalent to log(n+1)-1 levels.

### 4. In a strict/full binary tree, if we have N leaf nodes….then we have N-1⇒Internal nodes. Also it can be said that

**No. of leaf nodes = No. of internal nodes + 1**

### 5. Degree of a tree in our case is either 0, 1, 2.

### 6. GENERAL CASE:

Number of leaf nodes = 1 + Number of internal nodes with two children[not including root]

</aside>

---

# Implementation:

<aside>
💡

There are two ways to achieve trees:

- Linked representation(using pointers)
    - Covered by KK
- Sequential representation(using arrays)
    - Covered under Heaps
</aside>

## ⇒ Binary Tree Implementation:

```cpp
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

import java.util.*;

class BinaryTree{
    public BinaryTree(){}
    
    class Node{
        public Node left;
        public Node right;
        private int val;
        
        public Node(int data){
            this.val = data;
        }
    }
    
    private Node root;

    // insertion 
    public void populate(Scanner input){
        System.out.print("Enter the root node value: ");
        int val = input.nextInt();
        root = new Node(val);
        populate(input, root);
    }
    
    // overload populate
    public void populate(Scanner input, Node curr){
        System.out.print("Enter whether left of "+ curr.val + " ");
        boolean left = input.nextBoolean();
        if(left){
            System.out.print("Enter the value to the left of "+ curr.val + " ");
            int value = input.nextInt();
            curr.left = new Node(value);
            populate(input, curr.left);
        }
        
        System.out.println();
        
        System.out.print("Enter whether right of "+ curr.val + " ");
        boolean right = input.nextBoolean();
        if(right){
            System.out.print("Enter the value to the right of "+ curr.val + " ");
            int value = input.nextInt();
            curr.right = new Node(value); 
            populate(input, curr.right);
        }
    }
    
    // displaing tree
    public void display(){
        display(root, "");
    }
    
    private void display(Node trav, String indent){
        if(trav==null) return;
        
        System.out.println(indent + trav.val);
        display(trav.left, indent+" ");
        display(trav.right, indent.substring(0, indent.length()));
    }
    
    public void prettyDisplay(){
        prettyDisplay(root, 0);
    }
    
    private void prettyDisplay(Node node, int level){
        if(node==null){
            return;
        }
        
        prettyDisplay(node.right, level+1);
        
        if(level!=0){
            for(int i = 0; i<level-1; i++){
                System.out.println("|\t\t");
            }
            System.out.println("!------->" + node.val);
        }else{
            System.out.println(node.val);
        }
        
        prettyDisplay(node.left, level+1);
    }
    
}

class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        BinaryTree tree = new BinaryTree();
        tree.populate(input);
        tree.prettyDisplay();
    }
}
```

---

# ⇒ Binary-Search Tree:

(Assumption: Tree is balanced i.e. height difference between any two nodes is at most 1)

<aside>
💡

1. The main property of BST is that the left-hand side elements are smaller and the right hand side elements are larger than the current node.
2. In-order Traversal Of A BST is always in Sorted order…
3. Structure:

```cpp
Node{
	int val;
	Node left;
	Node right;
  int height; 
}
```

1. BST are balanced trees and the insertion and search time in such trees is log N…

```cpp
class BST {
  public class Node {
    private int value;
    private Node left;
    private Node right;
    private int height;

    public Node(int value) {
      this.value = value;
    }

    public int getValue() {
      return value;
    }
  }

  private Node root;

  public BST() {

  }

  public void insert(int value) {
    root = insert(value, root);
  }

  private Node insert(int value, Node node) {
    if (node == null) {
      node = new Node(value);
      return node;
    }

    if (value < node.value) {
      node.left = insert(value, node.left);
    }

    if (value > node.value) {
      node.right = insert(value, node.right);
    }

    node.height = Math.max(height(node.left), height(node.right)) + 1;
    return node;
  }

  public void populate(int[] nums) {
    for (int i = 0; i < nums.length; i++) {
      this.insert(nums[i]);
    }
  }

  public void populatedSorted(int[] nums) {
    populatedSorted(nums, 0, nums.length);
  }

  private void populatedSorted(int[] nums, int start, int end) {
    if (start >= end) {
      return;
    }

    int mid = (start + end) / 2;

    this.insert(nums[mid]);
    populatedSorted(nums, start, mid);
    populatedSorted(nums, mid + 1, end);
  }

  public void display() {
    display(this.root, "Root Node: ");
  }

  private void display(Node node, String details) {
    if (node == null) {
      return;
    }
    System.out.println(details + node.value);
    display(node.left, "Left child of " + node.value + " : ");
    display(node.right, "Right child of " + node.value + " : ");
  }

  public boolean isEmpty() {
    return root == null;
  }

  public int height(Node node) {
    if (node == null) {
      return -1;
    }
    return node.height;
  }

  public boolean balanced() {
    return balanced(root);
  }

  private boolean balanced(Node node) {
    if (node == null) {
      return true;
    }
    return Math.abs(height(node.left) - height(node.right)) <= 1 && balanced(node.left) && balanced(node.right);
  }
}

class Main {
  public static void main(String[] args) {
    // Scanner scanner = new Scanner(System.in);
    // BinaryTree tree = new BinaryTree();
    // tree.populate(scanner);
    // tree.prettyDisplay();

    BST tree = new BST();
    int[] nums = { 5, 2, 7, 1, 4, 6, 9, 8, 3, 10 };
    tree.populate(nums);
    tree.display();
  }
}
```

</aside>

---

# ⇒ Traversals:

1. Pre-order: N→L→R
2. In-order: L→N→R
3. Post-order: L→R→N
    1. When we need to delete from a binary tree, then we use post-order.
    2. When we perform bottom-up calculation and diameter of a tree.

---