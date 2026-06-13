[Link](https://www.naukri.com/code360/problems/childrensumproperty_790723?leftPanelTabValue=PROBLEM)
## Problem statement

Send feedback

Given a binary tree of nodes 'N', you need to modify the value of its nodes, such that the tree holds the Children sum property.

A binary tree is said to follow the children sum property if, for every node of that tree, the value of that node is equal to the sum of the value(s) of all of its children nodes( left child and the right child).

**Note :**

```
 1. You can only increment the value of the nodes, in other words, the modified value must be at least equal to the original value of that node.
 2. You can not change the structure of the original binary tree.
 3. A binary tree is a tree in which each node has at most two children.      
 4. You can assume the value can be 0 for a NULL node and there can also be an empty tree.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints :**

```
1 <= T <= 10^2
0 <= N <= 10^2
1 <= node.Value <= 10^6

Time Limit : 1 sec
```

**Sample Input 1 :**

```
1
2 35 10 2 3 5 2 -1 -1 -1 -1 -1 -1 -1 -1 
```

**Sample Output 1 :**

```
Valid ( One of the possible answers is : 45 35 10 32 3 8 2 -1 -1 -1 -1 -1, thus if the user modifies the given tree like this, the output printed will be valid).
```

**Explanation For Sample Input 1 :**

```
The tree can be represented as follows :
```

![altimage](https://files.codingninjas.in/screenshot-from-2020-10-09-12-55-59-5133.png)

```
The value at the root node is 2 which is less than the sum of its children’s values (35 + 10). So we simply increase the value at the root node to 45. The node with value  = 35 has children with values 2 and 3 so their sum i.s 2 + 3 = 5 < 35. As we can't decrement any value, so instead we have to increase the sum of children and thus we update 35's children (2 and 3) as 30 and 5 so that 30 + 5 = 35 and the same is done for the children of the node with value = 10.
```

#### The final tree looks like this :

![altimage](https://files.codingninjas.in/screenshot-from-2020-10-09-12-56-05-5132.png)

```
Note that there can be many other valid solutions.
```

**Sample Input 2 :**

```
1
10 5 5 -1 -1 -1 -1
```

**Sample Output 2 :**

```
Valid
```



# Optimal

```java
public class Solution {
    public static void changeTree(BinaryTreeNode < Integer > parent) {
        // Write your code here.
        if(parent==null)return;
        int left=0;
        if(parent.left!=null)left=parent.left.data;
        int right=0;
        if(parent.right!=null)right=parent.right.data;
        if(left==0 && right==0)return;
        else if(parent.data>left+right){
            if(left!=0)parent.left.data = parent.data;
            if(right!=0)parent.right.data = parent.data;
        }
        changeTree(parent.left);
        changeTree(parent.right);
        if(parent.left==null)parent.data = parent.right.data;
        else if(parent.right==null)parent.data = parent.left.data;
        else parent.data = parent.left.data+parent.right.data;
    }
}
```

OR 

```java
public class Solution {
    public static void changeTree(BinaryTreeNode < Integer > parent) {
        // Write your code here.
        if(parent==null)return;
        int child=0;
        if(parent.left!=null)child+=parent.left.data;
        if(parent.right!=null)child+=parent.right.data;
        if(parent.data>child){
            if(parent.left!=null)parent.left.data = parent.data;
            if(parent.right!=null)parent.right.data = parent.data;
        }
        changeTree(parent.left);
        changeTree(parent.right);
        child=0;
        if(parent.left==null && parent.right==null)return;
        if(parent.right!=null)child+= parent.right.data;
        if(parent.left!=null)child+= parent.left.data;
        parent.data = child;
    }
}
```