[Link](https://www.geeksforgeeks.org/problems/convert-min-heap-to-max-heap-1666385109/1)
Difficulty: **Medium**Accuracy: **55.0%**Submissions: **18K+**Points: **4**Average Time: **20m**

You are given an array **arr** of **N** integers representing a min Heap. The task is to convert it to max Heap.

A max-heap is a complete binary tree in which the value in each internal node is greater than or equal to the values in the children of that node. 

**Example 1**:

**Input**:
N = 4
arr = [1, 2, 3, 4]
**Output**:
[4, 2, 3, 1]
**Explanation**:

The given min Heap:

          1
        /   \
      2       3
     /
   4

Max Heap after conversion:

         4
       /   \
      2     3
    /
   1

**Example 2**:

**Input**:
N = 5
arr = [3, 4, 8, 11, 13]
**Output**:
**[**13, 11, 8, 3, 4]
**Explanation**:

The given min Heap:

          3
        /   \
      4      8
    /   \ 
  11     13

Max Heap after conversion:

          13
        /    \
      11      8
    /   \ 
   3     4

**Your Task:**  
Complete the function int **convertMinToMaxHeap**(), which takes integer N and array represented minheap as input and converts it to the array representing maxheap. You don't need to return or print anything, modify the original array itself.

**Note**: Only an unique solution is possible under the expected time complexity.

**Expected Time Complexity**: O(N * log N)  
**Expected Auxiliary Space**: O(N)

  
**Constraints:**

1 <= N <= 105  
1 <= arr[i] <= 109



```java
class Solution {
    static void downHeap(int[] arr,int i,int n){
        int min = i;
        int left = 2*i+1;
        int right = 2*i+2;
        if(left<n && arr[min]<arr[left])min = left;
        if(right<n && arr[min] < arr[right])min = right;
        if(min!=i){
            int temp = arr[min];
            arr[min] = arr[i];
            arr[i] = temp;
            downHeap(arr,min,n);
        }
    }
    static void convertMinToMaxHeap(int N, int arr[]) {
    // code here
        int p = (N-1)/2;
        for(int i=p;i>=0;i--){
            downHeap(arr,i,N);
        }
  }
}
```