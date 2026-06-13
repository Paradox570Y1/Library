# What is Linked List ?
- As we know in array elements are stored in contiguous memory location, but in Linked List they are stored randomly.
- In Linked List you can store all types of data types and even data structures.
- It is stored in heap memory.


# Traversing in Linked List
- In linked list we store elements by specifying their memory location.
- Starting of the linked list is called head of the linked list and HEAD of LL is stored in lets say memory location 1.
- Starting element also stores the next element's memory location, similarly 2nd element will store 3rd element's memory location and so on, its like creating links until it reaches the TAIL of the linked list or null.
- In JAVA it  is `null` and in C++ we use `nullptr`

# Where LL is used?
- In terms of data structures, LL is used in Stack and Queue.
- In real scenarios, we always use it in a browser.

# Types of LL

**1-D Linked List**
- Where we just store the address of the next element so we cannot move back but only go forward.
**2-D Linked List**
- In this type of LL we store address of next as well as previous element.

# Declaring a Linked List

**Self Defined Data Type**
`In C++`
```cpp
struct Node{
	public:
	int data;
	Node* next;
	Node(data1,next1){
		data = data1;
		next = next1;
	}
};
//or
```cpp
class Node{
	public:
	int data;
	Node* next;
	Node(data1,next1){
		data = data1;
		next = next1;
	}
};

// we can also customize LL
class Node{
	public:
	int data;
	Node* next;
	Node(data1,next1){
		data = data1;
		next = next1;
	}
	Node(data1){
		data = data1;
		next = nullptr;
	}
};
```
![[Pasted image 20241224084738.png|100]]

**For any type of data type to get stored use Template in CPP**
```cpp
template <Typename T>
class Node {
public:
    T data;
    Node<T> *next;

    // Default constructor
    Node()
    {
        data = 0;
        next = NULL;
    }

    // Parameterised Constructor
    Node(T data)
    {
        this->data = data;
        this->next = NULL;
    }
};
Node<int>* y = new Node(3);
```

`In Java (only Class)`
```java
class Node{
	int data;
	Node next;
	
	Node(int data1,Node next1){
		this.data = data1;
		this.next = next1;
	}
	Node(int data1){
		this.data = data1;
		this.next = null;
	}
}
```

> Struct is like the subset of class which doesn't offer OOPS concept but works just like it.
# Accessing a Linked List

- In C++
```cpp
Node n = Node(2,nullptr);
Node* y = &n;
//OR
Node* y = new Node(2,nullptr);
cout << y; //gives memory address of the node created
cout << y->data << " " << y->next;
```

> **If we don't use new keyword then it behaves like an object**
```cpp
Node y = Node(2,nullptr);
cout << y.data << " "<< y.next;
```


- In Java
```java
Node y = new Node(2,null);
System.out.print(y.data);
System.out.print(y.next);
```

# Memory Space of Linked List

> In 32 bit System:
> 	int takes 4 bytes
> 	pointer takes 4 bytes
> 	Total Size -> 8 bytes
> In64 bit System:
> 	int takes 4 bytes
> 	pointer takes 8 bytes
> 	Total Size -> 12 bytes


# How to push array into a Linked List

- In CPP
![[Pasted image 20241224092250.png|300]]

- In Java
![[Pasted image 20241224092455.png|300]]


# How to get length of Linked List

In CPP
![[Pasted image 20241224092417.png|200]]


In Java
![[Pasted image 20241224092604.png|300]]

# To check if Element is present in LL
![[Pasted image 20241224092747.png|300]]


# Deletion in LL

### Deleting Head of LL
![[Pasted image 20241224094640.png]]

In CPP you need to manually free the memory using free or delete but in Java we have garbage collector and therefore memory is freed automatically if there is no reference to data, but this might take place automatically during the future.

![[Pasted image 20241224094950.png|250]]

### Deleting Tail of LL
In CPP
![[Pasted image 20241224095616.png|300]]

In Java
![[Pasted image 20241224095736.png|300]]


# Deleting Kth Element
- In Linked List start from edge cases and build around it.
In CPP
![[Pasted image 20241224101422.png|300]]

In Java
![[Pasted image 20241224101555.png|300]]

# Deleting a Value
![[Pasted image 20241224115552.png|300]]

# Inserting at head

![[Pasted image 20241224114154.png|250]]

You can do it directly too
![[Pasted image 20241224114230.png|250]]


# Insert at Tail
![[Pasted image 20241224114409.png|200]]

# Insert at Kth Element

![[Pasted image 20241224115129.png|300]]

# Insert before the value x
![[Pasted image 20241224115935.png|300]]
If there is value not in node list then you can use flag to return accordingly

> [[ListNode vs Node]]


# Doubly Linked List

- Each **node** contains three parts:
    1. Data
    2. Pointer to the next node (`next`)
    3. Pointer to the previous node (`prev`)
- The **DoublyLinkedList** class manages the nodes and provides methods to manipulate the list.

```cpp
// Node structure for Doubly Linked List
class Node {
public:
    int data;
    Node* next;
    Node* prev;

