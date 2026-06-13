[4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

**Input:** nums1 = [1,3], nums2 = [2]
**Output:** 2.00000
**Explanation:** merged array = [1,2,3] and median is 2.

**Example 2:**

**Input:** nums1 = [1,2], nums2 = [3,4]
**Output:** 2.50000
**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

**Constraints:**

- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- `-106 <= nums1[i], nums2[i] <= 106`


# Brute
Complexity Analysis

**Time Complexity:** O(n1+n2), where  n1 and n2 are the sizes of the given arrays.  
**Reason:** We traverse through both arrays linearly.

**Space Complexity:** O(n1+n2), where  n1 and n2 are the sizes of the given arrays.  
**Reason:** We are using an extra array of size (n1+n2) to solve this problem.
```cpp
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n = nums1.length,m = nums2.length;
        int []nums3 = new int[n+m];
        int i=0,j=0,k=0;
        while(i<n && j<m){
            if(nums1[i]<=nums2[j]){
                nums3[k++] = nums1[i++];
            }
            else{
                nums3[k++] =nums2[j++];
            }
        }
        while(i<n){
            nums3[k++] = nums1[i++];
        }
        while(j<m){
            nums3[k++] = nums2[j++];
        }
        int in=(m+n)/2;
        if((m+n)%2==1){
            return (double)nums3[in];
        }
        return (nums3[in]+nums3[in-1])/(double)2;
    }
}
```

# Better
**Time Complexity:** O(n1+n2), where  n1 and n2 are the sizes of the given arrays.  
**Reason:** We traverse through both arrays linearly.

**Space Complexity:** O(1), as we are not using any extra space to solve this problem.
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n = nums1.length,m = nums2.length;
        int i=0,j=0,k=0;
        int in1=(m+n)/2;
        int in2=in1--;
        int a=-1,b=-1;
        while(i<n && j<m){
            
            if(nums1[i]<=nums2[j]){
                if(k==in1) a=nums1[i];
                if(k==in2)b=nums1[i];
                i++;k++;
            }
            else {
                if(k==in1) a=nums2[j];
                if(k==in2)b=nums2[j];
                j++;k++;
            }
                
        }
        while(i<n){
            if(k==in1) a=nums1[i];
            if(k==in2)b=nums1[i];
            i++;k++;
            
        }
        while(j<m){
            if(k==in1) a=nums2[j];
            if(k==in2)b=nums2[j];
            j++;k++;
        }
        if((n+m)%2==1)return b;
        return (a+b)/2.0;
    }
}
```
# Optimal
**Time Complexity:** O(log(min(n1,n2))), where n1 and n2 are the sizes of two given arrays.  
**Reason:** We are applying binary search on the range [0, min(n1, n2)].

**Space Complexity:** O(1) as no extra space is used.

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n1 = nums1.length,n2= nums2.length,n=n1+n2;
        if(n1>n2)return findMedianSortedArrays(nums2,nums1);//required
        
        int low=0,high = n1;
        int left = (n1+n2+1)/2;
        while(low<=high){
            int mid1 = (low+high)>>1;
            int mid2 = left-mid1;
            int r1=Integer.MAX_VALUE,r2=Integer.MAX_VALUE,l1=Integer.MIN_VALUE,l2=Integer.MIN_VALUE;
            if(mid1>=1) l1 = nums1[mid1-1];
            if(mid1<n1) r1 = nums1[mid1];
            if(mid2>=1) l2 = nums2[mid2-1];
            if(mid2<n2) r2 = nums2[mid2];
            if(l1<=r2 && r1>=l2){
                if(n%2==1) return (double)Math.max(l1,l2);
                else return ((double)Math.max(l1,l2)+Math.min(r1,r2))/2.0;
            }
            else if(l1>r2)high = mid1-1;
            else low = mid1+1;
        }
        return -1;
    }
}
```

OR

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n = nums1.length;
        int m = nums2.length;
        if(n>m)return findMedianSortedArrays(nums2,nums1); //required
        int left = (n+m+1)/2;
        int low=0,high=n;
        while(low<=high){
            int mid1 = (low+high)/2;
            int mid2 = left-mid1;
            int l1=Integer.MIN_VALUE,l2=Integer.MIN_VALUE;
            int r1=Integer.MAX_VALUE,r2=Integer.MAX_VALUE;
            if(mid1>0)l1 = nums1[mid1-1];
            if(mid1<n)r1 = nums1[mid1];
            if(mid2>0)l2 = nums2[mid2-1];
            if(mid2<m)r2 = nums2[mid2];
            if(l1<=r2 && l2<=r1){
                if((n+m)%2 == 1)return (double)Math.max(l1,l2);
                else return (Math.max(l1,l2) + Math.min(r1,r2))/2.0;
            }
            else if(l1>r2)high = mid1-1;
            else low = mid1+1;
        }
        return -1;
    }
}
```