[215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Given an integer array `nums` and an integer `k`, return _the_ `kth` _largest element in the array_.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Can you solve it without sorting?

**Example 1:**

**Input:** nums = [3,2,1,5,6,4], k = 2
**Output:** 5

**Example 2:**

**Input:** nums = [3,2,3,1,2,4,5,5,6], k = 4
**Output:** 4

**Constraints:**

- `1 <= k <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

using Sorting
```java
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        Arrays.sort(nums);
        int n = nums.length;
        return nums[n-k];
    }
}
```
# Using maxHeap
TC-> O(n log n)
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>((a,b)-> b-a);
        for(int i=0;i<nums.length;i++){
            pq.add(nums[i]);
        }
        while(k>1){
            pq.poll();k--;
        }
        return (int)pq.peek();
    }
}
```

# Using minHeap for maxHeap
TC -O(n log n)
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for(int i=0;i<nums.length;i++){
            pq.add(-nums[i]);
        }
        while(k>1){
            pq.poll();k--;
        }
        return -(int)pq.peek();
    }
}
```

# Using minHeap
TC-> O(n log k)
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        for(int i=0;i<nums.length;i++){
            minHeap.offer(nums[i]);
            if(minHeap.size()>k)minHeap.poll();
        }
        return minHeap.peek();
    }
}
```

Using QuickSort  `TLE`
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int n = nums.length;
        quickSort(nums,0,n-1);
        return nums[n-k];
    }
    void quickSort(int[] nums,int low,int high){
        if(low<high){
            int p = partition(nums,low,high);
            quickSort(nums,low,p-1);
            quickSort(nums,p+1,high);
        }
    }
    int partition(int[] nums,int low,int high){
        int pivot = nums[low];
        int left = low;
        int right = high;
        while(left<right){
            while(nums[left]<=pivot && left<high)left++;
            while(nums[right]>=pivot && right>low)right--;
            if(left<right){
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
            }
        }
        nums[low] = nums[right];
        nums[right]= pivot;
        return right;
    }
}
```

Still TLE
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int n = nums.length;
        int left=0,right=n-1;
        if(nums.length==1)return nums[0];
        while(true){
            int p = partition(nums,left,right);
            if(p==k-1)return nums[p];
            else if(p>k-1){
                right=p-1;
            }
            else left = p+1;
        }
    }
    int partition(int[] nums,int low,int high){
        int pivot = nums[low];
        int left = low;
        int right = high;
	        while(left<right){
	            while(nums[left]>=pivot && left<high)left++;
	            while(nums[right]<=pivot && right>low)right--;
	            if(left<right){
	                int temp = nums[left];
	                nums[left] = nums[right];
	                nums[right] = temp;
	            }
	        }
        nums[low] = nums[right];
        nums[right]= pivot;
        return right;
    }
}
```

### Another optimal way using Quick Select
TC-> Almost O(N)
SC-> O(1)
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int n = nums.length;
        int left=0,right=n-1;
        if(nums.length==1)return nums[0];
        while(true){
            int p = partition(nums,left,right);
            if(p==k-1)return nums[p];
            else if(p>k-1){
                right=p-1;
            }
            else left = p+1;
        }
    }
    int partition(int[] nums,int low,int high){
        int pivot = nums[low];
        int left = low+1;
        int right = high;
        while(left<=right){
            if(nums[left]<pivot && nums[right]>pivot){
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;right--;
            }
            if(nums[left]>=pivot)left++;
            if(nums[right]<=pivot)right--;
        }
        int temp = nums[low];
        nums[low] = nums[right];
        nums[right]= temp;
        return right;
    }
}
```
or
```java
class Solution {
    public void swap(int[] nums,int left,int right){
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }
    public int partition(int[] nums,int left,int right){
        int pivot = nums[left];
        int i = left+1;
        int j = right;
        while(i<=j){
            if(nums[i]<pivot && nums[j]>pivot){
                swap(nums,i,j);
                i++;j--;
            }
            if(nums[i]>=pivot)i++;
            if(nums[j]<=pivot)j--;
        }
        swap(nums,left,j);
        return j;
    }
    public int findKthLargest(int[] nums, int k) {
        int n = nums.length;
        int left = 0,right = n-1;
        for(int i=0;i<n;i++){
            int pos = partition(nums,left,right);
            if(pos==k-1)return nums[pos];
            else if(pos<k-1) left = pos+1;
            else right = pos-1;
        }
        return -1;
    }
}
```

# Optimal

Using Hashing
TC-> O(N)
SC-> O(20001)
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int arr[] = new int[20001];
        for(int num:nums){
            arr[num+10000]++;
        }
        for(int i=20000;i>=0;i--){
            k-=arr[i];
            if(k<=0)return i-10000;
        }
        return -1;
    }
}
```