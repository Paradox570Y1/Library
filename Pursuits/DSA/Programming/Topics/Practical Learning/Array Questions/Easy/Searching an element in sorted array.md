
Given an array **arr[]** sorted in ascending order of size **N** and an integer **K**. Check if K is present in the array or not.

  
**Example 1:**

**Input:**
N = 5, K = 6
arr[] = {1,2,3,4,6}
**Output:** 1
**Exlpanation:** Since, 6 is present in 
the array at index 4 (0-based indexing),
output is 1.

**Example 2:**

**Input:**
N = 5, K = 2
arr[] = {1,3,4,5,6}
**Output:** -1
**Exlpanation:** Since, 2 is not present 
in the array, output is -1.

**Your Task:**  
You don't need to read input or print anything. Complete the function **searchInSorted()** which takes the sorted array arr[], its size N and the element K as input parameters and returns 1 if K is present in the array, else it returns -1. 

  
**Expected Time Complexity:** O(Log N)  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
1 <= N <= 106  
1 <= K <= 106  
1 <= arr[i] <= 106
#### Optimal
```cpp
class Solution{
    public:
    // Function to find element in sorted array
    // arr: input array
    // N: size of array
    // K: element to be searche
    int searchInSorted(int arr[], int N, int K) 
    { 
    
       // Your code here
       int i=0,j=N-1;
       int mid;
       while(i<=j){
           int mid=(i+j)/2;
           if(K>arr[mid]){
               i=mid+1;
           }
           else if(K<arr[mid]){
               j=mid-1;
           }
           else return 1;
       
       }
       return -1;
       
    }
};
```

