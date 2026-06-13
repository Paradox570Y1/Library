[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

**Input:** l1 = [2,4,3], l2 = [5,6,4]
**Output:** [7,0,8]
**Explanation:** 342 + 465 = 807.

**Example 2:**

**Input:** l1 = [0], l2 = [0]
**Output:** [0]

**Example 3:**

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
**Output:** [8,9,9,9,0,0,0,1]

**Constraints:**

- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.


# Optimal


TC-> O(max(m,n))
SC-> O(max(m,n))

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode p1 = l1;
        ListNode p2 = l2;
        ListNode ans = new ListNode(-1);
        ListNode trav = ans;
        int c=0;
        while(p1!=null && p2!=null){
            trav.next = new ListNode((p1.val + p2.val+c)%10);
            c = (p1.val+p2.val+c)/10;
            trav = trav.next;
            p1=p1.next;
            p2=p2.next;
        }
        if(p1==null && p2==null){
            if(c==1)trav.next = new ListNode(1);
            return ans.next;
        }
        else if(p1==null){
            while(p2!=null){
                trav.next = new ListNode((p2.val+c)%10);
                c = (p2.val+c)/10;
                trav = trav.next;
                p2 = p2.next;
            }
        }
        else{
            while(p1!=null){
                trav.next = new ListNode((p1.val+c)%10);
                c = (p1.val+c)/10;
                trav = trav.next;
                p1 = p1.next;
            }
        }
        if(c==1)trav.next = new ListNode(1);
        return ans.next;
    }
}
```

OR (better readability)

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode p1 = l1;
        ListNode p2 = l2;
        int carry=0;
        ListNode ans=new ListNode(-1);
        ListNode temp = ans;
        while(p1!=null || p2!=null){
            int sum = carry;
            if(p1!=null)sum+=p1.val;
            if(p2!=null)sum+=p2.val;
            temp.next = new ListNode(sum%10);
            carry=sum/10;
            temp = temp.next;
            if(p1!=null)p1 = p1.next;
            if(p2!=null)p2 = p2.next;
        }
        if(carry==1)temp.next = new ListNode(1);
        return ans.next;
    }
}
```

Implementing it without using space for storing answer makes the code messier
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode p1 = l1;
        ListNode p2 = l2;
        int carry=0;
        ListNode temp=new ListNode(-1);
        while(p1!=null && p2!=null){
            p1.val+=(p2.val+carry);
            if(p1.val>=10){
                p1.val%=10;
                carry=1;
            }
            else carry=0;
            temp.next=p1;
            p1 = p1.next;
            p2 = p2.next;
        }
        
        if(p1 ==p2){
            if(carry==1) temp.next.next = new ListNode(1);
        }
       else if(p2==null){
        while(p1!=null){
            p1.val+=carry;
            if(p1.val>=10){
                p1.val%=10;
                carry=1;
            }
            else carry=0;
            temp=p1;
            p1 = p1.next;
        }
        if(carry==1)temp.next = new ListNode(1);
       }
       else if(p1==null){
            temp.next.next=p2;
            while(p2!=null){
                p2.val+=carry;
                if(p2.val>=10){
                    p2.val%=10;
                    carry=1;
                }   
                else carry=0;
                temp=p2;
                p2 = p2.next;
            }
            if(carry==1)temp.next = new ListNode(1);
       }
       return l1;
    }
}
```