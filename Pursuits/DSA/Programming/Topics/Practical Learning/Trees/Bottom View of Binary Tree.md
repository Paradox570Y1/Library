[Link](https://www.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1)
Given a binary **tree**, return an array where elements represent the bottom view of the binary tree from left to right.

Note: If there are **multiple** bottom-most nodes for a horizontal distance from the root, then the **latter** one in the level traversal is considered. For example, in the below diagram, 3 and 4 are both the bottommost nodes at a horizontal distance of 0, here **4** will be considered.

                      20  
                    /    \  
                  8       22  
                /   \     /   \  
              5      3 4     25  
                     /    \        
                 10       14

For the above tree, the output should be 5 10 **4** 14 25.

**Examples :**

**Input:
**       1
     /   \
    3     2
**Output:** 3 1 2
**Explanation:** First case represents a tree with 3 nodes and 2 edges where root is 1, left child of 1 is 3 and right child of 1 is 2.
![](https://contribute.geeksforgeeks.org/wp-content/uploads/BT-1.jpg)
Thus bottom view of the binary tree will be 3 1 2.

**Input:
**         10
       /    \
      20    30
     /  \
    40   60
**Output:** 40 20 60 30

**Input:
**        1
       /   
      2
**Output:** 2 1

**Constraints:**  
1 <= number of nodes <= 105  
1 <= node->data <= 105


# Using TreeMap

```java
class Solution
{
    //Function to return a list containing the bottom view of the giv
    class Pair{
        int col;
        Node node;
        Pair(Node node,int col){
            this.node = node;
            this.col = col;
        }
    }
    public ArrayList <Integer> bottomView(Node root)
    {
        // Code here
        TreeMap<Integer,Integer> tree = new TreeMap<>();
        Queue<Pair> q = new LinkedList<Pair>();
        q.offer(new Pair(root,0));
        while(!q.isEmpty()){
            Pair cur = q.poll();
            tree.put(cur.col,cur.node.data);
            if(cur.node.left!=null)q.offer(new Pair(cur.node.left,cur.col-1));
            if(cur.node.right!=null)q.offer(new Pair(cur.node.right,cur.col+1));
        }
        return new ArrayList<>(tree.values());
    }
}
```


# Using BFS with TreeMap

```java
class Solution
{
    //Function to return a list containing the bottom view of the giv
    class Pair{
        int col;
        Node node;
        Pair(Node node,int col){
            this.node = node;
            this.col = col;
        }
    }
    public ArrayList <Integer> bottomView(Node root)
    {
        // Code here
        ArrayList<Integer> ansL = new ArrayList<>();
        ArrayList<Integer> ansR = new ArrayList<>();
        int pos=0,neg=-1;
        Queue<Pair> q = new LinkedList<Pair>();
        q.offer(new Pair(root,0));
        while(!q.isEmpty()){
            int size = q.size();
            for(int i=0;i<size;i++){
                Pair cur = q.poll();
                if(pos==cur.col){
                    ansR.add(cur.node.data);pos++;
                }
                else if(neg == cur.col){
                    ansL.add(cur.node.data);neg--;
                }
                else{
                    if(cur.col<0){
                        ansL.set(-cur.col-1,cur.node.data);
                    }
                    else{
                        ansR.set(cur.col,cur.node.data);
                    }
                }
                if(cur.node.left!=null)q.offer(new Pair(cur.node.left,cur.col-1));
                if(cur.node.right!=null)q.offer(new Pair(cur.node.right,cur.col+1));
            }
        }
        int n = ansL.size();
        for(int i=0;i<n/2;i++){
            int j= n-i-1;
            int temp = ansL.get(i);
            ansL.set(i,ansL.get(j));
            ansL.set(j,temp);
        }
        n= ansR.size();
        for(int i=0;i<n;i++){
            ansL.add(ansR.get(i));
        }
        return ansL;
    }
}
```

# Using DFS

```java
class Solution
{
    //Function to return a list containing the bottom view of the given tree.
    private LinkedList<Integer> list = new LinkedList<>();
    private LinkedList<Integer> lvl = new LinkedList<>();
    private int pos=0,neg=-1;
    public ArrayList <Integer> bottomView(Node root)
    {
        // Code her
        dfs(root,0,0);
        return new ArrayList<>(list);
    }
    private void dfs(Node node,int level,int idx){
        if(node==null)return;
        if(idx<0){
            int index = -(neg+1)+idx;
            if(idx>neg && level>=lvl.get(index)){
                list.set(index,node.data);
                lvl.set(index,level);
            }
            else if(idx==neg){
                list.addFirst(node.data);
                lvl.addFirst(level);
                neg--;
            }
        }
        else{
            int index = -(neg+1)+idx;
            if(idx<pos && level>=lvl.get(index)){
                list.set(index,node.data);
                lvl.set(index,level);
            }
            else if(idx==pos){
                list.add(node.data);
                lvl.add(level);
                pos++;
            }
        }
        dfs(node.left,level+1,idx-1);
        dfs(node.right,level+1,idx+1);
    }
}
```