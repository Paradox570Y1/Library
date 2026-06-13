[138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return _the head of the copied linked list_.

The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

- `val`: an integer representing `Node.val`
- `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.

Your code will **only** be given the `head` of the original linked list.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

**Input:** head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
**Output:** [[7,null],[13,0],[11,4],[10,2],[1,0]]

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/12/18/e2.png)

**Input:** head = [[1,1],[2,1]]
**Output:** [[1,1],[2,1]]

**Example 3:**

**![](https://assets.leetcode.com/uploads/2019/12/18/e3.png)**

**Input:** head = [[3,null],[3,0],[3,null]]
**Output:** [[3,null],[3,0],[3,null]]

**Constraints:**

- `0 <= n <= 1000`
- `-104 <= Node.val <= 104`
- `Node.random` is `null` or is pointing to some node in the linked list.

# Better

```java
class Solution {
    public Node copyRandomList(Node head) {
        Node dummy = new Node(-1);
        Node temp = dummy;
        Node i = head;
        while(i!=null){
            temp.next = new Node(i.val);
            temp = temp.next;
            i = i.next;
        }
        temp.next =  null;
        HashMap<Node,Node> hm = new HashMap<>();
        i = head;
        temp = dummy.next;
        while(i!=null){
            hm.put(i,temp);
            i=i.next;
            temp=temp.next;
        }
        hm.put(i,temp);
        temp = dummy.next;
        i = head;
        while(temp!=null){
            temp.random = hm.get(i.random);
            temp = temp.next;
            i=i.next;
        }
        return dummy.next;
    }
}
```


```java
class Solution {
    public Node copyRandomList(Node head) {
        Node dummy = new Node(-1);
        Node temp = dummy;
        HashMap<Node,Integer> hm1 = new HashMap<>();
        Node i = head;
        int idx=0;
        while(i!=null){
            hm1.put(i,idx++);
            i = i.next;
        }
        hm1.put(i,idx);
        HashMap<Integer,Node> hm2 = new HashMap<>();
        i = head;
        int cnt=0;
        while(i!=null){
            temp.next = new Node(i.val);
            hm2.put(cnt++,temp.next);
            temp = temp.next;
            i = i.next;
        }
        temp.next =  null;
        hm2.put(cnt,temp.next);
        temp = dummy.next;
        i = head;
        while(temp!=null){
            temp.random = hm2.get(hm1.get(i.random));
            temp = temp.next;
            i=i.next;
        }
        return dummy.next;
    }
}
```

TC-> O(2n)
SC-> O(n) + O(n) {required by answer}

```java
class Solution {
    public Node copyRandomList(Node head) {
        Node i = head;
        HashMap<Node,Node> hm = new HashMap<>();
        while(i!=null){
            Node temp = new Node(i.val);
            hm.put(i,temp);
            i = i.next;
        }
        i = head;
        while(i!=null){
            Node curr = hm.get(i);
            curr.next = hm.get(i.next);
            curr.random = hm.get(i.random);
            i=i.next;
        }
        return hm.get(head);
    }
}
```


# Optimal
TC-> O(3n)
SC-> O(n) // required for storing answer
But no extra space used
```java
class Solution {
public:
    Node* copyRandomList(Node* head) {
        Node* temp = head;
        while(temp!=NULL){
            Node* copyNode = new Node(temp->val);
            copyNode->next = temp->next;
            temp->next = copyNode;
            temp = temp->next->next;
        }
        temp = head;
        while(temp!=NULL){
            if(temp->random !=NULL)
            temp->next->random = temp->random->next;
            else temp->next->random = nullptr;
            temp = temp->next->next;
        }
        Node* ans= new Node(-1);
        temp = head;
        Node* res = ans;
        while(temp!=NULL){
            res->next = temp->next;
            res = res->next;
            temp->next = temp->next->next;
            temp = temp->next;
        }
        return ans->next;
    }
};
```


OR

```java
class Solution {
    public Node copyRandomList(Node head) {
        Node dummy = new Node(-1);
        Node trav = head;
        while (trav != null) {
            Node node = new Node(trav.val);
            node.next = trav.next;
            trav.next = node;
            trav = trav.next.next;
        }
        trav = head;
        while (trav != null) {
            trav.next.random = (trav.random == null)? null: trav.random.next;
            trav = trav.next.next;
        }
        trav = head;
        Node cpy = dummy;
        while (trav != null) {
            cpy.next = trav.next;
            cpy = cpy.next;
            trav.next = cpy.next;
            trav = trav.next;
        }
        return dummy.next;
    }
}
```