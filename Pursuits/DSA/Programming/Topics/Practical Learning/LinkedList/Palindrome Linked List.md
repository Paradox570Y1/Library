[234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

Given the `head` of a singly linked list, return `true` _if it is a_ 

_palindrome_

 _or_ `false` _otherwise_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

**Input:** head = [1,2,2,1]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

**Input:** head = [1,2]
**Output:** false

**Constraints:**

- The number of nodes in the list is in the range `[1, 105]`.
- `0 <= Node.val <= 9`


# Brute

TC->O(N)
SC->O(N)
```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        Stack<Integer> st = new Stack<>();
        ListNode temp = head;
        st.push(temp.val);
        while(temp.next != null){
            temp = temp.next;
            st.push(temp.val);
        }
        temp = head;
        if(st.pop() != temp.val)return false;
        while(temp.next!=null){
            temp = temp.next;
            if(temp.val != st.pop())return false;
        }
        return true;
    }
}
```


# Optimal

TC-> O(N)
SC->O(1)
```java
class Solution {
    ListNode reverse(ListNode head){
        ListNode prev = null;
        while (head != null) {
            ListNode nextNode = head.next; 
            head.next = prev;         
            prev = head;                  
            head = nextNode;              
        }
        return prev;
    }
    public boolean isPalindrome(ListNode head) {
        ListNode mid = head;
        ListNode fast = head;
        while(fast!=null && fast.next!=null){
            fast = fast.next.next;
            mid = mid.next;
        }
        ListNode newHead = reverse(mid);
        while(newHead!=null){
            if(head.val != newHead.val){
                reverse(newHead); //reversing the linked list back to original
                return false;
            }
            head = head.next;
            newHead = newHead.next;
        }
        reverse(newHead);
        return true;
    }
}
```