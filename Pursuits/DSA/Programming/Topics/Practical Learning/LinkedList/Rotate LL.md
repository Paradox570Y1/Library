[61. Rotate List](https://leetcode.com/problems/rotate-list/)

Given the `head` of a linked list, rotate the list to the right by `k` places.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

**Input:** head = [1,2,3,4,5], k = 2
**Output:** [4,5,1,2,3]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

**Input:** head = [0,1,2], k = 4
**Output:** [2,0,1]

**Constraints:**

- The number of nodes in the list is in the range `[0, 500]`.
- `-100 <= Node.val <= 100`
- `0 <= k <= 2 * 109`

# Optimal

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head==null)return null;
        int cnt=0;
        ListNode temp = head;
        ListNode end = head;
        while(temp!=null){
            cnt++;
            if(temp.next==null)end = temp;
            temp=temp.next;
        }
        k %= cnt;
        cnt = cnt-k;
        temp = head;
        while(cnt-->1 && temp!=null){
            temp = temp.next;
        }
        end.next = head;
        if(temp.next!=null)head = temp.next;
        temp.next = null;
        return head;
    }
}
```

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head==null)return null;
        int cnt=0;
        ListNode temp = head;
        ListNode end = head;
        while(temp!=null){
            cnt++;
            if(temp.next==null)end = temp;
            temp=temp.next;
        }
        k %= cnt;
        cnt = cnt-k;
        temp = head;
        while(cnt-->1 && temp!=null){
            temp = temp.next;
        }
        ListNode breakPoint= temp;
        if(temp.next!=null)temp = temp.next;
        else return head;
        end.next = head;
        breakPoint.next = null;
        return temp;
    }
}
```

or

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head==null)return null;
        ListNode p1 = head;
        int cnt=0;
        while(p1!=null){
            cnt++;
            p1=p1.next;
        }
        p1 = head;
        k %= cnt;
        if(k==0)return head;
        int i=0;
        while(p1!=null && i<k){
            p1 = p1.next;
            i++;
        }
        ListNode trav =  head;
        while(p1!=null && p1.next!=null){
            trav = trav.next;
            p1 = p1.next;
        }
        ListNode newHead = trav.next;
        trav.next =null;
        p1.next = head;
        return newHead;
    }
}
```

OR

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head==null)return null;
        ListNode p1 = head;
        int cnt=1;
        while(p1.next!=null){
            cnt++;
            p1=p1.next;
        }
        k %= cnt;
        if(k==0)return head;
        cnt= cnt-k-1;
        ListNode trav =  head;
        while(cnt>0){
            trav = trav.next;
            cnt--;
        }
        ListNode newHead = trav.next;
        trav.next =null;
        p1.next = head;
        return newHead;
    }
}
```