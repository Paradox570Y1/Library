[GFG](https://www.geeksforgeeks.org/problems/find-length-of-loop/1)
Difficulty: **Easy**Accuracy: **44.26%**Submissions: **217K+**Points: **2**

Given the head of a linked list, determine whether the list contains a loop. If a loop is present, **return the number of nodes** in the loop, otherwise **return 0**.

![](https://contribute.geeksforgeeks.org/wp-content/uploads/linkedlist.png)

**Note: '**c**'** is the position of the node which is the next pointer of the last node of the linkedlist. If c is 0, then there is no loop.

**Examples:**

**Input:** LinkedList: 25->14->19->33->10->21->39->90->58->45, c = 4
**Output:** 7
**Explanation:** The loop is from 33 to 45. So length of loop is 33->_10_->21->39-> 90->58->_45_ = **7.** The number 33 is connected to the last node of the linkedlist to form the loop because according to the input the 4th node from the beginning(1 based indexing)   
will be connected to the last node for the loop.  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700620/Web/Other/blobid0_1722797558.png) 

**Input:** LinkedList: 5->4, c = 0
**Output:** 0
**Explanation:** There is no loop.  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700620/Web/Other/blobid3_1722798030.png)  

**Expected Time Complexity:** O(n)  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
1 <= no. of nodes <= 106  
0 <= node.data <=106  
0 <= c<= n-1



# Optimal

```java
public class LinkedListLoopLength {
    static int findLength(Node slow, Node fast){
        int cnt = 1;
        fast = fast.next;
        while(slow!=fast){
            cnt++;
            fast = fast.next;
        }
        return cnt;
    }
    static int lengthOfLoop(Node head) {
        Node slow = head;
        Node fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;  
            fast = fast.next.next; 
            if (slow == fast) {
                return findLength(slow, fast);
            }
        }
        return 0; 
    }
```

```java
class Solution {
  public:
    // Function to find the length of a loop in the linked list.
    int countNodesinLoop(Node *head) {
        // Code here
        Node* slow = head;
        Node* fast = head;
        if(head== NULL)return 0;
        while(fast!= NULL && fast->next !=NULL){
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow){
                int cnt=1;
                slow = slow->next;
                while(slow!=fast){
                    slow = slow->next;
                    cnt++;
                }
                return cnt;
            }
        }
        return 0;
    }
};
```