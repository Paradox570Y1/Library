[Link](https://www.geeksforgeeks.org/problems/inversion-of-array-1587115620/1)
Given an array of integers. Find the Inversion Count in the array.  Two elements arr[i] and arr[j] form an inversion if arr[i] > arr[j] and i < j.

_**Inversion Count**:_ For an array, inversion count indicates how far (or close) the array is from being sorted. If the array is already sorted then the inversion count is 0.  
If an array is sorted in the reverse order then the inversion count is the maximum. 

**Examples:**

**Input**: arr[] = {2, 4, 1, 3, 5}  
**Output**: 3
**Explanation**: The sequence 2, 4, 1, 3, 5 has three inversions (2, 1), (4, 1), (4, 3).

**Input**: arr[] = {2, 3, 4, 5, 6}  
**Output**: 0
**Explanation**: As the sequence is already sorted so there is no inversion count.

**Input**: arr[] = {10, 10, 10}  
**Output**: 0
**Explanation**: As all the elements of array are same, so there is no inversion count.

**Expected Time Complexity:** O(n*logn).  
**Expected Auxiliary Space:** O(n).  
  
**Constraints:**  
1 ≤ arr.size(),arr[i] ≤ 105

# Brute
**Time Complexity:** O(N2), where N = size of the given array.  
**Reason:** We are using nested loops here and those two loops roughly run for N times.

**Space Complexity:** O(1) as we are not using any extra space to solve this problem
```java
class Solution {
    static long inversionCount(long arr[]) {
        // Your Code Here
        long cnt=0;
        for(int i=0;i<arr.length-1;i++){
            for(int j=i+1;j<arr.length;j++){
                if(arr[i]>arr[j])cnt++;
            }
        }
        return cnt;
    }
}
```
# Optimal
**Time Complexity:** O(N*logN), where N = size of the given array.  
**Reason:** We are not changing the merge sort algorithm except by adding a variable to it. So, the time complexity is as same as the merge sort.

**Space Complexity:** O(N), as in the merge sort. We use a temporary array to store elements in sorted order.
```cpp
//Declaring global variable cnt
class Solution {
  public:
    long long cnt=0;
    void merge(vector<long long> &arr,int low,int mid,int high){
        int left=low;
        int right = mid+1;
        vector<long long> v;
        while(left<=mid && right<=high){
            if(arr[left]<=arr[right]){
                v.emplace_back(arr[left]);
                left++;
            }
            else{
                v.emplace_back(arr[right]);
                cnt += (mid-left+1);
                right++;
            }
        }
        while(left<=mid){
            v.emplace_back(arr[left++]);
        }
        while(right<=high){
            v.emplace_back(arr[right++]);
        }
        for(int i=low;i<=high;i++){
            arr[i] = v[i-low];
        }
    }
    long long ms(vector<long long> &arr,int low,int high){
        if(low<high){
            int mid = (low+high)/2;
            ms(arr,low,mid);
            ms(arr,mid+1,high);
            merge(arr,low,mid,high);
        }
        return cnt;
    }
    long long int inversionCount(vector<long long> &arr) {
        // Your Code Here
        long long ans = ms(arr,0,arr.size()-1);
        return ans;
    }
};
```


```cpp
//Passing cnt by functions
class Solution {
  public:
    // arr[]: Input Array
    // N : Size of the Array arr[]
    // Function to count inversions in the array.
    
    long long merge(vector<long long> &arr,int low,int mid,int high){
        int left=low;
        int right = mid+1;
        vector<long long> v;
        long long cnt=0;
        while(left<=mid && right<=high){
            if(arr[left]<=arr[right]){
                v.emplace_back(arr[left]);
                left++;
            }
            else{
                v.emplace_back(arr[right]);
                cnt += (mid-left+1);
                right++;
            }
        }
        while(left<=mid){
            v.emplace_back(arr[left++]);
        }
        while(right<=high){
            v.emplace_back(arr[right++]);
        }
        for(int i=low;i<=high;i++){
            arr[i] = v[i-low];
        }
        return cnt;
    }
    long long ms(vector<long long> &arr,int low,int high){
        long long cnt=0;
        if(low<high){
            int mid = (low+high)/2;
            cnt += ms(arr,low,mid);
            cnt += ms(arr,mid+1,high);
            cnt += merge(arr,low,mid,high);
        }
        return cnt;
    }
    long long int inversionCount(vector<long long> &arr) {
        // Your Code Here
        long long ans = ms(arr,0,arr.size()-1);
        return ans;
    }
};
```

```js
let cnt=0;
class Solution {
    // Function to count inversions in the array.
    constructor(){
        this.cnt =0;
    }
     merge(arr,low,mid,high){
        let left = low,right=mid+1;
        let temp = []
        while(left<=mid && right<=high){
            if(arr[left]<=arr[right])temp.push(arr[left++])
            else{
                temp.push(arr[right++]);
                this.cnt += (mid+1-left);
            } 
        }
        while(left<=mid){
            temp.push(arr[left++]);
        }
        while(right<=high){
            temp.push(arr[right++]);
        }
        for(let i=low;i<=high;i++){
            arr[i] = temp[i-low];
        }
    }
    mergeSort(arr,low,high){
        if(low<high){
            let mid = (low+high)>>1;
            this.mergeSort(arr,low,mid);
            this.mergeSort(arr,mid+1,high);
            this.merge(arr,low,mid,high);
        }
    }
    inversionCount(arr) {
        // your code here
        this.mergeSort(arr,0,arr.length-1);
        
        return this.cnt;
    }
}
```

```js
class Solution {
    // Function to count inversions in the array.
     merge(arr,low,mid,high){
        let left = low,right=mid+1;
        let temp = []
        let cnt=0;
        while(left<=mid && right<=high){
            if(arr[left]<=arr[right])temp.push(arr[left++])
            else{
                temp.push(arr[right++]);
                cnt += (mid+1-left);
            } 
        }
        while(left<=mid){
            temp.push(arr[left++]);
        }
        while(right<=high){
            temp.push(arr[right++]);
        }
        for(let i=low;i<=high;i++){
            arr[i] = temp[i-low];
        }
        return cnt;
    }
    mergeSort(arr,low,high){
        let cnt=0;
        if(low<high){
            let mid = (low+high)>>1;
            cnt+=this.mergeSort(arr,low,mid);
            cnt+=this.mergeSort(arr,mid+1,high);
            cnt+=this.merge(arr,low,mid,high);
        }
        return cnt;
    }
    inversionCount(arr) {
        // your code here
 
        return this.mergeSort(arr,0,arr.length-1);
    }
```

OR

```java
class Solution {
    private static int merge(int[] arr, int low, int mid, int high) {
        int l = low;
        int r = mid+1;
        ArrayList<Integer> list = new ArrayList<>();
        int count = 0;
        while (l <= mid && r <= high) {
            if (arr[l] > arr[r]) {
                list.add(arr[r]);
                count += (mid - l + 1);
                r++;
            } else {
                list.add(arr[l]);
                l++;
            }
        }
        
        while (l <= mid) {
            list.add(arr[l]);
            l++;
        }
        
        while (r <= high) {
            list.add(arr[r]);
            r++;
        }
        
        for (int i = low; i <= high; i++) {
            arr[i] = list.get(i-low);
        }
        return count;
    }
    static int mergeSort(int[] arr, int low, int high) {
        if (low >= high) return 0;
        int mid = low + (high - low) / 2;
        int count = 0;
        count = mergeSort(arr, low, mid);
        count += mergeSort(arr, mid+1, high);
        count += merge(arr, low, mid, high);
        return count;
    }
    static int inversionCount(int arr[]) {
        // Code Here
        return mergeSort(arr, 0, arr.length-1);
    }
}
```
#### You can even say in interview that  in this approach i am changing the data, in case you don't want to change the data then i can take the copy of the data and then use this approach on it.