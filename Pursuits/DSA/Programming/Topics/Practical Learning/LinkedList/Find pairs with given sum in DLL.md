### Find pairs with given sum in doubly linked list
[Link](https://www.geeksforgeeks.org/problems/find-pairs-with-given-sum-in-doubly-linked-list/1)
Difficulty: **Easy**Accuracy: **66.01%**Submissions: **63K+**Points: **2**

Given a sorted doubly linked list of positive distinct elements, the task is to find pairs in a doubly-linked list whose sum is equal to given value **target**.

**Example 1:**

**Input:**  
1 <-> 2 <-> 4 <-> 5 <-> 6 <-> 8 <-> 9
target = 7
**Output:** (1, 6), (2,5)
**Explanation:** We can see that there are two pairs 
(1, 6) and (2,5) with sum 7.

**Example 2:**

**Input:** 
1 <-> 5 <-> 6
target = 6
**Output:** (1,5)
**Explanation:** We can see that there is one pairs  (1, 5) with sum 6.

**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **findPairsWithGivenSum()** which takes head node of the doubly linked list and an integer target as input parameter and returns an array of pairs. If there is no such pair return empty array.

**Expected Time Complexity:** O(N)  
**Expected Auxiliary Space:** O(1)  
**Constraints:**  
1 <= N <= 105  
1 <= target <= 105



# Optimal

TC-> O(2N)
SC-> O(1)

```java
class Solution {
    public static ArrayList<ArrayList<Integer>> findPairsWithGivenSum(int target, Node head) {
        // code here
        if(head==null)return null;
        Node left = head;
        Node right = head;
        ArrayList<ArrayList<Integer>> li = new ArrayList<>();
        while(right.data<target && right.next!=null) right = right.next;
        while(left != right && right.next != left){
            int a = left.data,b = right.data;
            if(a+b>target)right = right.prev;
            else if(a+b<target)left = left.next;
            else{
                li.add(new ArrayList<>(List.of(a,b)));
                left = left.next;
                right = right.prev;
            }
        }   
        return li;
    }
}
```