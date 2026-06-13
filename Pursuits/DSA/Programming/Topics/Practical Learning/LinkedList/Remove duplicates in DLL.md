[Link](https://www.geeksforgeeks.org/problems/remove-duplicates-from-a-sorted-doubly-linked-list/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=remove-duplicates-from-a-sorted-doubly-linked-list)
### Remove duplicates from a sorted doubly linked list

Difficulty: **Easy**Accuracy: **50.36%**Submissions: **43K+**Points: **2**

Given a doubly linked list of **n** nodes sorted by values, the task is to remove duplicate nodes present in the linked list.

**Example 1:**

**Input:**
n = 6
1<->1<->1<->2<->3<->4
**Output:**
1<->2<->3<->4
**Explanation:**
Only the first occurance of node with value 1 is 
retained, rest nodes with value = 1 are deleted.

**Example 2:**

**Input:**
n = 7
1<->2<->2<->3<->3<->4<->4
**Output:**
1<->2<->3<->4
**Explanation:**
Only the first occurance of nodes with values 2,3 and 4 are 
retained, rest repeating nodes are deleted.

**Your Task:**  
You have to complete the method **removeDuplicates**() which takes **1** argument: the **head** of the linked list.  Your function should return a pointer to a linked list with no duplicate element.

**Constraint:**  
1 <= n <= 105  
**Expected Time Complexity:** O(n)  
**Expected Space Complexity:** O(1)

```java
class Solution{
    Node removeDuplicates(Node head){
        // Code Here.
        Node i = head;
        if(i==null)return null;
        Node j = head.next;
        while(j!=null){
            if(j.data != i.data){
                i.next = j;
                j.prev = i;
                i=j;
            }
            else if(j.next==null){
                i.next = null;
            }
            j=j.next;
        }
        return head;
    }
}
```

```java
class Solution
{
public:

    Node * removeDuplicates(struct Node *head)
    {
        // Your code here
        Node* temp = head;
        while(temp!=NULL && temp->next!=NULL){
            Node* nextNode = temp->next;
            while(nextNode!=NULL && nextNode->data == temp->data){
                Node* deleteNode = nextNode;
                nextNode = nextNode->next;
                free(deleteNode);
            }
            temp->next = nextNode;
            if(nextNode!=NULL)nextNode->prev = temp;
            temp = temp->next;
        }
        return head;
    }
};
```