### Sort a linked list of 0s, 1s and 2s
[Link](https://www.geeksforgeeks.org/problems/given-a-linked-list-of-0s-1s-and-2s-sort-it/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=given-a-linked-list-of-0s-1s-and-2s-sort-it)
Difficulty: **Easy**Accuracy: **60.75%**Submissions: **214K+**Points: **2**

Given a linked list where nodes can contain values **0s**, **1s,** and **2s** only. The task is to segregate **0s**, **1s,** and **2s** linked list such that all zeros segregate to the head side, 2s at the end of the linked list, and 1s in the middle of 0s and 2s.

**Examples:**

**Input:** LinkedList: 1->2->2->1->2->0->2->2
**Output:** 0->1->1->2->2->2->2->2
**Explanation:** All the 0s are segregated to the left end of the linked list, 2s to the right end of the list, and 1s in between.  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700028/Web/Other/blobid1_1723665173.png) 

**Input:** LinkedList: 2->2->0->1
**Output:** 0->1->2->2
**Explanation:** After arranging all the 0s,1s and 2s in the given format, the output will be 0 1 2 2.  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700028/Web/Other/blobid0_1723665157.png)

**Expected Time Complexity:** O(n).  
**Expected Auxiliary Space:** O(n).

**Constraints:**  
1 <= no. of nodes <= 106  
0 <= node->data <= 2


# Brute

```java
```java
class Solution {
    // Function to sort a linked list of 0s, 1s and 2s.
    static Node segregate(Node head) {
        // add your code here
        int cnt0 =0,cnt1=0;
        Node temp = head;
        while(temp!=null){
            if(temp.data == 0)cnt0++;
            else if(temp.data ==1)cnt1++;
            temp = temp.next;
        }
        temp = head;
        while(temp!=null){
            if(cnt0>0){
                temp.data = 0;
                cnt0--;
            }
            else if(cnt1>0){
                temp.data=1;
                cnt1--;
            }
            else temp.data=2;
            temp=temp.next;
        }
        return head;
    }
}
```

# Better

```java
class Solution {
    // Function to sort a linked list of 0s, 1s and 2s.
    static Node segregate(Node head) {
        // add your code here
        Node ans = new Node(-1);
        Node p = ans;
        for(int i=0;i<=2;i++){
            Node temp = head;
            while(temp!=null){
                if(temp.data==i){
                    p.next = new Node(temp.data);
                    p = p.next;
                }
                temp = temp.next;
            }
        }
        return ans.next;
    }
}
```

# Best

```java
class Solution {
    // Function to sort a linked list of 0s, 1s and 2s.
    static Node segregate(Node head) {
        // add your code here
        if(head == null || head.next == null)return head;
        Node zero = new Node(-1);
        Node one = new Node(-1);
        Node two = new Node(-1);
        Node ztemp = zero;
        Node otemp = one;
        Node ttemp = two;
        Node temp =head;
        while(temp!=null){
            if(temp.data == 0){
                ztemp.next = temp;
                ztemp = ztemp.next;
            }
            else if(temp.data ==1){
                otemp.next = temp;
                otemp = otemp.next;
            }
            else if(temp.data == 2){
                ttemp.next = temp;
                ttemp = ttemp.next;
            }
            temp = temp.next;
        }
        ztemp.next = (one.next!=null)?one.next:two.next;
        otemp.next = two.next;
        ttemp.next = null;
        return zero.next;
    }
}
```