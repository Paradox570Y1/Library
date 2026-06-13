- Write properly structured codes
![[Pasted image 20250715194024.png|500]]

![[Pasted image 20250715194257.png|400]]

-  Interface is dissociated from implementation.
	- The **definition of how something is used (interface)** is **separated from how it works internally (implementation)**.
- You can share the header files and executable and that is interface and implementation is handled by language itself, unless you read documentation.

#### Array implementation

- Create an array of size n and push elements as long as it has space. Now if space is full then do following.
- Make use of dynamic memory allocation:
	- Now we will create an array of size n+1 , copy all elements of original array and then add 1 more element. This way to add 1 more element will require O(N) time complexity which means , N elements will take O(N²) time complexity and quadratic time complexity is something we avoid.
	- Now if we use standard way to create an array of twice the size of original array in case original array become full. Then it will take O(N) time complexity in case of adding N elements as well.(as explained following)

![[Pasted image 20250715195350.png|400]]
![[Pasted image 20250715195504.png|400]]
![[Pasted image 20250715195801.png|400]]

How to avoid the unused space in case of doubling the size of an array.
![[Pasted image 20250715203424.png]]
- In case your array is half empty then reduce the size by 1/4, this will make sure that your amortized time complexity is O(N).
- If you tried to reduce it by 1/2 when array is filled less than half then again on crossing that half boundary will lead to doubling the size so this will reduce the performance and leads to thrashing or resizing oscillation.
- It's not the best - **Why?** → It causes inefficient memory use and doesn't help amortized cost — better to shrink only when size drops below 1/4 and then halve.
# Even better way 
- Best Practice (what most libraries like Java's `ArrayList`, Python's `list`, etc. follow):
	- Double the array size when full
	- Halve the array size when the number of elements falls below 1/4 capacity


- In case of linked list this graph will be constant which is most optimal.
	- But still accessing linked list from storage can be more time consuming then accessing contiguous memory as it gets stored in cache whereas linked list is scattered across the main storage.



> Whole purpose of doing problem solving is to deal with Big Data , like millions of entries so we need to create an optimized algorithm to that task.


Look at documentation to know how data structure is implemented in language.
![[Pasted image 20250715200531.png]]


- assert library in C

- In C there is no garbage collector so if using dynamic memory allocation , free the memory as well

---
# Stack Implementation

```java
#include <stdio.h>
#include <stdlib.h>
#include <assert.h>
#include <stdbool.h>
int* stack;
int max_size=1;
int len=0;
void resize_array(int new_size){
  int* new_stack = (int*)malloc(new_size * sizeof(int));
  for(int i=0;i<len;i++){
    new_stack[i] = stack[i];
  }
  free(stack);
  stack = new_stack;
}
void push(int e){
  stack[len++] = e;
  if(len == max_size){
    max_size*=2;
    resize_array(max_size);    
  }
}
int pop(){
  if(len==0)return -1;
  int item = stack[--len];
  if(len <= max_size/4 && max_size>1){
    max_size/=2;
    resize_array(max_size);
  }
  return item;
}
int size(){
  return len;
}
bool empty(){
  return len==0;
}
void testCases(){
  assert(max_size==1);
  push(5);
  push(8);
  assert(max_size==4);
  pop();
  push(1);
  push(12);
  push(34);
  assert(max_size==8);
  assert(size()==4);
  assert(empty()==false);
  pop();
  pop();
  pop();
  pop();
  assert(empty()==true);
}
int main(){
  stack = (int*)malloc(max_size * sizeof(int));
  testCases(); 
}
```

--- 
# Queue Implementation

```C
// Online C compiler to run C program online
#include <stdio.h>
#include <assert.h>
#include <stdlib.h>
int* queue;
int rear=0;
int front=0;
int max_size=1;
void resize(int new_size){
    int* new_queue = (int*) malloc(sizeof(int)*new_size);
    for(int i=front;i<rear;i++){
        new_queue[i-front] = queue[i];
    }
    free(queue);
    rear = rear-front;
    front=0;
    max_size = new_size;
    queue = new_queue;
}
void push(int val){
    queue[rear++] = val;
    if(rear==max_size){
        resize(2*max_size);
    }
}
int pop() {
    if (rear - front > 0) {
        int val = queue[front++];
        if (size() <= max_size / 4 && max_size > 1) {
            resize(max_size / 2);
        }
        return val;
    }
    return -1;
}
int size(){
    return rear-front;
}
int isEmpty(){
    return rear == front;
}
void test(){
    push(3);
    push(2);
    assert(size()==2);
    assert(pop() == 3);
    push(5);
    push(8);
    assert(size() == 3);
}
int main() {
    queue = (int*) malloc(sizeof(int)*max_size);
    test();
    return 0;
}
```

---
>Use `-ea` flag  like `java -ea file.java` to use assert in java

# Binary Tree

![[Pasted image 20250805194712.png|400]]

