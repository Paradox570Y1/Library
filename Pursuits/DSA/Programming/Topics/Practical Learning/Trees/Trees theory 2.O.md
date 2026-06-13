- Unlike other data structures Tree is an hierarchical data structure
- In binary trees you have at max 2 child nodes.
- Node which does not have children are leaf nodes.
- Any node and relative to it the beneath nodes are together called as subtree of the tree.
- For lower nodes , the upper nodes are their ancestors whether parent or parent of parent.


# 5 Types of binary Trees

- Full Binary Tree
	- Every node will either have 2 or 0 children
- Complete Binary Trees
	- All levels are completely filled except the last level.
	- The last level has nodes as left as possible.
- Perfect Binary Trees
	- All leaf nodes are at the same level.
- Balanced Binary Trees
	- A **balanced tree** is a binary tree in which the height difference between the left and right subtrees of any node is minimized.
	- The goal of balancing a tree is to ensure efficient operations, such as insertion, deletion, and searching, all of which ideally run in **O(log⁡N)** time.
	- Height can be at maximum of log N where N is no. of nodes.
	- Used in databases, file systems, and memory indexing.
- Degenerate Trees (also called a **pathological tree**)
	- Each node has at most one child.
	- Behaves more like linked list than a balanced trees.
	- The height of the tree is equal to the number of nodes (i.e., O(N)).
	- 1. It can be **left-skewed** (all nodes have only left children) or **right-skewed** (all nodes have only right children).
	- Worst-case time complexity for operations like search, insertion, and deletion is **O(N)** instead of **O(log⁡N)** in balanced trees.


# Some useful formulas
1. Total number of nodes in perfect binary tree, height = h but total number of nodes (2^(h+1))-1…

2. Leaf nodes in perfect binary tree is equivalent to 2^height…

3. (Perfect trees applicable) //height and width is relatable in perfect trees.
	- If n = no. of leaves, then minimum height is log(N)
	- If n = no. of nodes, then the minimum number of levels or minimum height we will have is equivalent to log(n+1)-1 levels.  //even node count and height is relatable

4. In a strict/full binary tree, if we have N leaf nodes then we have N-1⇒Internal nodes. Also it can be said that
	- **No. of leaf nodes = No. of internal nodes + 1**
5. Degree of a tree in our case is either 0, 1, 2.
	In **tree terminology (DSA context)**:
		Degree of a node = number of its children
6. GENERAL CASE:
	- Number of leaf nodes = 1 + Number of internal nodes with two children not including root

