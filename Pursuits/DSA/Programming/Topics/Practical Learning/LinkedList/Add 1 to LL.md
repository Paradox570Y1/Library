### Add 1 to a Linked List Number

Difficulty: **Medium**Accuracy: **31.91%**Submissions: **276K+**Points: **4**

You are given a linked list where each element in the list is a node and have an integer data. You need to add **1** to the number formed by concatinating all the list node numbers together and return the head of the modified linked list. 

**Note:** The head represents the first element of the given array.

**Examples :**

**Input:** LinkedList: 4->5->6
**Output:** 457  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700053/Web/Other/blobid0_1722278845.png)  
**Explanation:** 4->5->6 represents 456 and when 1 is added it becomes 457. 

**Input:** LinkedList: 1->2->3
**Output:** 124  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700053/Web/Other/blobid1_1722278908.png)   
**Explanation:**  1->2->3 represents 123 and when 1 is added it becomes 124. 

**Expected Time Complexity:** O(n)  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
1 <= len(list) <= 105  
0 <= list[i] <= 9  

# Better
TC-> O(3N)
SC-> O(N)
```java
class Solution {
    int addCarry(Node head){
        if(head==null)return 1;
        int carry = addCarry(head.next);
        head.data +=carry;
        if(head.data ==10){
            head.data = 0;
        }
        else return 0;
        return 1;
    }
    public Node addOne(Node head) {
        // code here.
        int carry = addCarry(head);
        if(carry==1){
            Node temp = new Node(1);
            temp.next = head;
            return temp;
        }
        return head;
    }
}
```

```java
class Solution {
    Node reverseNode(Node head){
        if(head==null || head.next==null)return head;
        Node newHead = reverseNode(head.next);
        Node front = head.next;
        front.next = head;
        head.next = null;
        return newHead;
    }
    public Node addOne(Node head) {
        // code here.
        Node temp = reverseNode(head);
        head = temp;
        while(temp!=null){
            temp.data++;
            if(temp.data==10){
                temp.data=0;
                if(temp.next == null) {
                    temp.next = new Node(1);
                    break;
                }
            }
            else break;
            temp = temp.next;
        }
        temp = reverseNode(head);
        return temp;
    }
}
```


# Optimal

TC-> O(N)
SC -> O(N) as recursion used some stack space
```java
class Solution {
  public:
    Node* implement(Node* head){
        if(head->next == NULL){
            head->data++;
            if(head->data == 10){
                head->data = 0;
            }
            return head;
        }
        Node* newHead = implement(head->next);
        Node* front = head->next;
        if(front->data==0){
            head->data++;
            if(head->data == 10) head->data = 0;
        }
        return head;
    }
    Node* addOne(Node* head) {
        if(head==NULL)return head;
        Node* temp = implement(head);
        if(temp->data == 0){
            Node* ans = new Node(1);
            ans->next = temp;
            return ans;
        }
        return temp;
    }
};
```