    // Constructor
    Node(int value) {
        data = value;
        next = nullptr;
        prev = nullptr;
    }
    Node(int value,Node* next1,Node* prev1){
	    data = value;
	    next = next1;
	    prev = prev1;
    }
};
```

# How to make Doubly LL
 Construct the doubly linked list from **arr** and return the **head** of it.
 [Link](https://www.geeksforgeeks.org/problems/introduction-to-doubly-linked-list/1)
```java
class Solution {
    Node DLL(int arr[]){
        if(arr.length==0)return null;
        Node head = new Node(arr[0]);
        Node temp = head;
        for(int i=1;i<arr.length;i++){
            Node tempPrev = temp;
            temp.next = new Node(arr[i]);
            temp = temp.next;
            temp.prev = tempPrev;
        }
        return head;
    }
    Node constructDLL(int arr[]) {
        // Code here
        return DLL(arr);
    }
}
```


```cpp
class Solution {
  public:
    Node* constructDLL(vector<int>& arr) {
        // code here
        Node* head = new Node(arr[0]);
        Node* temp  = head;
        for(int i=1;i<arr.size();i++){
            Node* temp2 = temp;
            temp->next = new Node(arr[i]);
            temp = temp->next;
            temp->prev = temp2;
        }
        return head;
    }
};
```


# How to delete a node Double LL
[Link](https://www.geeksforgeeks.org/problems/delete-node-in-doubly-linked-list/1)
```cpp
class Solution {
  public:
    // Function to delete a node at given position.
    Node* deleteHead(Node* temp){
        Node* back = temp;
        temp = temp->next;
        back->next = nullptr;
        delete back;
        temp->prev = nullptr;
        return temp;
    }
    void deleteTail(Node* temp){
        Node* front = temp;
        temp = temp->prev;
        front->prev = nullptr;
        delete front;
        temp->next = nullptr;
    }
    Node* deleteNode(Node* head, int x) {
        // Your code here
        if(head == NULL)return NULL;
        Node* temp = head;
        int cnt=1;
        while(cnt<x){
            temp = temp->next;
            cnt++;
        }
        Node* back = temp->prev;
        Node* front = temp->next;
        if(back !=NULL && front!=NULL){
            temp->prev = nullptr;
            temp->next = nullptr;
            back->next = front;
            front->prev = back;
        }
        else if(back == NULL){
            return deleteHead(temp);
        }
        else if(front == NULL){
            deleteTail(temp);
        }
        return head;
    }
};
```

# Adding a node in Doubly LL

[Link](https://www.geeksforgeeks.org/problems/insert-a-node-in-doubly-linked-list/1)
```java
class Solution {
    // Function to insert a new node at given position in doubly linked list.
    Node addNode(Node head, int p, int x) {
        // Your code here
        Node temp = head;
        int cnt = 0;
        while(cnt<p){
            temp = temp.next;
            cnt++;
        }
        if(temp.next == null){
            temp.next = new Node(x);
            Node prevNode = temp;
            temp = temp.next;
            temp.prev = prevNode;
        }
        else{
            Node nextNode = temp.next;
            temp.next = new Node(x);
            Node prevNode = temp;
            temp = temp.next;
            temp.prev = prevNode;
            temp.next = nextNode;
            prevNode = temp;
            temp = temp.next;
            temp.prev = prevNode;
        }
        return head;
    }
}
```


# Reverse a DLL

```cpp
class Solution {
  public:
    // Function to reverse a doubly linked list
    DLLNode* reverseDLL(DLLNode* head) {
        // Your code here
        DLLNode* temp = head;
        while(1){
            DLLNode* front = temp->next;
            temp->next = temp->prev;
            temp->prev = front;
            if(temp->prev == NULL)break;
            temp = temp->prev;
        }
        return temp;
    }
};
```


# Using library functions for linked list

```java
LinkedList<Integer> li = new ArrayList<>();
li.addFirst(3);
li.addLast(4); or li.add(4)
li.removeFirst()
li.removeLast() or li.remove()
li.size()
li.get(index)
// for printing all elements
for (int num : list) {
    System.out.println(num);
}
```