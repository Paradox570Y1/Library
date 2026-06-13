[445. Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/)

You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/04/09/sumii-linked-list.jpg)

**Input:** l1 = [7,2,4,3], l2 = [5,6,4]
**Output:** [7,8,0,7]

**Example 2:**

**Input:** l1 = [2,4,3], l2 = [5,6,4]
**Output:** [8,0,7]

**Example 3:**

**Input:** l1 = [0], l2 = [0]
**Output:** [0]

**Constraints:**

- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.

# Brute

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
    ListNode reverseLL(ListNode head){
        
        ListNode prev = null;
        while(head.next!=null){
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        head.next = prev;
        return head;
    }
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head1 = reverseLL(l1);
        ListNode head2 = reverseLL(l2);
        ListNode ans = new ListNode(-1);
        ListNode temp = ans;
        int carry=0;
        while(head1!=null && head2!=null){
            int sum = carry;
            sum+=head1.val;
            sum+=head2.val;
            temp.next = new ListNode(sum%10);
            carry = sum/10;
            head1 = head1.next;
            head2 = head2.next;
            temp = temp.next;
        }
        if(head1==null && head2==null){
            if(carry==1)temp.next = new ListNode(1);
            return reverseLL(ans.next);
        }
        if(head1==null){
            while(head2!=null){
                int sum = carry;
                sum+=head2.val;
                temp.next = new ListNode(sum%10);
                carry = sum/10;
                head2 = head2.next;
                temp = temp.next;
            }
        }
        else if(head2==null){
            while(head1!=null){
                int sum = carry;
                sum+=head1.val;
                temp.next = new ListNode(sum%10);
                carry = sum/10;
                head1 = head1.next;
                temp = temp.next;
            }
        }
        if(carry==1)temp.next = new ListNode(1);
        return reverseLL(ans.next);
    }
}
```