![[Pasted image 20250805194826.png|400]]
![[Pasted image 20250805194918.png|400]]
- It is a utility algorithm and has many use cases
- Uses of Priority Queue
	- Artificial Intelligence (A* Search)
	- Computer Networks (Web Cache)
	- OS(scheduling, load balancing)
	- Date Compression (Huffman Codes)
	- Graphs (Dijkstra's Algorithm {shortest path}, Prime Algorithm)
	- Number Theory (Sum of Powers)
	- Machine Learning
		- Spam filtering (Bayesian Spam Filter)
		- Stats applications


![[Pasted image 20250805200249.png|400]]

- Make use of  access specifiers like `public\private\protected` during coding.

>NOTE
>In C/C++ , int array is primitive data type.
>In Java , int array is not a primitive type.
>- They have properties (like `.length`) and methods like `.clone()`.
>![[Pasted image 20250805200628.png|300]]

| Feature             | C/C++             | Java                                                |
| ------------------- | ----------------- | --------------------------------------------------- |
| `int[]` is...       | Primitive-like    | Object                                              |
| Memory layout       | Contiguous memory | Heap, object layout                                 |
| Has metadata?       | ❌ No              | ✅ Yes (e.g., `.length`)                             |
| First-class object? | ❌ No              | ✅ Yes                                               |
| Type system         | Not unified       | Unified (everything is an object except primitives) |

#### Using Ordered and Unordered Array
![[Pasted image 20250805201425.png|400]]

![[Pasted image 20250805201924.png|400]]

- Time complexity is for n operations
![[Pasted image 20250805202507.png|400]]

![[Pasted image 20250805202827.png|400]]

- Generics
- Operators
- Comparators
- Comparables

---
Use following tools to check if you are writing the code according to Coding Standards.
- Java - use `Checkstyle`
- C++ - use `cpplint`
## Coding Standards

Following coding standards is important for students because it prepares them for professional development. Often in the selection process of product companies, interviewers look for if student is writing clean and structured code. Students who follow these guidelines early on are better prepared for internships and future careers, where they will be expected to work on large, complex projects with teams.

Development environments like Eclipse, VS Code etc. have inbuilt tools which automatically formats the code e.g. indentation. However, there are still lots of guidelines which students do not incorporate while coding such as comments, following naming conventions amongst others.

This article covers tools for Java and C/C++ which students can run and ensure compliance with industry standards. This will help build them muscle memory to always write clean and structured code. This will also be essential for students while developing projects and submitting to companies during the campus placement.

### Checkstyle

[Checkstyle](https://checkstyle.sourceforge.io/) is a development tool to help programmers write Java code that adheres to a coding standard. It can find class design and method problems, code layout and formatting issues. The latest release of CheckStyle can be downloaded from [here](https://github.com/checkstyle/checkstyle/releases/).

Checkstyle can be run on your Java file using the following command

```wsl
java -jar <path to checkstyle jar> -c google_checks.xml <path to java file>
```

### Cpplint

Cpplint is an open-source command-line tool designed to check C++ source code for conformance to Google’s C++ style guide. it functions as a static code analysis tool focusing on style and formatting issues.

On Ubuntu, Cpplint can be installed using following command

```wsl
sudo apt-get install cpplint
```

Cpplint can be run on a C/C++ file using the following command

```c
cpplint QueueArray.cpp
cpplint QueueArray.c // only casting warnings will be thrown
cpplint --filter=-readability/casting QueueArray.c //Since it is checking readability according to cpp but c does not have static_cast or reinterpret_cast
```

---

[[Java Interface]]
![[Pasted image 20250826194051.png|300]]

![[Pasted image 20250826194110.png|300]]

- Java is strongly typed language , so rather then runtime errors, errors are tried to be caught during compile time. 
- Therefore Java throws a lot of compilation error.

![[Pasted image 20250826194544.png|300]]
![[Pasted image 20250826194617.png|300]]
- It will print "Hello".
![[Pasted image 20250826195748.png|300]]
### Polymorphism can take place in any shape
- A class can take shape of:
	- class
	- base class
	- Interface

# In java
- One class can extend only one class
- as many interfaces.
- Object class in Java
	- It has two methods equals and hashcode.


# Equals
- here c1 and c2 are objects having same data but both created with new keyword.
![[Pasted image 20250826201313.png]]
- answer is false false 


![[Pasted image 20250826201424.png|300]]
- Here parameter is `Object o` bcz that is the method we are trying to override

![[Pasted image 20250826202750.png]]















# Comparable interface

![[Pasted image 20250826201623.png|300]]

![[Pasted image 20250826203445.png|250]]

**Why Typecast to Item\[] in above case from new Object\[]**
- At Compile time , compiler doesn't know what kind of datatype will be passed to it so at compile type it take the data as generic object but during runtime that generic object gets type casted to given template.
![[Pasted image 20250826204800.png|250]]

- So if we pass Wrapper class of  primitive data types to interface then those data types class already have Comparable interface implemented so just type casting their objects to Comparable and using compareTo method works.
![[Pasted image 20250826210653.png]]

- But in case you create custom classes then you have to implement that Comparable Interface yourself.
- So you must explicitly implement `Comparable<T>` and override `compareTo`.
![[Pasted image 20250826205309.png|300]]


# Overriding equals method

![[Pasted image 20250902202355.png]]


# `HashCode()` Method of object
- It is in Object Class
	- So it is available to every class
	- You don't override it and it returns the memory address of where the object is stored.
- `HashCode()` is integer representation of object.
- They are computed at runtime.
- They are Deterministic.
	- If hash code of an object is calculated million times it will still be same.
![[Pasted image 20250902203023.png|400]]

According to Java Contracts:
- If two objects are equal then their hashcode should be equal.
- It is not required but it is desirable.
- It's difficult to ensure that because objects are created at runtime so you can't do much compile time check for this.
- Hence we say it's desirable and cannot be enforced.
![[Pasted image 20250909194454.png|200]]


Every class that is available to you in Java has some implementation of Hash code which is refined over the years.

![[Pasted image 20250909194806.png|300]]
![[Pasted image 20250909194803.png|300]]

![[Pasted image 20250909195030.png|300]]
![[Pasted image 20250909195026.png|300]]
So, i == j is false but rest condition are true.


![[Pasted image 20250909195148.png|300]]
![[Pasted image 20250909195152.png|300]]
Even hash codes for true and false are predefined.


#### How to implement hashcode for String

![[Pasted image 20250909195656.png]]
- Hence if two strings are equal then their hash value will also be equal.
- Number 31 is taken because it's a prime number as prime number results in uniform distribution and based on data prime number changes.
- One of the reason 31 is chosen because there are 31 bits in an integer.
[[Reason for choosing 31]]

# How to implement it in custom class

![[Pasted image 20250909200744.png|300]]


---
# HashMap
- It is available in all languages whether functional or procedural.
![[Pasted image 20250909191317.png|400]]


- Using array
![[Pasted image 20250909191710.png]]

Problems:
- If we take size of array as number of keys then it will not be space efficient.
- Lookup takes upto O(N²) time for N lookups.


### What is Hashing?
![[Pasted image 20250909194026.png|300]]
The process of converting key objects into number is called hashing.

#### Most popular Approaches for Hashing out of 1000's of approaches:
- **Separate Chaining**
	![[Pasted image 20250909192930.png|300]]
	There would be collision
	![[Pasted image 20250909193020.png|200]]
	-We need to ensure that data gets uniformly distributed.
	-For N entries and M blocks we need each block should have N/M entries  instead of having dispersed values.
	-Therefore in case of high collision time complexity for look up becomes O(N) in worst case ever.
	![[Pasted image 20250909193251.png|300]]
	In separate chaining you try to make the size of  array M to be N/4.
	So
	![[Pasted image 20250909201647.png]]
	
	It is implemented with Linked List where objects with similar hash codes are linked together and whenever you look up an element if it exists getter function returns you the hashcode which consist of LinkedList containing the object you are looking for then you will traverse the linked list to get the object.
	![[Pasted image 20250909201852.png]]
- Linear Probing - best for space efficiency


#### Important use case
- Hashing is used in DNS Servers for domain names.
- Sharding concept is also similar where requests are distributed uniformly over the 
![[Pasted image 20250909202558.png|200]]


# HashMap characteristics
- If one object is created in hashmap then it's hash code gets evaluated, now suppose we created a string then generating it's hashcode take time equal to length of string and then it is cached but if we again generate the same string in hashmap then it's hashcode is fetched from cache.
- There is every possibility that different objects can end up colliding so even if hashcode  are equal using equal method we can differentiate among them.
- It's a dynamic data structure so it also resizes itself according to data.


### How DOS attack was used to bring down the server
![[Pasted image 20250909203519.png]]
- But through hash codes we can distribute the request uniformly among servers which prevents this as well.




Q. `LinkedHashMap` and how it is used.




# Implementing HashMap using Separate Chaining

![[Pasted image 20250916192403.png|400]]


# Implementing HashMap using Linear Probing
![[Pasted image 20250916192937.png|400]]

- Key value pair is placed at position itself
![[Pasted image 20250916193638.png|300]]

- Using delete operation in linear probing is tricky.
	- If you delete a key at position then you need to ensure that while checking some another key downwards it doesn't stop at that point. So there will be extra overhead to handle that.
	- Simplest way to handle this is to create some dummy node at place where deletion happened, so while searching for another key it continues further till null is discovered or key is discovered.



# Recursion
- Stack overflow error
![[Pasted image 20250916200210.png|400]]
- Another way to prevent Stack Overflow is using Tail Recursion.
- Scala , Kotlin , Javascript support tail recursion but java and Python does not.
- Unless you are using a function programming language Tail Recursion cannot be done.


# For finding base case faster
- Instead of thinking the way of implementation in recursion think what should be the base case like empty list , only 1 node etc.
- Don't think about what should you do for next input to function but see what should be done for the current function considering we got the future part.
![[Pasted image 20250916202234.png|300]]
- How to combine sub problems to return the result.

- Inductive data structure
	- Those data structure in which you are using the simpler component to define the whole data structure like node used to define a linked list.
	- If there is any problem on inductive data structure then there is high chance that recursive solution is feasible.


### How to calculate time complexity
- One way is do it Mathematically.
	![[Pasted image 20250916203121.png|300]]
	
	![[Pasted image 20250916203316.png|300]]



- Using Master's Theorem
	![[Pasted image 20250916204004.png|300]]
	![[Pasted image 20250916203859.png|300]]
	![[Pasted image 20250916203954.png|300]]
	![[Pasted image 20250916204116.png|300]]


# Example of Tail Recursion

![[Pasted image 20250916204642.png]]
- 2nd code does not do processing on return value but 1st does.
- This is called tail call operation.
![[Pasted image 20250916205016.png|400]]


---
# Trees

![[Pasted image 20251006191131.png|300]]

In relational database their are two types of indexes:
1. Keys of hashmap
2. ordered operations - balanced search (red-black tree)

Using HashMap, priority queue, arrays , linked list it is difficult to optimally find elements in a range and will take roughly O(N²) in worst case
![[Pasted image 20251006192124.png|300]]
- As you need to compare each key to check with the range bcz it's not necessary values in range is present among those elements or not.

# Binary Search Tree
![[Pasted image 20251006195242.png|300]]
structure of a node in binary tree
![[Pasted image 20251006195919.png|200]]

Time complexity chart
![[Pasted image 20251006195311.png|300]]

- All the keys in left side will be lesser and all the keys to the right side is greater than
- It's kind of like a self referential data structure. In which one structure points to another structure.
- One often use recursion as it's easier to understand the sub problems.
- Binary search tree doesn't guarantee that tree's structure will be always balanced or near balanced.
	![[Pasted image 20251006200127.png|300]]
	- It could be Linear as well leaning to left or right.
- If your use case doesn't involve delete operation then based on research if you are using real world data your tree structure height will be `1.39 log₂N`.
	- But since their are no drawbacks or overhead in using Balanced Search Tree and it guarantees the height of tree to be exactly `log₂N` therefore Balanced Search Tree are preferred over Binary Search Tree.
- Balanced Search Tree are used in real world instead of Binary Search Tree.

- Base case for put operation in BST
	![[Pasted image 20251006202751.png|300]]
	- If in a tree we reached null then we return a new node with the key and value we want to put
	- In case the key already exists then just update the value at that key.
	![[Pasted image 20251006202930.png|300]]


How to implement delete node in Tree
![[Pasted image 20251007200415.png|300]]
![[Pasted image 20251007201244.png|300]]
![[Pasted image 20251007200953.png|300]]


# Floor

![[Pasted image 20251007201857.png|300]]

# Implement the delete code for any node
![[Pasted image 20251007204028.png]]


# Rank
- Rank of tree determines the number of elements less than it.
- One approach is  we can use inorder traversal and get the elements in sorted order and find the position 
- Another approach is maintain a variable in class of node itself which tells all the elements under that element including itself.
	- This approach helps to get size of tree at any node as well.
	- But this also helps in finding rank as now if you know the count in one branch whether left or right then using basic maths you can get size of right side too without traversing. So we just need to traverse only in one side and hence time complexity becomes log n.
	- So while insertion of new element  we have to update that variable while back tracking.
	![[Pasted image 20251007210440.png|300]]


---
![[Pasted image 20251013201912.png]]

![[Pasted image 20251013201941.png]]


- Euler Cycle


- Adjacency list vs adjacency Matrix
	- list provides better space utilization.
	- matrix is faster due to less overhead.

# Directed Graphs
# Implementation of Graph with linkedlist

```java
import java.util.LinkedList;

public class Graph{
  private int V;
  private int E;
  private LinkedList<Integer>[] adj;
  public Graph(int V) {
    this.V = V;
    // Initializing the array. Size of array is number of vertices
    this.adj = new LinkedList[V];
    this.E = 0;
    for (int i = 0; i < V; i++) {
      // Initializing each adjacency list.	    
      this.adj[i] = new LinkedList<Integer>();
    }
  }

  public void addEdge(int v, int w) {
     this.adj[v].add(w);
     this.adj[w].add(v);
     this.E++;
  }

  public int V() { 	  	  
    return this.V;
  }

  public int E() {
    return this.E;
  }

  public Iterable<Integer> adj(int v) {
    return this.adj[v];
  }
}
```

Frequently asked Interview question is to find if two vertices are connected or not .

## BFS implementation

```java
import java.util.Queue;
import java.util.LinkedList;
import java.util.Stack;

public class BFS{
  private boolean marked[];
  private int[] edgeTo;  
  int s;
  BFS(Graph g, int s) {
    this.marked = new boolean[g.V()];
    this.edgeTo = new int[g.V()];
    this.s = s;
    bfs(g, s);
  }
  
  private void bfs(Graph g, int v) {
    Queue<Integer> q = new LinkedList<Integer>();
    q.add(v);
    marked[v] = true;

    while (!q.isEmpty()) {
      int w = q.poll();

      for (int z : g.adj(w)) {
	if (marked[z]) continue;
	marked[z] = true;
	edgeTo[z] = w;
	q.add(z);
      }
    }
  }

  // To find if vertex v is connnected to source node
  public boolean connected(int v) {
    return this.marked[v];
  }

  // Printing the shortest path
  public void printPath(int v) {
    if (!connected(v)) return;

    Stack<Integer> path = new Stack<>();
    for (int w = v; w != s; w = edgeTo[w]) {
       path.push(w);
    }
    path.push(s);

    while (!path.isEmpty()) {
      System.out.print(path.pop());
      if (path.size() > 1) System.out.print(" -> ");
    }
    System.out.println();
  }
}
```

HW : Implement and test DFS




# Connected Components
![[Pasted image 20251028191355.png|300]]

###### Related Questions
![[Pasted image 20251028191830.png|200]]
- Count number of islands.
- find second larges islands



Using DFS
![[Pasted image 20251028193351.png|400]]

```java
public class ConnectedComponents {
  private boolean[] marked;
  private int count;
  private int[] id;

  ConnectedComponents(Graph g) {
    this.marked = new boolean[g.V()];
    this.id = new int[g.V()];
    this.count = 0;    

    for (int v = 0; v < g.V(); v++) {
      if (!marked[v]) {
        dfs(g, v);
	count++;
      }
    }
  }

  // Is vertex v and w are connected
  public boolean connected(int v, int w) {
    return this.id[v] == this.id[w];
  }

  // Number of components in Graph
  public int count() {
    return this.count;
  }

  //Given a vertex which component it is part of
  public int id(int v) {
    return this.id[v];
  }

  private void dfs(Graph g, int v) {
    marked[v] = true;
    id[v] = count;

    for (int w : g.adj(v)) {
      if (!marked[w]) {
        dfs(g, w);
      }
    }
  }

  public static void main(String[] args) {
    Graph g = new Graph(9);
    g.addEdge(1, 2);
    g.addEdge(2, 3);
    g.addEdge(1, 3);

    g.addEdge(4, 5);
    g.addEdge(5, 6);
    g.addEdge(4, 6);

    g.addEdge(7, 8);

    ConnectedComponents cc = new ConnectedComponents(g);

    assert cc.connected(1, 3) == true;
    assert cc.connected(1, 4) == false;
    assert cc.connected(7, 4) == false;
    assert cc.connected(7, 1) == false;
    assert cc.connected(7, 8) == true;
    assert cc.connected(4, 5) == true;

    assert cc.count() == 4;
  }
}
```


HW
- Identify a Bipartite Graph. Then find two sets of vertices differentiated as per Bipartite graph.
	![[Pasted image 20251028194905.png|300]]
	
- Find Cycle in graph
	![[Pasted image 20251028195047.png|300]]
- Find Euler Cycle in Graph
	- It's a graph processing algorithm


>RESOURCES for CORE
>- https://www.youtube.com/results?search_query=georgia+tech+computer+networking
>- https://www.youtube.com/playlist?list=PLTsf9UeqkReZbK7xqIYn_mXmsQZIb011T
>- https://www.udacity.com/blog/2014/07/new-course-computer-networking.html
>- 
# Directed Graphs

![[Pasted image 20251103194538.png|400]]

- Example : bank has given loan to customer but customer is not the one that gives loan to bank.
- Cab
	![[Pasted image 20251103194658.png|300]]
- Web Pages
	![[Pasted image 20251103194745.png|300]]
	- It can have bidirectional edge or one way edge.

##### HW
Design a Web Crawler and it's variation. (project with graphs)
- white list those pages which you want your crawler to visit.
- black list those pages which you don't want to visit.
- robot.text file or some other format  file  prevent the crawler from crawling sites with sensitive content.
# Problems in Graph

![[Pasted image 20251103200021.png|400]]
- Strong Connectivity
	![[Pasted image 20251103195934.png|300]]
- Transitive Closure
- Page Rank

# Topological Sort

![[Pasted image 20251103201918.png|300]]


**Example**
![[Pasted image 20251103202435.png|100]]

![[Pasted image 20251103210025.png|100]]
Topological Order:
![[Pasted image 20251103202552.png|200]]
or other combination
![[Pasted image 20251103205450.png]]

![[Pasted image 20251103203246.png|200]]

- There should be no cycle in graph otherwise Topological sort is not possible.
- Based on order in which we add the edges the result may vary as there  are multiple combination possible of Topological sort.
Topological Sort
```java
import java.util.Stack;
public class TopologicalSort {
  private boolean[] marked;
  private Stack<Integer> reversePostOrder;

  public TopologicalSort(DirectedGraph g) {
    reversePostOrder = new Stack<Integer>();
    marked = new boolean[g.V()];
    
    for (int i = 0; i < g.V(); i++) {
      if (!marked[i]) {
      	dfs(g, i);
      }
    }    
  }

  private void dfs(DirectedGraph g, int v) {
    marked[v] = true;

    for (int w : g.adj(v)) {
      if (!marked[w]) {
	dfs(g, w);
      }
    }
    reversePostOrder.push(v);
  }
  public Stack<Integer> order() {
    return this.reversePostOrder;
  }

  public static void main(String[] args) {
    DirectedGraph dg = new DirectedGraph(7);

    dg.addEdge(0, 5);
    dg.addEdge(0, 2);
    dg.addEdge(0, 1);
    dg.addEdge(1, 4);
    dg.addEdge(3, 6);
    dg.addEdge(3, 5);
    dg.addEdge(3, 4);
    dg.addEdge(5, 2);
    dg.addEdge(6, 4);
    dg.addEdge(6, 0);
    dg.addEdge(3, 2);
    TopologicalSort ts = new TopologicalSort(dg);
    Stack<Integer> st = ts.order();
    while (!st.isEmpty()) {
      System.out.print(st.pop() + " ");
    }
    System.out.println();
  }
}

```



---
- If i run a light program like print hello world with empty physical memory of 16GB then will it use virtual memory
	- Short answer: **Yes, but only a tiny bit — because virtual memory is _always_ used**, even when you have **16GB free RAM** and the program is very light.
	- If a system supports virtual memory then every application that runs on it will use virtual memory , it's not selective every process must use it.

![[Pasted image 20251117194102.png|300]]
16 Exabytes of data equivalent to 1000 petabytes
![[Pasted image 20251117194136.png|300]]


Problems
- How does everything fits?
	- Like memory size is so big compared to ram. Then how a processes from main memory fit in ram.
- What goes where?
	- How mapping of process happens from main memory to ram.
	![[Pasted image 20251117204204.png|300]]
- How to protect?
- How to share?
	- The bits which makes up the page table also has addition bits telling about permissions like Read, Write etc.
	![[Pasted image 20251117204517.png|300]]

#### Indirection
It is jokingly said that any Computer science problem can be solved using indirection.
![[Pasted image 20251117200020.png|400]]

Similarly indirection is achieved in OS by mapping Virtual Address to Physical address
![[Pasted image 20251117200343.png|300]]
![[Pasted image 20251117200540.png|300]]

- If our OS is 64 bit architecture then each process thinks that they have the complete memory for itself like 16 Exabytes here.
- Runtime/Compiler system will write in physical memory.
- This indirection information will be stored in page table.
- There is one page table per process in a system.


![[Pasted image 20251117201550.png|400]]
- Now addresses in RAM is different, Disk is different so who does this translation.
	- This translation is done by MMU (Memory Management Unit) 
		- This translation happens in hardware side not software side hence it's faster.
		![[Pasted image 20251117201747.png|300]]


- Data is transferred page by page not byte by byte in OS.
- CPU reads data only from physical memory and in case data is not in RAM then it needs to first be brought in RAM.

- A pages can be of different size like 256 bits or 4 MB and when data is accessed it's not just reference to data that comes in RAM but the whole page itself as CPU only reads data from RAM.
![[Pasted image 20251117202319.png]]

- RAM is kind of a cache itself as it speeds up the process quite a bit.
- Penalty for accessing data from ram is 33 times than that of L1,L2 cache and of disk is10000 time than that of L1,L2 cache.
	![[Pasted image 20251117202534.png|400]]

- Virtual Pages are also stored in non- contiguous fashion.
	![[Pasted image 20251117203448.png]]


![[Pasted image 20251117203541.png|400]]

![[Pasted image 20251117203815.png|300]]
- Process of page fault


# Page Table
![[Pasted image 20251117204605.png|300]]

![[Pasted image 20251117204847.png]]
- Now to make this process faster TLB (Translation Look aside buffer) comes into picture.
- TLB is basically an small hardware cache.
- TLB has has around 128 to 256 entries depending on your system's TLE.

![[Pasted image 20251118191908.png|300]]

![[Pasted image 20251118192136.png|300]]
- TLB directly stores the mapping of physical address from virtual address and hence it need not to worry about page number or  offset.
- Data in TLB does not directly come from disk but it has to take a route of ram then unified cache then to the finally to TLB cache of your cpu.


![[Pasted image 20251118194540.png|300]]

> Who decides the bit architecture?
> 
> The "bitness" of a computer is defined by the **CPU's Integer Register Size** (also called Word Size).1
> - **Registers:** If the internal General Purpose Registers are **64 bits** wide, it is a 64-bit architecture.2
    - **What this means:** The CPU can process a 64-bit integer in a single clock cycle.3
    - **Virtual Address:** Because registers are used to hold memory pointers, the register size dictates the size of the **Virtual Address**. A 64-bit CPU uses 64-bit pointers, allowing it to "see" (address) a practically infinite amount of virtual memory ($2^{64}$).

- For 8 bit virtual address.
	![[Pasted image 20251118195233.png|300]]

![[Pasted image 20251118195425.png]]

![[Pasted image 20251118195553.png|400]]
This is what a TLB looks like

![[Pasted image 20251118200137.png]]

# SQL

Here is the database
```sql
/* Delete the tables if they already exist */
drop table if exists Movie;
drop table if exists Reviewer;
drop table if exists Rating;

/* Create the schema for our tables */
create table Movie(mID int, title text, year int, director text);
create table Reviewer(rID int, name text);
create table Rating(rID int, mID int, stars int, ratingDate date);

/* Populate the tables with our data */
insert into Movie values(101, 'Gone with the Wind', 1939, 'Victor Fleming');
insert into Movie values(102, 'Star Wars', 1977, 'George Lucas');
insert into Movie values(103, 'The Sound of Music', 1965, 'Robert Wise');
insert into Movie values(104, 'E.T.', 1982, 'Steven Spielberg');
insert into Movie values(105, 'Titanic', 1997, 'James Cameron');
insert into Movie values(106, 'Snow White', 1937, null);
insert into Movie values(107, 'Avatar', 2009, 'James Cameron');
insert into Movie values(108, 'Raiders of the Lost Ark', 1981, 'Steven Spielberg');

insert into Reviewer values(201, 'Sarah Martinez');
insert into Reviewer values(202, 'Daniel Lewis');
insert into Reviewer values(203, 'Brittany Harris');
insert into Reviewer values(204, 'Mike Anderson');
insert into Reviewer values(205, 'Chris Jackson');
insert into Reviewer values(206, 'Elizabeth Thomas');
insert into Reviewer values(207, 'James Cameron');
insert into Reviewer values(208, 'Ashley White');

insert into Rating values(201, 101, 2, '2011-01-22');
insert into Rating values(201, 101, 4, '2011-01-27');
insert into Rating values(202, 106, 4, null);
insert into Rating values(203, 103, 2, '2011-01-20');
insert into Rating values(203, 108, 4, '2011-01-12');
insert into Rating values(203, 108, 2, '2011-01-30');
insert into Rating values(204, 101, 3, '2011-01-09');
insert into Rating values(205, 103, 3, '2011-01-27');
insert into Rating values(205, 104, 2, '2011-01-22');
insert into Rating values(205, 108, 4, null);
insert into Rating values(206, 107, 3, '2011-01-15');
insert into Rating values(206, 106, 5, '2011-01-19');
insert into Rating values(207, 107, 5, '2011-01-20');
insert into Rating values(208, 104, 3, '2011-01-02');
```

### Questions
Q1. Find the titles of all movies directed by Steven Spielberg.  
Q2. Find all years that have a movie that received a rating of 4 or 5, and sort them in increasing order.  
Q3. Find the titles of all movies that have no ratings.  
Q4. Some reviewers didn't provide a date with their rating. Find the names of all reviewers who have ratings with a NULL value for the date.  
Q5. Write a query to return the ratings data in a more readable format: reviewer name, movie title, stars, and ratingDate. Also, sort the data, first by reviewer name, then by movie title, and lastly by number of stars.  
Q6. For all cases where the same reviewer rated the same movie twice and gave it a higher rating the second time, return the reviewer's name and the title of the movie.  
Q7. For each movie that has at least one rating, find the highest number of stars that movie received. Return the movie title and number of stars. Sort by movie title.  
Q8. For each movie, return the title and the 'rating spread', that is, the difference between highest and lowest ratings given to that movie. Sort by rating spread from highest to lowest, then by movie title.  
Q9. Find the difference between the average rating of movies released before 1980 and the average rating of movies released after 1980. (Make sure to calculate the average rating for each movie, then the average of those averages for movies before 1980 and movies after. Don't just calculate the overall average rating before and after 1980.)  
Q10. Find the names of all reviewers who rated Gone with the Wind.  
Q11. For any rating where the reviewer is the same as the director of the movie, return the reviewer name, movie title, and number of stars.  
Q12. Return all reviewer names and movie names together in a single list, alphabetized. (Sorting by the first name of the reviewer and first word in the title is fine; no need for special processing on last names or removing "The".)  
Q13. Find the titles of all movies not reviewed by Chris Jackson.  
Q14. For all pairs of reviewers such that both reviewers gave a rating to the same movie, return the names of both reviewers. Eliminate duplicates, don't pair reviewers with themselves, and include each pair only once. For each pair, return the names in the pair in alphabetical order.  
Q15. For each rating that is the lowest (fewest stars) currently in the database, return the reviewer name, movie title, and number of stars.  
Q16. List movie titles and average ratings, from highest-rated to lowest-rated. If two or more movies have the same average rating, list them in alphabetical order.  
Q17. Find the names of all reviewers who have contributed three or more ratings.  
Q18. Some directors directed more than one movie. For all such directors, return the titles of all movies directed by them, along with the director name. Sort by director name, then movie title.  
Q19. Find the movie(s) with the highest average rating. Return the movie title(s) and average rating.  
Q20. For each director, return the director's name together with the title(s) of the movie(s) they directed that received the highest rating among all of their movies, and the value of that rating. Ignore movies whose director is NULL.


#### Commands to setup SQL Lite
```bash
sudo apt install sqlite3          // to install
sqlite3 db_name.db < sql_file.sql // to create a database
sqlite3 db_name.db                // to use the database
```

#### Useful commands in SQL Lite
```sql
.exit        // to exit the sqlite3 terminal
.shell clear // to clean the screen
.mode box    // for table format output
```




# JOINS

- Cross Join
	![[Pasted image 20251202191226.png|300]]
	![[Pasted image 20251202191336.png|300]]

	- Number of Resultant will be m x n   
	![[Pasted image 20251202191304.png|300]]


- Natural Join
	![[Pasted image 20251202191634.png|300]]
	![[Pasted image 20251202191846.png|400]]
	- It is not recommended as in case someone changes the column name then it will not work as intended.
	- Hence explicitly use the type of join as needed.


- Inner join
	![[Pasted image 20251202192316.png|400]]
- left outer join
	![[Pasted image 20251202192626.png]]
	- developer tries to ensure that their is no null value.
- right outer join
	![[Pasted image 20251202192858.png|300]]
- full outer join
	![[Pasted image 20251202193136.png]]


### Query Optimization

While using aggregation function like MIN , MAX on particular column then that column should be mentioned in aggregation like in group by otherwise you cannot use it

select SUM(A.A1), A.A1, B.A1
![[Pasted image 20251202195559.png|300]]


> Resources : edx - stanford - Jenifer Widom



# System Design

Question:
1. You have a website which is currently running on a single web server on PostgreSQL database. Web Server, application server and database are installed on the same virtual machine (8 GB RAM, 100 GB HHD, 4 core CPU). It was serving around 10000 users per day.. In the holiday season you expect that number to go to 1 million per day. How would you scale your web application?
2. How would you check if  their is latency in the network and it is causing a bottle neck? How will you determine if their is a packet loss in the network which is causing the issue.



# Why load balancer?
1. Load distribution
2. Reliability
3. Scalability
4. Security - clients are only talking with load balancer they don't know what's inside the packet(ip, content, what they do etc.).
- It runs on application layer and transport layer. But it can happen on network
	- In transport layer it contains IP and Port and it is not worried about packet content but only the header content. It worries about IP address , port , protocols but not the content.
	- Why application layer? here LB is not performing any kind of intelligence
	![[Pasted image 20251213194221.png|400]]
	At application layer there can be multiple ways to route:
		- static
			- Round Robin
			- Hash
			- Weighted Round Robin (based on server performing capacity )
		- dynamic
			- Least connections
			- Resource Based
			- Least Response Time
- It Routes request based on IP address to different set of addresses.
- Load Balancer does provide sticky sessions
	- It was done earlier with cookies but now JWT is used instead of sticky session.
	- There will be time limit to each session.
	- As long as session is valid user request will reach the same server.
- Path-Based Routing
	![[Pasted image 20251213200053.png|200]]
- In Load balancer as data is decrypted so it can either pass the decrypted data or re-encrypt it before sending.
- Load Balancer also uses firewall to prevent DDOS attack to a particular server.
![[Pasted image 20251213200333.png|400]]


psql handles the connection to PostgreSQL.

![[Pasted image 20251213201749.png]]


# Types of Load Balancer
- Types of load Balancer:
	- Load Balancer at application layer
	- Load Balancer at Transport Layer
- HA Proxy (most popular) -> Application , Transport
- NGINX -> Application, Transport

# Vagrant 
- Used to run and manage VM's.
- Task
	- Run 3 VM
	- Install Software
		- ha proxy
		- PostgreSQL
		- nginx
	- ha proxy
		- mode: tp (transfer to database server in transport layer)
		- mode: http (application layer)

![[Pasted image 20251213202530.png]]

![[Pasted image 20251213202833.png]]
Load balancer - 192.168.34.10
Database Server : port 5432 - private network : 192.168.34.12 -> TL
HTTP Server Port: 80 private network 192.168.34.11
Browser - http://localhost:8081 -> http://192.168.34.10:80
Database client -
	a. `psql -h localhost -p 54320` -> `psql -h 192.168.34.10 -p 54320` port forwarding.


# what is firewall?
- Security appliances used to monitor incoming and outgoing traffic
- Firewalls are present in router where it is configured to block traffic which arrives at random ports. So if any port is not whitelisted and no application is running there then the incoming traffic to such ports are by default configured to block.
- Any firewall you use uses good amount of memory. So, before using them one should know it's memory footprints or performance footprints.

##### ufw firewall utility
- This firewall is present at transport layer and it didn't read the content of the packets but based on ports and ip address  filter requests.
![[Pasted image 20251216192407.png|500]]
- By default there is rate limit request of 6 request, if any client makes more than 6 request then that client will not be able to connect to server for some time.

![[Pasted image 20251216192701.png|300]]


# Software needed to be installed in a server for security
![[Pasted image 20251216194041.png|300]]
`crs` provides the rules whereas `libapache2-mad-security2` processes the rules and ensure security


>Google cloud armor also used as a firewall. 
# Types of attacks
- SQL Injection
	![[Pasted image 20251216193625.png|400]]


https://docs.google.com/spreadsheets/d/1kx1gNGHYFTcZ0kmV_1vrlhwbuF0jv67fJIqSkBrpp5I/edit?gid=0#gid=0


# SQL / No SQL

![[Pasted image 20260120192227.png]]

ACID vs BASE

# No SQL databases
- Document
- Wide column database
	- Big Table
	- Pioneered by Google
		- High level mechanism: it can have multiple columns for each alphabet. So using boolean operation it can store name of website by make true the alphabet that is in name of website kind of like tries. So for 1000 websites it might be storing 1000 words for each. 
			![[Pasted image 20260120194018.png|300]]
			- So wide column database are used when you care about speed and not care about the space required.
		- But in sparse database we can just store the characters as in name of website directly which saves space.
			![[Pasted image 20260120194107.png|300]]
- Key Value databases
- Graph databases
	- Neo4j
	- Time series database
		![[Pasted image 20260120194807.png|300]]
- Data Warehouses (not exactly database)
	- Ex: MongoDB


![[Pasted image 20260120195644.png|400]]

- Spanner 
	- It is a SQL database but it can scale out means it support horizontal scaling.
	- So,this database remains consistent and performant while scaling upto Peta bytes of database often said as New SQL.
	- It provides performance like No SQL with consistency like SQL database.
	- Why not to choose to it then?
		- It uses lot of expensive hardware and machinery. It's cost goes upto $9000 to $15000.
		- some concept of atomic clock is used where it store very precise time till each nano second for more details checkout the documentation😅

**Google Spanner** is used when you need a database that combines:
> **relational semantics + global scale + strong consistency**
It exists for a _very specific class of problems_ that most databases cannot solve well.


![[Pasted image 20260120202118.png]]

![[Pasted image 20260120202658.png]]
# Big Query
- It's a SQL database but can use maximum data.
	![[Pasted image 20260120202434.png|200]]
- In mongo db database you want be running analytical queries like which city has maximum number of complaints or which city has maximum number of rides so such queries are answered by joining all the data. 


![[Pasted image 20260217192229.png]]
![[Pasted image 20260217192225.png]]

Describe your projects and your achievements.

![[Pasted image 20260217192258.png]]