[Link](https://www.geeksforgeeks.org/problems/top-view-of-binary-tree/1)

Difficulty: **Medium**Accuracy: **38.43%**Submissions: **370K+**Points: **4**Average Time: **45m**

You are given a binary tree, and your task is to return its **top view**. The top view of a binary tree is the set of nodes visible when the tree is viewed from the top.

**Note:** 

- Return the nodes from the leftmost node to the rightmost node.
- If two nodes are at the same position (horizontal distance) and are outside the shadow of the tree, consider the leftmost node only. 

**Examples:**

**Input:** root[] = [1, 2, 3]   
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700490/Web/Other/blobid0_1733898095.png)   
**Output:** [2, 1, 3]

**Input:** root[] = [10, 20, 30, 40, 60, 90, 100]  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700490/Web/Other/blobid1_1733898122.png)   
**Output:** [40, 20, 10, 30, 100]  
**Explanation:** The root 10 is visible.
On the left, 40 is the leftmost node and visible, followed by 20.
On the right, 30 and 100 are visible. Thus, the top view is 40 20 10 30 100.

**Input:** root[] = [1, 2, 3, N, 4, N, N, N, 5, N, 6]
       1
     /   \
    2     3
     \   
      4
       \
        5
         \
          6
**Output:** [2, 1, 3, 6]  
**Explanation:** Node 1 is the root and visible.
Node 2 is the left child and visible from the left side.
Node 3 is the right child and visible from the right side.
Nodes 4, 5, and 6 are vertically aligned, but only the lowest node 6 is visible from the top view. Thus, the top view is 2 1 3 6.

**Constraints:**  
1 ≤ number of nodes ≤ 105  
1 ≤ node->data ≤ 105


# Using BSF

```java
class Solution {
    // Function to return a list of nodes visible from the top view
    // from left to right in Binary Tree.
    static class Element{
        int id;
        Node node;
        Element(Node node,int id){
            this.node = node;
            this.id = id;
        }
    }
    static ArrayList<Integer> topView(Node root) {
        // code here
        ArrayList<Integer> ansL = new ArrayList<>();
        ArrayList<Integer> ansR = new ArrayList<>();
        Queue<Element> q = new LinkedList<>();
        q.offer(new Element(root,0));
        int left=-1,right = 0;
        while(!q.isEmpty()){
            int size = q.size();
            for(int i=0;i<size;i++){
                Element cur = q.poll();
                if(cur.id== left){
                    ansL.add(cur.node.data);left--;
                }
                else if(cur.id == right){
                    ansR.add(cur.node.data);right++;
                }
                if(cur.node.left!=null)q.offer(new Element(cur.node.left,cur.id-1));
                if(cur.node.right!=null)q.offer(new Element(cur.node.right,cur.id+1));
            }
        }
        int i=0,j=ansL.size()-1;
        while(i<j){
            int temp = ansL.get(i);
            ansL.set(i,ansL.get(j));
            ansL.set(j,temp);
            i++;j--;
        }
        for(int k=0;k<ansR.size();k++){
            ansL.add(ansR.get(k));
        }
        return ansL;
    }
}
```


# Using DFS and LinkedList

```java
class Solution {
    private static LinkedList<Integer> lvl = new LinkedList<>();
    private static LinkedList<Integer> list = new LinkedList<>();
    private static int neg=-1;
    private static int pos=0;
    static ArrayList<Integer> topView(Node root) {
        // code here
        neg=-1;
        pos=0;
        lvl = new LinkedList<>();
        list = new LinkedList<>();
        dfs(root,0,0);
        ArrayList<Integer> ans = new ArrayList<>();
        for(int i=0;i<list.size();i++){
            ans.add(list.get(i));
        }
        return ans;
    }
    static void dfs(Node root,int level,int i){
        if(root==null)return;
        if(i==pos){
            list.add(root.data);
            lvl.add(level);
            pos++;
        }
        else if(i==neg){
            list.addFirst(root.data);
            lvl.addFirst(level);
            neg--;
        }
        else {
            int index = -(neg+1)+i;
            if(lvl.get(index)>level){
                list.set(index,root.data);
                lvl.set(index,level);
            }
        }
        dfs(root.left,level+1,i-1);
        dfs(root.right,level+1,i+1);
    }
}
```

# Using TreeMap 
Easier implementation

```java
class Solution {
    static class Element{
        int pos;
        Node node;
        Element(Node node,int pos){
            this.node = node;
            this.pos = pos;
        }
    }
    static ArrayList<Integer> topView(Node root) {
        // code here
        TreeMap<Integer,Integer> tree =new TreeMap<>();
        Queue<Element> q = new LinkedList<>();
        q.offer(new Element(root,0));
        while(!q.isEmpty()){
            Element cur = q.poll();
            if(!tree.containsKey(cur.pos)){
                tree.put(cur.pos,cur.node.data);
            }
            if(cur.node.left!=null)q.offer(new Element(cur.node.left,cur.pos-1));
            if(cur.node.right!=null)q.offer(new Element(cur.node.right,cur.pos+1));
        }
        return new ArrayList<>(tree.values());
    }
}
```