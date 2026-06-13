[Link](https://www.geeksforgeeks.org/problems/burning-tree/1)

> Similar Question: [2385. Amount of Time for Binary Tree to Be Infected](https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected/)

Given a binary tree and a **node data** called **target**. Find the minimum time required to burn the complete binary tree if the target is set on fire. It is known that in 1 second all nodes connected to a given node get burned. That is its left child, right child, and parent.  
**Note:** The tree contains unique values.

**Examples :** 

**Input:** root[] = [1,2,3,4,5,N,6,N,N,7,8,N,9,N,N,N,N,N,10],  target = 8  **![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/702131/Web/Other/blobid0_1733996113.jpg)**  
**Output:** 7
**Explanation:** If leaf with the value 8 is set on fire. 
After 1 sec: 5 catches fire.  
After 2 sec: 2, 7 catches fire.  
After 3 sec: 4, 1 catches fire.  
After 4 sec: 3 catches fire.  
After 5 sec: 6 catches fire.  
After 6 sec: 9 catches fire.  
After 7 sec: 10 catches fire.  
It takes 7s to burn the complete tree.

**Input:** root[] = [1, 2, 3, 4, 5, N, 7, 8, N, 10], target = 10  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/702131/Web/Other/blobid0_1735037594.webp)
**Output:** 5**Explanation****:** If leaf with the value 10 is set on fire. - After 1 sec: Node 5 catches fire.
- After 2 sec: Node 2 catches fire.
- After 3 sec: Nodes 1 and 4 catches fire.
- After 4 sec: Node 3 and 8 catches fire.
- After 5 sec: Node 7 catches fire.
It takes 5s to burn the complete tree.

**Constraints:**  
1 ≤ number of nodes ≤ 105  
1 ≤ node->data ≤ 105

# Another approach is to store parent of each node and traverse in three directions from the point of infection 
# Using Level Order Traversal ( BFS)

```java
class Solution {
    public static int minTime(Node root, int target) {
        // code here
        HashMap<Integer,Node> Parent = new HashMap<>();
        HashSet<Integer> visited = new HashSet<>();
        Queue<Node> q = new LinkedList<>();
        q.offer(root);
        Node targetNode = null;
        while(!q.isEmpty()){
            Node cur = q.poll();
            if(cur.data == target)targetNode = cur;
            if(cur.left!=null){
                q.offer(cur.left);
                Parent.put(cur.left.data,cur);
            }
            if(cur.right!=null){
                q.offer(cur.right);
                Parent.put(cur.right.data,cur);
            }
        }
        q.offer(targetNode);
        int cnt=-1;
        while(!q.isEmpty()){
            cnt++;
            int n = q.size();
            for(int i=0;i<n;i++){
                Node cur = q.poll();
                visited.add(cur.data);
                if(cur!=root && !visited.contains(Parent.get(cur.data).data)){
                    q.offer(Parent.get(cur.data));
                }
                if(cur.left!=null && !visited.contains(cur.left.data)){
                    q.offer(cur.left);
                }
                if(cur.right!=null && !visited.contains(cur.right.data)){
                    q.offer(cur.right);
                }
            }
        }
        return cnt;
    }
}
```


# Using dfs

```java
class Solution {
    private static HashMap<Integer,Integer> map = new HashMap<>();
    private static int ans=0;
    private static void dfs(Node node,int cnt){
        if(node==null)return;
        cnt = map.getOrDefault(node.data,cnt);
        ans = Math.max(cnt,ans);
        dfs(node.left,cnt+1);
        dfs(node.right,cnt+1);
    }
    private static int locate(Node node,int target){
        if(node==null)return -1;
        if(node.data == target){
            map.put(target,0);
            return 0;
        }
        int left = locate(node.left,target);
        if(left>=0){
            map.put(node.data,left+1);
            return left+1;
        }
        int right = locate(node.right,target);
        if(right>=0){
            map.put(node.data,right+1);
            return right+1;
        }
        return -1;
    }
    public static int minTime(Node root, int target) {
        // code here
        ans=0;
        map = new HashMap<>();
        locate(root,target);
        dfs(root,0);
        return ans;
    }
}
```