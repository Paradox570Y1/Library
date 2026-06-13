Difficulty: **Medium**Accuracy: **67.25%**Submissions: **110K+**Points: **4**Average Time: **45m**

Given **k** sorted arrays arranged in the form of a matrix of size **k** * **k**. The task is to merge them into one sorted array. Return the merged sorted array ( as a pointer to the merged sorted arrays in **cpp,** as an ArrayList in **java,** and list in **python**).

  
**Examples :**

**Input:** k = 3, arr[][] = {{1,2,3},{4,5,6},{7,8,9}}
**Output:** 1 2 3 4 5 6 7 8 9
**Explanation:** Above test case has 3 sorted arrays of size 3, 3, 3 arr[][] = [[1, 2, 3],[4, 5, 6],[7, 8, 9]]. The merged list will be [1, 2, 3, 4, 5, 6, 7, 8, 9].

**Input:** k = 4, arr[][]={{1,2,3,4},{2,2,3,4},{5,5,6,6},{7,8,9,9}}
**Output:** 1 2 2 2 3 3 4 4 5 5 6 6 7 8 9 9 
**Explanation:** Above test case has 4 sorted arrays of size 4, 4, 4, 4 arr[][] = [[1, 2, 2, 2], [3, 3, 4, 4], [5, 5, 6, 6], [7, 8, 9, 9 ]]. The merged list will be [1, 2, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 8, 9, 9].

**Expected Time Complexity:** O(k2*Log(k))  
**Expected Auxiliary Space:** O(k2)

**Constraints**:  
1 <= k <= 100


```java
class Solution
{
    public static ArrayList<Integer> mergeKArrays(int[][] arr,int K) 
    {
        ArrayList<Integer> ans= new ArrayList<>();
        for(int n:arr[0])ans.add(n);
        int len=K;
        for(int i=1;i<arr.length;i++){
            merge(arr[i],ans,K,len);
            len+=K;
        }
        return ans;
    }
    static void merge(int[] arr,ArrayList<Integer> li,int n,int m){
        ArrayList<Integer> temp = new ArrayList<>();
        int st1 = 0,st2=0;
        while(st1<n && st2<m){
            if(arr[st1]>li.get(st2))temp.add(li.get(st2++));
            else temp.add(arr[st1++]);
        }
        while(st1<n)temp.add(arr[st1++]);
        while(st2<m)temp.add(li.get(st2++));
        for(int i=0;i<m;i++){
            li.set(i,temp.get(i));
        }
        for(int i=m;i<m+n;i++){
            li.add(temp.get(i));
        }
    }
}
```


# Using Heap (Optimal way)

TC-> n log k
```java
class Solution
{
    //Function to merge k sorted arrays.
    public static ArrayList<Integer> mergeKArrays(int[][] arr,int K) 
    {
        // Write your code here.
        PriorityQueue<Element> minHeap = new PriorityQueue<>((a,b)->a.val-b.val);
        for(int i=0;i<K;i++){
            minHeap.add(new Element(arr[i][0],i,0));
        }
        ArrayList<Integer> list = new ArrayList<>();
        while(!minHeap.isEmpty()){
            Element root = minHeap.remove();
            list.add(root.val);
            if(root.col+1<K){
                minHeap.add(new Element(arr[root.row][root.col+1],root.row,root.col+1));
            }
        }
        return list;
    }
    static class Element{
        int val,row,col;
        Element(int a,int b,int c){
            this.val = a;
            this.row = b;
            this.col = c;
        }
    }
}
```


OR

n log n
```java
class Solution {
    // Function to merge k sorted arrays.
    public static ArrayList<Integer> mergeKArrays(int[][] arr, int K) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for(int i = 0; i<arr.length; i++){
            for(int j=0; j<arr[i].length; j++){
                pq.offer(arr[i][j]);
            }
        }
        
        ArrayList<Integer> ret = new ArrayList<>();
        while(!pq.isEmpty()){
            ret.add(pq.poll());
        }
        
        return ret;    
    }
    
}
```