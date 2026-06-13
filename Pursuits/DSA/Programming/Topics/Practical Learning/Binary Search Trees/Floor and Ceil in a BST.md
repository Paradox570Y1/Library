
To find floor
[Link](https://www.naukri.com/code360/problems/ceil-from-bst_920464?leftPanelTabValue=PROBLEM)
## Problem statement

Send feedback

Ninja is given a binary search tree and an integer. Now he is given a particular key in the tree and returns its ceil value. Can you help Ninja solve the problem?

**Note:**

```
Ceil of an integer is the closest integer greater than or equal to a given number.
For example:
arr[] = {1, 2, 5, 7, 8, 9}, key = 3.
The closest integer greater than 3 in the given array is 5. So, its ceil value in the given array is 5.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= T <= 10    
1 <= N <= 10^5
0 <= node data <= 10^9
1 <= X <= 10^9     

Time limit: 1 second
```



```java
public class Solution {

    public  static int findCeil(TreeNode<Integer> root, int x) {

        // Write your code here
        TreeNode<Integer> node = root;
        int ceil=-1;
        while(node!=null){
            if(node.data==x){
                return x;
            }
            else if(node.data<x){
                node=node.right;
            }
            else{
                if(node.data>x)ceil = node.data;
                node=node.left;
            }
        }
        return ceil;
    }
}
```


# To find both floor and ceil

Given a **root** of binary search tree and a **key**(node) value, find the floor and ceil value for that particular key value.

- **Floor** Value Node: Node with the greatest data lesser than or equal to the key value. 
- **Ceil** Value Node: Node with the smallest data larger than or equal to the key value.

If a particular floor or ceil value is not present then output -1.

Examples:

**Input :** root = [8, 4, 12, 2, 6, 10, 14] , key = 11

**Output :** [10, 12]

**Explanation :**

![](https://static.takeuforward.org/content/ProblemSetter-eDbjy9Um)

**Input :** root = [8, 4, 12, 2, 6, 10, 14] , key = 15

**Output :** [14, -1]

**Explanation :**


![](https://static.takeuforward.org/content/ProblemSetter-D00IL4KV)


```java
class Solution {
    public List<Integer> floorCeilOfBST(TreeNode root, int key) {
        //your code goes here
        TreeNode node = root;
        int floor=-1,ceil=-1;
        while(node!=null){
            if(node.data == key){
                return new ArrayList<>(List.of(key,key));
            }
            else if(node.data<key){
                floor=node.data;
                node = node.right;
            }
            else{
                ceil=node.data;
                node = node.left;
            }
        }
        return new ArrayList<>(List.of(floor,ceil));
    }
}
```


# Recursive way

```java
public class Solution {

    public  static int findCeil(TreeNode<Integer> node, int x) {

        // Write your code here
        return helper(node, x, -1);
    }
    private static int helper(TreeNode<Integer> node, int x, int ceil) {
        if(node == null) return ceil;
        if(node.data==x)return x;
        if(node.data < x) {
            return helper(node.right, x, ceil);
        }
        return helper(node.left, x, node.data);
    }
}
```