[148. Sort List](https://leetcode.com/problems/sort-list/)
Given the `head` of a linked list, return _the list after sorting it in **ascending order**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

**Input:** head = [4,2,1,3]
**Output:** [1,2,3,4]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

**Input:** head = [-1,5,3,4,0]
**Output:** [-1,0,3,4,5]

**Example 3:**

**Input:** head = []
**Output:** []

**Constraints:**

- The number of nodes in the list is in the range `[0, 5 * 104]`.
- `-105 <= Node.val <= 105`



# Optimal
TC -> O( (n/2+n)* log n)  as it takes n/2 time to find middle element
SC -> O(1)
```java
class Solution {
    ListNode findMiddle(ListNode head){
        if (head == null || head.next == null) {
        return head;
    }
        ListNode slow = head;
        ListNode fast = head.next;
        while(fast!=null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
    ListNode merge(ListNode leftHead,ListNode rightHead){
        ListNode head = new ListNode(-1);
        ListNode temp = head;
        while(leftHead!= null && rightHead != null){
            if(leftHead.val < rightHead.val){
                temp.next = leftHead;
                leftHead = leftHead.next;
                temp = temp.next;
            }
            else{
                temp.next = rightHead;
                rightHead = rightHead.next;
                temp = temp.next;
            }
        }
        if(leftHead!=null)temp.next = leftHead;
        else temp.next = rightHead;
        return head.next;
    }
    ListNode mergeSort(ListNode head){
        if(head == null || head.next == null)return head;
        ListNode middle = findMiddle(head);
        ListNode leftHead = head,rightHead = middle.next;
        middle.next = null;
        leftHead = mergeSort(leftHead);
        rightHead = mergeSort(rightHead);
        return merge(leftHead,rightHead);
    }
    public ListNode sortList(ListNode head) {
        return mergeSort(head);
    }
}
```