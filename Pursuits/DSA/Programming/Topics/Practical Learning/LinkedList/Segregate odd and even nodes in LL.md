[328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return _the reordered list_.

The **first** node is considered **odd**, and the **second** node is **even**, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/10/oddeven-linked-list.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [1,3,5,2,4]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/10/oddeven2-linked-list.jpg)

**Input:** head = [2,1,3,5,6,4,7]
**Output:** [2,3,6,7,1,5,4]

**Constraints:**

- The number of nodes in the linked list is in the range `[0, 104]`.
- `-106 <= Node.val <= 106`



# Brute
Do data replacement.
Use list to store first odd data and then even data and then again traverse the nodes and modify the data from list.

# Better

```java
class TUF{
static ListNode head, tail; // head and tail of the LinkedList

static void PrintList(ListNode head) // Function to print the LinkedList
{
    ListNode curr = head;
    for (; curr != null; curr = curr.next)
        System.out.print(curr.val+"-->");
    System.out.println("null");
}

static void InsertatLast(int value) // Function for creating a LinkedList
{

    ListNode newnode = new ListNode(value);
    if (head == null)
        {
        head = newnode;
        tail = newnode;
        }
    else
        tail = tail.next = newnode;
}

static ListNode SegregatetoOddEVen()
{
    // creating Heads of Odd and Even LinkedLists
    ListNode oddHead = new ListNode(-1), oddTail = oddHead;
    ListNode evenHead = new ListNode(-1), evenTail = evenHead;
    ListNode curr = head, temp;
    while (curr!=null)
    {
        // Breaking the Link of the curr Node.
        temp = curr;
        curr = curr.next;
        temp.next = null;

        if (temp.val%2!=0) // If odd Node,append to or = curr.ndd LinkedList
        {
            oddTail.next = temp;
            oddTail = temp;
        }
        else // If Even Node,append to even LinkedList
        {
            evenTail.next = temp;
            evenTail = temp;
        }
    }
    evenTail.next = oddHead.next; 
    // Appending Odd LinkedList at end of EvenLinkedList
    return evenHead.next;
}
```

# Optimal

#Mine
```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        ListNode LastOddNode = head;
        while(LastOddNode!= null && LastOddNode.next!=null && LastOddNode.next.next!=null){
            LastOddNode = LastOddNode.next.next;
        }
        if(head == LastOddNode) return head;
        ListNode temp = head;
        boolean toggle = false;
        ListNode LastNode = LastOddNode;
        ListNode LastEven = null;
        if(LastNode.next != null)LastEven = LastNode.next;
        ListNode prev = null;
        while(temp!=LastOddNode){
            
            if(toggle){
                LastNode.next = temp;
                prev.next = temp.next;
                LastNode = LastNode.next;
            }
            toggle = toggle ^ 1<3; //basically toggle ^ true
            prev = temp;
            temp = temp.next;
        }
        LastNode.next = LastEven;
        return head;
    }
}
```

#Striver
```java
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        ListNode* Odd = head;
        if(Odd == NULL || Odd->next == NULL)return head;
        ListNode* EvenStart = head->next;
        ListNode* Even = EvenStart;
        while(Even!= NULL && Even->next!=NULL){
            Odd->next = Odd->next->next;
            Even->next = Even->next->next;
            Odd = Odd->next;
            Even = Even->next;
        }
        Odd->next = EvenStart;
        return head;
    }
};
```

