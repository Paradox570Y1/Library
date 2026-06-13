# Maximum Sum Combinations

[Link](https://www.interviewbit.com/problems/maximum-sum-combinations/)

**Problem Description**  
Given two equally sized 1-D arrays **A, B** containing **N** integers each.
A **sum combination** is made by adding one element from array **A** and another element of array **B**.
Return the **maximum C valid sum combinations** from all the possible sum combinations.
  
**Problem Constraints**  

1 <= N <= 105
1 <= A[i] <= 105
1 <= C <= N
  
**Input Format**  

First argument is an one-dimensional integer array **A** of size **N**.
Second argument is an one-dimensional integer array **B** of size **N**.
Third argument is an integer **C**.
  
**Output Format**  
Return a one-dimensional integer array of size **C** denoting the top C maximum sum combinations.

**NOTE:**
The returned array must be sorted in non-increasing order.

  
**Example Input**  

Input 1:
 A = [3, 2]
 B = [1, 4]
 C = 2

Input 2:
 A = [1, 4, 2, 3]
 B = [2, 5, 1, 6]
 C = 4
  
**Example Output**  
Output 1:
 [7, 6]

Output 1:
 [10, 9, 9, 8]

# Brute

```java
public class Solution {
    public int[] solve(int[] A, int[] B, int C) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        for(int i=0;i<A.length;i++){
            for(int j=0;j<B.length;j++){
                minHeap.offer(A[i]+B[j]);
                if(minHeap.size()>C)minHeap.poll();
            }
        }
        
        int[] ans = new int[C];
        for(int i=C-1;i>=0;i--){
            ans[i] = minHeap.poll();
        }
        return ans;
    }
}
```

# Optimal

```java
public class Solution {
    class Element{
        int sum,idx1,idx2;
        Element(int sum, int idx1, int idx2){
            this.sum = sum;
            this.idx1 = idx1;
            this.idx2 = idx2;
        }
    }
    public int[] solve(int[] A, int[] B, int C) {
        Arrays.sort(A);
        Arrays.sort(B);
        int n = A.length-1, m = B.length-1;
        HashSet<String> visited = new HashSet<>();
        PriorityQueue<Element> maxHeap = new PriorityQueue<>((a,b)-> b.sum - a.sum);
        maxHeap.offer(new Element(A[n]+B[m],n,m));
        int i = 0;
        int[] ans = new int[C];
        while(i<C && !maxHeap.isEmpty()){
            Element root = maxHeap.poll();
            ans[i++]  = root.sum;
            int a = root.idx1;
            int b = root.idx2;
            if(a>0 && !visited.contains((a-1)+","+b)){
                maxHeap.offer(new Element(A[a-1]+B[b],a-1,b));
                visited.add((a-1)+","+b);
            }
            if(b>0 && !visited.contains(a+","+(b-1))){
                maxHeap.offer(new Element(A[a]+B[b-1],a,b-1));
                visited.add(a+","+(b-1));
            }
        }
        return ans;
    }
	}
```