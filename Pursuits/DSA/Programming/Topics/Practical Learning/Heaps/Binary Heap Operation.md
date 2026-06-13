[Link](https://www.geeksforgeeks.org/problems/operations-on-binary-min-heap/1)
Difficulty: **Medium**Accuracy: **22.3%**Submissions: **103K+**Points: **4**Average Time: **15m**

A **binary heap** is a Binary Tree with the following properties:  
**1)** Its a _complete tree_ (All levels are completely filled except possibly the last level and the last level has all keys as left as possible). This property of Binary Heap makes them suitable to be stored in an array.

**2)** A Binary Heap is either **Min Heap** or **Max Heap**. In a _Min Binary Heap_, the key at the _root_ must be _minimum_ among all keys present in Binary Heap. The same property must be recursively true for all nodes in Binary Tree. Max Binary Heap is similar to MinHeap.

You are given an empty Binary Min Heap and some queries and your task is to implement the three methods **insertKey,  deleteKey,**  and **extractMin** on the Binary Min Heap and call them as per the query given below:  
**1)** _1  x_  (a query of this type means to insert an element in the min-heap with value x )  
**2)** _2  x_  (a query of this type means to remove an element at position x from the min-heap)  
**3)** _3_  (a query like this removes the min element from the min-heap and prints it ).

**Examples :**

**Input:** Q = 7
Queries:
insertKey(4)
insertKey(2)
extractMin()
insertKey(6)
deleteKey(0)
extractMin()
extractMin()
**Output:** [2, 6, -1]
**Explanation:** In the first test case for
query 
insertKey(4) the heap will have  {4}  
insertKey(2) the heap will be {2 4}
extractMin() removes min element from 
             heap ie 2 and prints it
             now heap is {4} 
insertKey(6) inserts 6 to heap now heap
             is {4 6}
deleteKey(0) delete element at position 0
             of the heap,now heap is {6}
extractMin() remove min element from heap
             ie 6 and prints it  now the
             heap is empty
extractMin() since the heap is empty thus
             no min element exist so -1
             is printed.

**Input:**
Q = 5
Queries:
insertKey(8)
insertKey(9)
deleteKey(1)
extractMin()
extractMin()
**Output:** [8, -1]

**Constraints:**  
1 <= **Q** <= 104  
1 <= **x** <= 104


```java
int extractMin()
    {
        // Your code here.
        if(heap_size==0)return -1;
        int ans = harr[0];
        heap_size--;
        if(heap_size != 0){
            harr[0] = harr[heap_size];
            MinHeapify(0); //downHeap
        }
        return ans;
    }
```

```java
void insertKey(int k) 
    {
        // Your code here.
        decreaseKey(heap_size,k);//insert at heap_size and upHeap
        heap_size++;
    }
```

```java
void deleteKey(int i) 
    {
        decreaseKey(i,Integer.MIN_VALUE);
        extractMin();
}
OR
void deleteKey(int i) {
        if (i >= heap_size) return;
        int last = harr[heap_size - 1];
        harr[i] = last;
        heap_size--;
        if (i != 0 && harr[i] < harr[parent(i)]) {
            // Percolate up
            while (i != 0 && harr[parent(i)] > harr[i]) {
                int temp = harr[i];
                harr[i] = harr[parent(i)];
                harr[parent(i)] = temp;
                i = parent(i);
            }
        } else {
            MinHeapify(i);
        }
    }
```