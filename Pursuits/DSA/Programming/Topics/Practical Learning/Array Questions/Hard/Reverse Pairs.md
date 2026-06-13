[493. Reverse Pairs](https://leetcode.com/problems/reverse-pairs/)
`Hard`
Given an integer array `nums`, return _the number of **reverse pairs** in the array_.

A **reverse pair** is a pair `(i, j)` where:

- `0 <= i < j < nums.length` and
- `nums[i] > 2 * nums[j]`.

**Example 1:**

**Input:** nums = [1,3,2,3,1]
**Output:** 2
**Explanation:** The reverse pairs are:
(1, 4) --> nums[1] = 3, nums[4] = 1, 3 > 2 * 1
(3, 4) --> nums[3] = 3, nums[4] = 1, 3 > 2 * 1

**Example 2:**

**Input:** nums = [2,4,3,5,1]
**Output:** 3
**Explanation:** The reverse pairs are:
(1, 4) --> nums[1] = 4, nums[4] = 1, 4 > 2 * 1
(2, 4) --> nums[2] = 3, nums[4] = 1, 3 > 2 * 1
(3, 4) --> nums[3] = 5, nums[4] = 1, 5 > 2 * 1

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `-231 <= nums[i] <= 231 - 1`

# Brute
**Time Complexity:** O(N²), where N = size of the given array.  
**Reason:** We are using nested loops here and those two loops roughly run for N times.

**Space Complexity:** O(1) as we are not using any extra space to solve this problem.
```java
class Solution {
    public int reversePairs(int[] nums) {
        int cnt=0;
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                if((long)nums[i]> (long)nums[j]*2) cnt++;
            }
        }
        return cnt;
    }
}
```

# Optimal
**Time Complexity:** O(2N*logN), where N = size of the given array.  
**Reason:** Inside the mergeSort() we call merge() and countPairs() except mergeSort() itself. Now, inside the function countPairs(), though we are running a nested loop, we are actually iterating the left half once and the right half once in total. That is why, the time complexity is O(N). And the merge() function also takes O(N). The mergeSort() takes O(logN) time complexity. Therefore, the overall time complexity will be O(logN * (N+N)) = O(2N*logN).

**Space Complexity:** O(N), as in the merge sort We use a temporary array to store elements in sorted order.

```cpp
class Solution {
public:
    int cnt=0;
    void merge(vector<int>& nums,int low ,int mid , int high){
        int left = low,right = mid+1;
        vector<int> v;
        int l=left;int r= right;
        while(r<=high){
            long long c = 2*static_cast<long long>(nums[r]);
            while(nums[l]<=c && l<=mid)l++;
            if(l>mid) break;
            cnt += (mid-l+1);
            r++;
        }
        while(left<= mid && right<=high){
            if(nums[left]<nums[right]){
                v.emplace_back(nums[left++]);
            }
            else{
                v.emplace_back(nums[right]);
                right++;
            }
        }
        while(left<=mid){
            v.emplace_back(nums[left++]);
        }
        while(right<=high){
            v.emplace_back(nums[right]);
            right++;
        }
        for(int i=low;i<=high;i++){
            nums[i] = v.at(i-low);
        }
    }
    void ms(vector<int>& nums,int low,int high){
        if(low<high){
            int mid = (low+high)/2;
            ms(nums,low,mid);
            ms(nums,mid+1,high);
            merge(nums,low,mid,high);
        }
    }
    int reversePairs(vector<int>& nums) {
        ms(nums,0,nums.size()-1);
        return cnt;
    }
};
```


```java
class Solution {
    int merge(int[] nums,int low ,int mid ,int high){
        int left = low,right = mid+1;
        int cnt=0;
        int l=left,r=right;
        while(l<=mid){
            while(r<=high && nums[l] > 2*(long)nums[r])r++;
            cnt += r-mid-1;
            l++;
        }
        List<Integer> li = new ArrayList<>();
        while(left<=mid && right <= high){
            if(nums[left]<=nums[right]){
                li.add(nums[left++]);
            }
            else{
                li.add(nums[right++]);
            }
        }
        while(left<=mid){
            li.add(nums[left++]);
        }
        while(right<=high){
            li.add(nums[right++]);
        }
        for(int i=low;i<=high;i++){
            nums[i] = li.get(i-low);
        }
        return cnt;
    }
    int ms(int[] nums,int low,int high){
        int cnt=0;
        if(low<high){
            int mid = (low+high)/2;
            cnt += ms(nums,low,mid);
            cnt += ms(nums,mid+1,high);
            cnt += merge(nums,low,mid,high);
        }
        return cnt;
    }
    public int reversePairs(int[] nums) {
        int ans = ms(nums,0,nums.length-1);
        return ans;
    }
}
```

Using different function for count
```java
class Solution {
    void merge(int[] nums,int low ,int mid ,int high){
        int left = low,right = mid+1;
        List<Integer> li = new ArrayList<>();
        while(left<=mid && right <= high){
            if(nums[left]<=nums[right]){
                li.add(nums[left++]);
            }
            else{
                li.add(nums[right++]);
            }
        }
        while(left<=mid){
            li.add(nums[left++]);
        }
        while(right<=high){
            li.add(nums[right++]);
        }
        for(int i=low;i<=high;i++){
            nums[i] = li.get(i-low);
        }
    }
    int countPairs(int[] nums,int low,int mid,int high){
        int right=mid+1;
        int cnt=0;
        for(int i=low;i<=mid;i++){
            while(right<=high && nums[i] > 2*(long)nums[right])right++;
            cnt += right-mid-1;
        }
        return cnt;
    }
    int ms(int[] nums,int low,int high){
        int cnt=0;
        if(low<high){
            int mid = (low+high)/2;
            cnt += ms(nums,low,mid);
            cnt += ms(nums,mid+1,high);
            cnt += countPairs(nums,low,mid,high);
            merge(nums,low,mid,high);
        }
        return cnt;
    }
    public int reversePairs(int[] nums) {
        int ans = ms(nums,0,nums.length-1);
        return ans;
    }
}
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
function merge(nums,low,mid,high){
    let left = low,right = mid+1;
    let temp = [];
    var cnt=0;
    let i = left,j=right;
    while(j<=high){
        let temp = nums[j]*2;
        if(nums[i]>temp){
            cnt+=(mid+1-i);
            j++;
        }
        else if(i!=mid) i++;
        else j++;
    }
    while(left<=mid && right <=high){
        if(nums[left]<=nums[right]){
            temp.push(nums[left++]);
        }
        else{
            temp.push(nums[right++]);
        }
    }
    while(left<=mid){
        temp.push(nums[left++]);
    }
    while(right<=high){
        temp.push(nums[right++]);
    }
    for(let k=low;k<=high;k++){
        nums[k] = temp[k-low];
    }
    return cnt;
 }
 function mergeSort(nums,low,high){
    var cnt =0;
    if(low<high){
        let mid = (low+high)>> 1;
        cnt+= mergeSort(nums,low,mid);
        cnt+= mergeSort(nums,mid+1,high);
        cnt+= merge(nums,low,mid,high);
    }
    return cnt;
 }
var reversePairs = function(nums) {
    return mergeSort(nums,0,nums.length-1);
};
```

OR

```java
class Solution {
    private int merge(int[] nums,int low,int mid,int high){
        int left = low;
        int right = mid+1;
        int i=low;
        int j = mid+1;
        int cnt=0;
        while(i<=mid && j<=high){
            if((long)nums[i]>(long)nums[j]*2){
                cnt+=(mid-i+1);
                j++;
            }
            else i++;
        }
        int[] li = new int[high-low+1];
        int p=0;
        while(left<=mid && right <= high){
            if(nums[left] < nums[right]){
                li[p++] = nums[left++];
            }
            else li[p++] = nums[right++];
        }
        while(left<=mid){
            li[p++] = nums[left++];
        }
        while(right<=high){
            li[p++] = nums[right++];
        }
        for(int k=low;k<=high;k++){
            nums[k] = li[k-low];
        }
        return cnt;
    }
    private int  ms(int[] nums,int low,int high){
        if(low>=high)return 0;
        int cnt=0;
        int mid = low + (high-low)/2;
        cnt+= ms(nums,low,mid);
        cnt+= ms(nums,mid+1,high);
        cnt+= merge(nums,low,mid,high);
        return cnt;
    }
    public int reversePairs(int[] nums) {
        int n = nums.length;
        return ms(nums,0,nums.length-1);
    }
}
```


OR

```java
class Solution {
    private int evaluate(int[] arr, int low, int mid, int high) {
        int l = low;
        int r = mid+1;
        int count = 0;
        while (l <= mid && r <= high) {
            if ((long)arr[l] > (long)2*arr[r]) {
                count += (mid - l + 1);
                r++;
            } else l++;
        }
        return count;
    }
    private int merge(int[] arr, int low, int mid, int high) {
        int l = low;
        int r = mid+1;
        ArrayList<Integer> list = new ArrayList<>();
        int count = evaluate(arr, low, mid, high);
        while (l <= mid && r <= high) {
            if (arr[l] > arr[r]) {
                list.add(arr[r]);
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
    private int mergeSort(int[] arr, int low, int high) {
        if (low >= high) return 0;
        int mid = low + (high - low) / 2;
        int count = 0;
        count = mergeSort(arr, low, mid);
        count += mergeSort(arr, mid+1, high);
        count += merge(arr, low, mid, high);
        return count;
    }
    public int reversePairs(int[] nums) {
        return mergeSort(nums,0,nums.length-1);
    }
}
```