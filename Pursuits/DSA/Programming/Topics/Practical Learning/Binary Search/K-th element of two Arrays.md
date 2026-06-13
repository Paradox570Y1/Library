[Link](https://www.geeksforgeeks.org/problems/k-th-element-of-two-sorted-array1317/1)
Given two sorted arrays **arr1** and **arr2** and an element **k**. The task is to find the element that would be at the kth position of the combined sorted array.

**Examples :**

**Input:** k = 5, arr1[] = [2, 3, 6, 7, 9], arr2[] = [1, 4, 8, 10]
**Output:** 6
**Explanation:** The final combined sorted array would be - 1, 2, 3, 4, 6, 7, 8, 9, 10. The 5th element of this array is 6.

**Input:** k = 7, arr1[] = [100, 112, 256, 349, 770], arr2[] = [72, 86, 113, 119, 265, 445, 892]
**Output:** 256
**Explanation:** Combined sorted array is - 72, 86, 100, 112, 113, 119, 256, 265, 349, 445, 770, 892. 7th element of this array is 256.

**Expected Time Complexity:** O(log(n) + log(m))  
**Expected Auxiliary Space:** O(log (n))

**Constraints:  
**1 <= k<= arr1.size()+arr2.size()  
1 <= arr1.size(), arr2.size() <= 106  
0 <= arr1[i], arr2[i] < 108


# Better
TC => O(n1+n2)
SC => O(1)
```cpp
class Solution {
  public:
    int kthElement(int pos, vector<int>& arr1, vector<int>& arr2) {
        // code here
        int left = 0,right=0,k=0;
        pos--;
        int n1=arr1.size(),n2=arr2.size();
        while(left<n1 && right<n2){
            if(arr1[left]<=arr2[right]){
                if(k++==pos) return arr1[left];
                left++;
            }
            else{
                if(k++==pos) return arr2[right];
                right++;
            }
        }
        while(left<n1){
            if(k++==pos) return arr1[left];
            left++;
        }
        while(right<n2){
            if(k++==pos)return arr2[right];
            right++;
        }
        return -1;
    }
};
```
# Optimal
**Time Complexity:** O(log(min(m, n))), where m and n are the sizes of two given arrays.  
**Reason:** We are applying binary search on the range [max(0, k-n2), min(k, n1)]. The range length <= min(m, n).

**Space Complexity:** O(1), as we are not using any extra space to solve this problem.
```cpp
class Solution {
  public:
    int kthElement(int k, vector<int>& arr1, vector<int>& arr2) {
        // code here
        int n1 = arr1.size(),n2=arr2.size(),n=n1+n2;
        if(n1>n2) return kthElement(k,arr2,arr1); // not required
        
        int low=max(0,k-n2),high=min(k,n1);
        int left = k;
        while(low<=high){
            int mid1 = (low+high)>>1;
            int mid2 = left-mid1;
            int l1=INT_MIN,l2 = INT_MIN , r1=INT_MAX ,r2=INT_MAX;
            if(mid1<n1)r1=arr1[mid1];
            if(mid2<n2)r2=arr2[mid2];
            if(mid1>=1)l1 = arr1[mid1-1];
            if(mid2>=1)l2 = arr2[mid2-1];
            if(l1<=r2 && l2 <=r1){
                return max(l1,l2);
            }
            else if(l1>r2)high =mid1-1;
            else low=mid1+1;
            
            
        }
        return -1;
    }
};
```

OR

```java
class Solution {
    public int kthElement(int a[], int b[], int k) {
        // code here
        int n = a.length;
        int m = b.length;
        int low = Math.max(0,k-m),high = Math.min(n,k);
        while(low<=high){
            int mid1 = (low+high)/2;
            int mid2 = k-mid1;
            int l1 = Integer.MIN_VALUE,l2 = Integer.MIN_VALUE;
            int r1 = Integer.MAX_VALUE,r2 = Integer.MAX_VALUE;
            if(mid1>0)l1 = a[mid1-1];
            if(mid2>0)l2 = b[mid2-1];
            if(mid1<n)r1 = a[mid1];
            if(mid2<m)r2 = b[mid2];
            if(l1<=r2 && l2<=r1) return Math.max(l1,l2);
            else if(l1>r2)high = mid1-1;
            else low = mid1+1;
        }
        return -1;
    }
}
```