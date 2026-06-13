[25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

**Input:** head = [1,2,3,4,5], k = 2
**Output:** [2,1,4,3,5]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

**Input:** head = [1,2,3,4,5], k = 3
**Output:** [3,2,1,4,5]

**Constraints:**

- The number of nodes in the list is `n`.
- `1 <= k <= n <= 5000`
- `0 <= Node.val <= 1000`

# Optimal

Striver's
```java
static Node reverseLinkedList(Node head) {
        Node temp = head;  
       Node prev = null;  
       while(temp != null){  
           Node front = temp.next;  
           temp.next = prev;  
           prev = temp;  
           temp = front; 
       }
       return prev;  
    }

    static Node getKthNode(Node temp, int k) {
        k -= 1;
        while (temp != null && k > 0) {
            k--;
            temp = temp.next;
        }
        return temp;
    }

    // Function to reverse nodes in groups of K
    static Node kReverse(Node head, int k) {
        Node temp = head;
        Node prevLast = null;
        while (temp != null) {
            Node kThNode = getKthNode(temp, k);
            if (kThNode == null) {
                if (prevLast != null) {
                    prevLast.next = temp;
                }
                break;
            }
            
            Node nextNode = kThNode.next;
            kThNode.next = null;
            reverseLinkedList(temp);
            if (temp == head) {
                head = kThNode;
            } else {
                prevLast.next = kThNode;
            }
            prevLast = temp;
            temp = nextNode;
        }
        return head;
    }
```
Mine approach
```java
class Solution {
    public void reverse(ListNode head,ListNode tail){
        if(head==tail)return;
        reverse(head.next,tail);
        ListNode front = head.next;
        front.next = head;
        head.next = null;
    }
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode i = head;
        ListNode tempHead = head;
        ListNode newHead=head;
        ListNode start=null;
        int cnt=1;
        while(i!=null){
            if(cnt==k){
                ListNode front = i.next;
                if(tempHead==head)newHead = i;
                reverse(tempHead,i);
                if(start!=null)start.next = i;
                tempHead.next = front;
                i=tempHead;
                start=i;
                tempHead = tempHead.next;
                cnt=0;
            }
            i = i.next;
            cnt++;
        }
        return newHead;
    }
}
```

```java
class Solution {
    void reverse(ListNode head,ListNode tail){
        ListNode prev = null;
        ListNode temp = head;
        while(temp!=tail){
            ListNode front = temp.next;
            temp.next = prev;
            prev = temp;
            temp = front;
        }
    }
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode temp = head;
        ListNode start = null;
        ListNode tempHead = head;
        ListNode newHead = head;
        int cnt=1;
        while(temp!=null){
            if(cnt==k){
                ListNode front = temp.next;
                reverse(tempHead,temp.next);
                if(start==null)newHead = temp;
                else start.next =temp;
                tempHead.next =front;
                temp = tempHead;
                start = tempHead;
                tempHead = front;
                cnt=0;
            }
            temp = temp.next;
            cnt++;
        }
        return newHead;
    }
}
```


OR

Latest

```java
class Solution {
    private void reverse(ListNode head,int k){
        ListNode prev = null;
        ListNode trav = head;
        int i=0;
        while(trav!=null && i<k){
            ListNode next = trav.next;
            trav.next = prev;
            prev = trav;
            trav = next;
            i++;
        }
    }
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode p = head;
        ListNode prev = null;
        int i=0;
        while(p!=null && i<k){
            prev = p;
            p = p.next;
            i++;
        }
        if(i<k)return head;
        ListNode newNext = reverseKGroup(p,k);
        reverse(head,k);
        head.next = newNext;
        return prev;
    }
}
```

OR

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
    private void reverse(ListNode head){
        ListNode prev = null;
        ListNode trav = head;
        while(trav!=null){
            ListNode next = trav.next;
            trav.next = prev;
            prev = trav;
            trav = next;
        }
    }
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode p = head;
        ListNode prev = null;
        int i=0;
        while(p!=null && i<k){
            prev = p;
            p = p.next;
            i++;
        }
        if(i<k)return head;
        ListNode newNext = reverseKGroup(p,k);
        prev.next = null;
        reverse(head);
        head.next = newNext;
        return prev;
    }
}
```


OR

```java
class Solution {
    private ListNode reverseGroup(ListNode node, ListNode limitNode) {
        if (node == limitNode) return node;
        ListNode newHead = reverseGroup(node.next, limitNode);
        ListNode front = node.next;
        front.next = node;
        node.next = null;
        return newHead;
    }
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode trav = head;
        ListNode prev = null;
        int c = 1;
        ListNode newHead = head;
        while(trav != null && c < k) {
            c++;
            trav = trav.next;
        }
        newHead = trav;
        trav = head;
        c = 0;
        while (trav != null) {
            ListNode curGroup = trav;
            ListNode lastNode = null;
            while (trav != null && c < k) {
                lastNode = trav;
                trav = trav.next;
                c++;
            }
            if (c != k) break;
            ListNode nextGroup = trav;
            ListNode revGroup = reverseGroup(curGroup, lastNode);
            curGroup.next = nextGroup;
            if (prev != null) prev.next = revGroup;
            prev = curGroup;
            c = 0;
        }
        return newHead;
    }
}
```