[876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)
Given the `head` of a singly linked list, return _the middle node of the linked list_.

If there are two middle nodes, return **the second middle** node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [3,4,5]
**Explanation:** The middle node of the list is node 3.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

**Input:** head = [1,2,3,4,5,6]
**Output:** [4,5,6]
**Explanation:** Since the list has two middle nodes with values 3 and 4, we return the second one.

**Constraints:**

- The number of nodes in the list is in the range `[1, 100]`.
- `1 <= Node.val <= 100`


# Brute
```java
public class FindMiddleOfLinkedList {
    static Node findMiddle(Node head) {
        if (head == null || head.next == null) {
            return head;
        }
        Node temp = head;
        int count = 0;
        
        while (temp != null) {
            count++;
            temp = temp.next;
        }

        int mid = count / 2 + 1;
        temp = head;

        while (temp != null) {
            mid = mid - 1;
            if (mid == 0){
                break;
            }
            temp = temp.next;
        }
        return temp;
    }
```

# Optimal

Using tortoise and Hare algorithm
```java
public class FindMiddleOfLinkedList {
    static Node findMiddle(Node head) {
        Node slow = head; 
        Node fast = head;   
        while (fast != null && fast.next != null && slow != null) {
            fast = fast.next.next;  
            slow = slow.next;        
        }
        return slow;  
    }
```

My approach
```java
class Solution {
    public ListNode middleNode(ListNode head) {
        if(head.next == null)return head;
        ListNode temp = head;
        temp = temp.next;
        ListNode middle = temp;
        int cnt=2;
        int nodePos = 2;
        int diff =0;
        while(temp.next!=null){
            cnt++;
            if(cnt%2==1)diff++;
            if(cnt-diff != nodePos){
                nodePos++;
                middle = middle.next;
            }
            temp = temp.next;
        }
        return middle;
    }
}
```