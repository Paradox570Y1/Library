[1721. Swapping Nodes in a Linked List](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/)
You are given the `head` of a linked list, and an integer `k`.

Return _the head of the linked list after **swapping** the values of the_ `kth` _node from the beginning and the_ `kth` _node from the end (the list is **1-indexed**)._

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/21/linked1.jpg)

**Input:** head = [1,2,3,4,5], k = 2
**Output:** [1,4,3,2,5]

**Example 2:**

**Input:** head = [7,9,6,6,7,8,3,0,9,5], k = 5
**Output:** [7,9,6,6,8,7,3,0,9,5]

**Constraints:**

- The number of nodes in the list is `n`.
- `1 <= k <= n <= 105`
- `0 <= Node.val <= 100`


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode swapNodes(ListNode head, int k) {
        ListNode temp = head;
        int len=0;
        while(temp!=null){
            temp=temp.next;
            len++;
        }
        int t = len-k+1;
        temp = head;
        int cnt=1;
        ListNode p1=null,p2=null;
        while(temp!=null){
            if(cnt==k)p1=temp;
            if(cnt==t)p2=temp;
            if(p1!= null && p2!=null)break;
            temp = temp.next;
            cnt++;
        }
        int swap = p1.val;
        p1.val = p2.val;
        p2.val = swap;
        return head;
    }
}
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode swapNodes(ListNode head, int k) {
        ListNode i,j,l;
        i= j = l =head;
        int c=1;
        while(c<k){
            j=j.next;
            l=l.next;
            c++;
        }
        while(j.next!=null){
            j=j.next;
            i=i.next;
        }
        int temp = i.val;
        i.val=l.val;
        l.val = temp;
        return head;
    }
}
```

# Optimal

```java
class Solution {
    public ListNode swapNodes(ListNode head, int k) {
        if (head == null || head.next == null) return head;
        ListNode i,j,l;
        i= j = l =head;
        for(int t=1;t<k;t++){
            j=j.next;
        }
        l=j;
        while(j.next!=null){
            j=j.next;
            i=i.next;
        }
        int temp = i.val;
        i.val=l.val;
        l.val = temp;
        return head;
    }
}
```