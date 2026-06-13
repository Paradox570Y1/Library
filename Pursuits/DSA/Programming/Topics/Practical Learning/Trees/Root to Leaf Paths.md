[Link](https://www.geeksforgeeks.org/problems/root-to-leaf-paths/1)

Difficulty: **Medium**Accuracy: **43.65%**Submissions: **136K+**Points: **4**Average Time: **30m**

Given a **Binary Tree**, you need to **find all the possible paths** from the **root node** to all the **leaf nodes** of the binary tree.

**Note:** The paths should be returned such that paths from the left subtree of any node are listed first, followed by paths from the right subtree.

**Examples:**

**Input:** root[] = [1, 2, 3, 4, 5]
![ex-3](https://media.geeksforgeeks.org/wp-content/uploads/20241007105251989873/ex-3.webp)
**Output:** [[1, 2, 4], [1, 2, 5], [1, 3]] 
**Explanation:** All possible paths: 1->2->4, 1->2->5 and 1->3

**Input:** root[] = [1, 2, 3]
       1
    /     \
   2       3
**Output:** [[1, 2], [1, 3]] 
**Explanation:** All possible paths: 1->2 and 1->3

**Input:** root[] = [10, 20, 30, 40, 60]
         10
       /    \
      20    30
     /  \
    40   60
**Output:** [[10, 20, 40], [10, 20, 60], [10, 30]]  
**Explanation:** All possible paths: 10->20 ->40, 10->20->60 and 10->30

**Constraints:**  
1<=number of nodes<=104  
1<=node->data<=104

# Using dfs

```java
class Solution {
    public static ArrayList<ArrayList<Integer>> Paths(Node root) {
        // code here
        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
        dfs(root,ans,new ArrayList<>());
        return ans;
    }
    static void dfs(Node node,ArrayList<ArrayList<Integer>> ans,ArrayList<Integer> list){
        if(node==null)return;
        if(node.left == null && node.right==null){
            list.add(node.data);
            ans.add(new ArrayList<>(list));
            list.remove(list.size()-1);
            return;
        }
        
        list.add(node.data);
        dfs(node.left,ans,list);
        dfs(node.right,ans,list);
        list.remove(list.size()-1);
        
    }
}
```