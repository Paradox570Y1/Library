
Problem statement

You have been given a Binary Tree of _**'N'**_ nodes, where the nodes have integer values.

Your task is to return the ln-Order, Pre-Order, and Post-Order traversals of the given binary tree.


**For example :**

```
For the given binary tree:
```

![Binary - Tree1](https://files.codingninjas.in/tt1-6639.jpg)

```
The Inorder traversal will be [5, 3, 2, 1, 7, 4, 6].
The Preorder traversal will be [1, 3, 5, 2, 4, 7, 6].
The Postorder traversal will be [5, 2, 3, 7, 6, 4, 1].
```

Detailed explanation ( Input/output format, Notes, Images )

**Sample Input 1 :**

```
1 2 3 -1 -1 -1  6 -1 -1
```

**Sample Output 1 :**

```
2 1 3 6 
1 2 3 6 
2 6 3 1
```

**Explanation of Sample Output 1 :**

```
 The given binary tree is shown below:
```

![BT - 3](https://files.codingninjas.in/tt3-6641.jpg)

```
Inorder traversal of given tree = [2, 1, 3, 6]
Preorder traversal of given tree = [1, 2, 3, 6]
Postorder traversal of given tree = [2, 6, 3, 1]
```

**Sample Input 2 :**

```
1 2 4 5 3 -1 -1 -1 -1 -1 -1
```

**Sample Output 2 :**

```
5 2 3 1 4 
1 2 5 3 4 
5 3 2 4 1
```

**Explanation of Sample Output 2 :**

```
The given binary tree is shown below:
```

![BT - 5](https://files.codingninjas.in/tt5-6643.jpg)

```
Inorder traversal of given tree = [5, 2, 3, 1, 4]
Preorder traversal of given tree = [1, 2, 5, 3, 4]
Postorder traversal of given tree = [5, 3, 2, 4, 1]
```

**Constraints :**

```
1 <= 'N' <= 10^5
0 <= 'data' <= 10^5     

where 'N' is the number of nodes and 'data' denotes the node value of the binary tree nodes.

Time limit: 1 sec
```



```java
import java.util.List;
import java.util.ArrayList;
public class Solution {
    public static List<Integer> inOrder(TreeNode node,List<Integer> li){
        if(node==null)return li;
        inOrder(node.left,li);
        li.add(node.data);
        inOrder(node.right,li);
        return li;
    }
    public static List<Integer> preOrder(TreeNode node,List<Integer> li){
        if(node==null)return li;
        li.add(node.data);
        preOrder(node.left,li);
        preOrder(node.right,li);
        return li;
    }
    public static List<Integer> postOrder(TreeNode node,List<Integer> li){
        if(node==null)return li;
        postOrder(node.left,li);
        postOrder(node.right,li);
        li.add(node.data);
        return li;
    }
    public static List<List<Integer>> getTreeTraversal(TreeNode root) {
        // Write your code here.
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(inOrder(root,new ArrayList<>()));
        ans.add(preOrder(root,new ArrayList<>()));
        ans.add(postOrder(root,new ArrayList<>()));
        return ans;
    }
}
```



# To do pre-order , in-order, post-order in Single Traversal

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
        List<List<Integer>> ans = new ArrayList<>(Arrays.asList(inOrder,preOrder,postOrder));
        return ans;
    }
}
```