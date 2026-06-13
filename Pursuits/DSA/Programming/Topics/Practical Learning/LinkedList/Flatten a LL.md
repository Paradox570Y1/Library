### Flattening a Linked List
[Link](https://www.geeksforgeeks.org/problems/flattening-a-linked-list/1)
Difficulty: **Medium**Accuracy: **51.53%**Submissions: **169K+**Points: **4**

Given a Linked List, where every node represents a sub-linked-list and contains two pointers:  
(i) a **next** pointer to the next node,  
(ii) a **bottom** pointer to a linked list where this node is head.  
Each of the sub-linked lists is in sorted order.  
Flatten the Link List so all the nodes appear in a single level while maintaining the sorted order.

**Note:** The flattened list will be printed using the **bottom** **pointer** instead of the next pointer. Look at the printList() function in the driver code for more clarity.

**Examples:**

**Input:**  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700192/Web/Other/blobid0_1722066129.png)
**Output:** 5-> 7-> 8- > 10 -> 19-> 20-> 22-> 28-> 30-> 35-> 40-> 45-> 50.
**Explanation**: The resultant linked lists has every node in a single level.(**Note:** | represents the bottom pointer.)

**Input:**  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700192/Web/Other/blobid1_1722066171.png)   
**Output:** 5-> 7-> 8-> 10-> 19-> 22-> 28-> 30-> 50
**Explanation:** The resultant linked lists has every node in a single level.(**Note:** | represents the bottom pointer.)

**Note:** In the output section of the above examples, the **->** represents the bottom pointer**.**

**Expected Time Complexity:** O(n * n * m)  
**Expected Auxiliary Space:** O(n)

**Constraints:**  
0 <= number of nodes <= 50  
1 <= no. of nodes in sub-LinkesList(mi) <= 20  
1 <= node->data <= 103

Try more examples
# Brute 
TC-> O(n\*m) * 2 + O((n\*m) log(n\*m))
SC-> O(n\*m) * 2

```java
class Solution {
    // Function to flatten a linked list
    Node flatten(Node root) {
        // code here
        Node temp = root;
        List<Integer> li = new ArrayList<>();
        while(temp!=null){
            Node btm = temp;
            while(btm!=null){
                li.add(btm.data);
                btm = btm.bottom;
            }
            temp = temp.next;
        }
        Collections.sort(li);
        Node ans = new Node(li.get(0));
        temp = ans;
        for(int i=1;i<li.size();i++){
            temp.bottom = new Node(li.get(i));
            temp = temp.bottom;
        }
        return ans;
    }
}
```


# Optimal

TC-> O(2nm)
SC-> O(n) // using recursive stack space

```java
class Solution {
  public:
    // Function which returns the  root of the flattened linked list.
    Node* merge(Node* l1,Node* l2){
        Node* dummyNode = new Node(-1);
        Node* temp = dummyNode;
        while(l1!=NULL && l2!=NULL){
            if(l1->data <l2->data){
                temp->bottom = l1;
                l1 = l1->bottom;
            }
            else{
                temp->bottom = l2;
                l2 = l2->bottom;
            }
            temp = temp->bottom;
        }
        if(l1==NULL)temp->bottom = l2;
        else temp->bottom = l1;
        return dummyNode->bottom;
    }
    Node* mergeSortedLL(Node *head){
        if(head->next ==NULL)return head;
        Node* list2 = mergeSortedLL(head->next);
        return merge(head,list2);
    }
    Node *flatten(Node *root) {
        // Your code here
        Node* temp = root;
        return mergeSortedLL(temp);
    }
};
```

OR

```java
class Solution {
    // Function to flatten a linked list
    private Node merge(Node l1,Node l2){
        Node p1 = l1;
        Node p2 = l2;
        Node ans = new Node(-1);
        Node trav = ans;
        while(p1!=null && p2!=null){
            if(p1.data<p2.data){
                trav.bottom = p1;
                p1 = p1.bottom;
            }
            else{
                trav.bottom = p2;
                p2 = p2.bottom;
            }
            trav = trav.bottom;
        }
        if(p1==null)trav.bottom = p2;
        else trav.bottom = p1;
        return ans.bottom;
        
    }
    Node flatten(Node root) {
        if(root.next == null)return root;
        Node list2 = flatten(root.next);
        return merge(root,list2);
    }
}
```
# Optimal Using Heap

```java
class Solution {
    // Function to flatten a linked list
    Node flatten(Node root) {
        // code here
        PriorityQueue<Node> minHeap = new PriorityQueue<>((a,b)->a.data-b.data);
        Node temp = root;
        while(temp!=null){
            minHeap.add(temp);
            temp = temp.next;
        }
        Node dummy = new Node(-1);
        temp = dummy;
        while(!minHeap.isEmpty()){
            Node min = minHeap.remove();
            temp.bottom = new Node(min.data);
            temp = temp.bottom;
            if(min.bottom!=null){
                min = min.bottom;
                minHeap.add(min);
            }
        }
        return dummy.bottom;
    }
}
```

OR

```java
class Solution {
    // Function to flatten a linked list
    Node flatten(Node root) {
        // code here
        PriorityQueue<Node> pq = new PriorityQueue<>((a,b)->a.data - b.data);
        Node trav = root;
        while(trav!=null){
            pq.offer(trav);
            trav = trav.next;
        }
        Node ans = new Node(-1);
        trav = ans;
        while(!pq.isEmpty()){
            Node cur = pq.poll();
            trav.bottom = cur;
            trav = trav.bottom;
            if(cur.bottom!=null)pq.offer(cur.bottom);
        }
        return ans.bottom;
    }
}
```