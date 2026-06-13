[Link](https://www.geeksforgeeks.org/problems/kth-smallest-element5635/1)
Difficulty: **Medium**Accuracy: **35.17%**Submissions: **675K+**Points: **4**Average Time: **25m**

Given an array **arr[]** and an integer **k** where k is smaller than the size of the array, the task is to find the **kth smallest** element in the given array.

**Follow up:** Don't solve it using the inbuilt sort function.

**Examples :**

**Input:** arr[] = [7, 10, 4, 3, 20, 15], k = 3
**Output:**  7
**Explanation:** 3rd smallest element in the given array is 7.

**Input:** arr[] = [2, 3, 1, 20, 15], k = 4 
**Output:** 15
**Explanation:** 4th smallest element in the given array is 15.

**Expected Time Complexity:** O(n+(max_element) )

**Expected Auxiliary Space:** O(max_element)

**Constraints:**  
1 <= arr.size <= 106  
1<= arr[i] <= 106  
1 <= k <= n


# Optimal

Using maxHeap
```cpp
class Solution {
  public:
    // arr : given array
    // k : find kth smallest element and return using this function
    int kthSmallest(vector<int> &arr, int k) {
        // code here
        priority_queue<int> maxHeap;
        for(int v:arr){
            maxHeap.push(v);
            if(maxHeap.size()>k)maxHeap.pop();
        }
        return maxHeap.top();
    }
};
```

TC-> O(N)
SC-> O(100000)
```java
class Solution {
    public static int kthSmallest(int[] arr, int k) {
        // Your code here
        int hash[] = new int[1000001];
        for(int n:arr){
            hash[n]++;
        }
        for(int i=0;i<1000001;i++){
            k-=hash[i];
            if(k<=0)return i;
        }
        return -1;
    }
}
```

TC -> O(N)
SC -> O(1)
```java
class Solution {
    public static int kthSmallest(int[] arr, int k) {
        // Your code here
        int left=0,right=arr.length-1;
        int ans;
        while(true){
            int p = partition(arr,left,right);
            if(p==k-1){
                ans=arr[p];
                break;
            }
            else if(p>k-1)right=p-1;
            else left = p+1;
        }
        return ans;
    }
    static int partition(int[] arr,int left,int right){
        int pivot = arr[left];
        int l = left+1;
        int r = right;
        while(l<=r){
            if(arr[l]>pivot && arr[r]<pivot){
                int temp = arr[l];
                arr[l] = arr[r];
                arr[r] = temp;
            }
            if(arr[l]<=pivot)l++;
            if(arr[r]>=pivot)r--;
        }
        arr[left] = arr[r];
        arr[r] = pivot;
        return r;
    }
}
```