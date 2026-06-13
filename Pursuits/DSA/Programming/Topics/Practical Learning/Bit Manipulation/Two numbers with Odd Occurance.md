[Link](https://www.geeksforgeeks.org/problems/two-numbers-with-odd-occurrences5846/1)
### Two numbers with odd occurrences

Difficulty: **Medium**Accuracy: **49.49%**Submissions: **67K+**Points: **4**

Given an unsorted array, **Arr**[] of size **N** and that contains **even** number of occurrences for all numbers except two numbers. Find the two numbers in **decreasing** order which has **odd** occurrences.  
  
**Example 1:**

**Input:**
N = 8
Arr = {4, 2, 4, 5, 2, 3, 3, 1}
**Output:** {5, 1} 
**Explanation:** 5 and 1 have odd occurrences.

  
**Example 2:**

**Input:**
N = 8
Arr = {1 7 5 7 5 4 7 4}
**Output:** {7, 1}
**Explanation:** 7 and 1 have odd occurrences.

  
**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **twoOddNum()** which takes the array **Arr[]** and its size **N** as input parameters and returns the two numbers in decreasing order which have odd occurrences.

  
**Expected Time Complexity:** O(N)  
**Expected Auxiliary Space:** O(1)

  
**Constraints:**  
2 ≤ N ≤ 106  
1 ≤ Arri ≤ 1012

Try more examples

```java
class Solution
{
    public int[] twoOddNum(int Arr[], int N)
    {
        // code here
        int xorOfAns = 0;
        for(int i=0;i<N;i++){
            xorOfAns^=Arr[i];
        }
        int bitmask = xorOfAns & -xorOfAns;
        //rightmost set bit of xorOfAns , 2 raise to power of that bit
        int n1=0,n2=0;
        for(int i=0;i<N;i++){
            if((Arr[i]&bitmask)>0)n1^=Arr[i];
            else n2^=Arr[i];
        }
        if(n1>n2)return new int[]{n1,n2};
        return new int[]{n2,n1};
    }
}
```