[206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [5,4,3,2,1]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

**Input:** head = [1,2]
**Output:** [2,1]

**Example 3:**

**Input:** head = []
**Output:** []

**Constraints:**

- The number of nodes in the list is the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`

# Brute
A straightforward approach to reversing a singly linked list requires an **additional** **data** **structure** to temporarily store the values. We can use a **stack** for this. By pushing each node onto the stack as we move through the list, we effectively **reverse** **the** **order** of the nodes. Once all the nodes are stored in the **stack**, we rebuild the reversed linked list by **popping nodes** from the stack and **assigning** them to the nodes. The result is a new linked list with the elements in the **opposite** **order** of the original list.

**Time Complexity: O(2N)** This is because we **traverse** the linked list **twice**: once to push the values onto the stack, and once to pop the values and update the linked list. Both traversals take O(N) time, hence time complexity  O(2N) ~ O(N).

**Space Complexity: O(N)** We use a **stack** to store the values of the linked list, and in the worst case, the stack will have all **N** **values,**  ie. storing the complete linked list.
```java

import java.util.Stack;
public class ReverseLinkedListUsingStack {
    public static Node reverseLinkedList(Node head) {
        Node temp = head;       
        Stack<Integer> stack = new Stack<>();  

        while (temp != null) {
            stack.push(temp.data); 
            temp = temp.next;      
        }
        temp = head;  

        while (temp != null) {
            temp.data = stack.pop();  
            temp = temp.next;         
        }
        return head;  
    }
```


# Optimal

**Time Complexity: O(N)** The code **traverses** the **entire** **linked** **list** once, where 'n' is the number of nodes in the list. This traversal has a **linear** **time** **complexity**, O(n).

**Space Complexity: O(1)** The code uses only a **constant** **amount** of **additional** **space**, regardless of the linked list's length. This is achieved by using three pointers (**prev, temp** and **front**) to reverse the list without any significant extra memory usage, resulting in **constant** **space** complexity, O(1).

```java
public class ReverseLinkedListUsingStack(Node head) {
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
```

my solution
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode back = head;
        ListNode prevLocation = null;
        while(head != null){
            head = head.next;
            back.next = prevLocation;
            prevLocation = back;
            back = head;
        }

        return prevLocation;
    }
}
```



# Optimal 3

Recursion gives the ability to **break** **down** a problem statement into **small** **problems** that can be solved **incrementally**. It keeps solving these smaller problems until it reaches the smallest possible solution, often referred to as the base case, from where it can start combining the results of those smaller solutions to ultimately solve the original, larger problem.

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head==NULL || head->next == NULL){
            return head;
        }
        ListNode* newHead= reverseList(head->next);
        ListNode* front= head->next;
        front->next = head;
        head->next = nullptr;
        return newHead;
    }
};
```