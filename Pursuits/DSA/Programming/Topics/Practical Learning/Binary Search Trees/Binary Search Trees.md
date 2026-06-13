- [[BST Theory]]
- [[Self Balancing Trees]]
- [[Segment Trees]]
# Problems
- [[700. Search in a Binary Search Tree]] //move left right until null
- [[Floor and Ceil in a BST]] // in iterative way keep a global pointer to the ceil or floor as in their domain and evaluate equal before hand
  // in recursive carry an extra variable for keeping track of ceil or floor in their domain
  //domain of ceil is greater than and for floor is less than and equal is handle before hand
- [[701. Insert into a Binary Search Tree]] //keep track of parent while trying to reach the node to be inserted
- [[Inorder successor and predecessor in BST]] // similar to ceil and floor just equal part requires intuition to check for any successor or predecessor that lies to the left or right.
-  [[450. Delete Node in a BST]] // To delete a node either shift the nodes which are left of target to left of the node which is leftmost of right node to the target and in case their is no such right node then directly connect parent of target to node which is left of target.
   Or shift the nodes which are right of target to right of the node which is rightmost of left node to the target and in case their is no such left node then directly connect parent to the right node.
- [[230. Kth Smallest Element in a BST]] // Do inorder traversal while keeping count globally until we have found it which means we are not returning -1 anymore
- [[Kth largest Element in a BST ]] // Do reverse inorder traversal while keeping count globally until we have found it which means we are not returning -1 anymore
- [[98. Validate Binary Search Tree]] // check current node in range or not
- [[235. Lowest Common Ancestor of a Binary Search Tree]] // check if no node is found in left subtree move to right subtree and vice versa but if node is found in both left and right subtree return current node as that is the LCA.
  OR take the given nodes as range by ensuring first node is smaller and second node is bigger then check if current node is bigger than the range then move to left subtree and if current node is smaller than the range then move to right subtree , now if current node is not to the left or right then that's the LCA as it lies between that range or let's say those nodes.
- [[1008. Construct Binary Search Tree from Preorder Traversal]] create a global counter to traverse and create a node and then recursively create left subtree first then right subtree if preorder is traversed or max bound check fails return null.
- [[173. Binary Search Tree Iterator]] // In this you have to breakdown the iterative inorder traversal using stack
- [[653. Two Sum IV - Input is a BST]] //create inorder array out of BST and then use two pointer to find the sum or create some `BSTIterator` which let's you iterate through the graph
- [[99. Recover Binary Search Tree]] // traverse inorder and while doing so keep track of 2-3 nodes which are not in order then if their are just 2 nodes then swap those otherwise in case of 3 swap the first node with the 3rd one as two defective node are present in different subtree.
- [[Largest BST in Binary Tree]] // Use an object to store range and size during backtracking and if range fails for current node then return the max size of left and right subtree and make the range impossible for their ancestors as now BST can no longer increase.



# Other problems

- [[1382. Balance a Binary Search Tree]]