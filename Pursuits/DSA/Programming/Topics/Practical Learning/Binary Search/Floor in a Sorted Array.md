**Floor** of **x** is the largest element which is smaller than or equal to **x**. Floor of **x** doesn’t exist if **x** is smaller than smallest element of **arr[]**.


[Link to Problem](https://www.geeksforgeeks.org/problems/floor-in-a-sorted-array-1587115620/1?track=DSASP-Searching&amp%253BbatchId=154&utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=floor-in-a-sorted-array)
Given a sorted array **arr**[] of size **n** without duplicates, and given a value **x**. Floor of x is defined as the largest element **k** in arr[] such that k is smaller than or equal to x. Find the index of k(0-based indexing).

**Examples  
**

**Input:** n = 7, x = 0 arr[] = {1,2,8,10,11,12,19}
**Output:** -1
**Explanation:** No element less than 0 is found. So output is "**-1**".

**Input:** n = 7, x = 5 arr[] = {1,2,8,10,11,12,19}
**Output:** 1
**Explanation:** Largest Number less than 5 is **2 (i.e k = 2)**, whose index is **1**(0-based indexing).

**Your Task:**  
The task is to complete the function **findFloor**() which returns an integer denoting the index value of K or return **-1** if there isn't any such number.

**Expected Time Complexity:** O(log N).  
**Expected Auxiliary Space:** O(1).

**Constraints:**  
1 ≤ n ≤ 107  
1 ≤ arr[i] ≤ 1018  
0 ≤ x ≤ arr[n-1]


# Brute
```cpp
```

# Optimal
- 3 Approaches
#### 1.
```cpp
class Solution {
  public:
    // Function to find floor of x
    // n: size of vector
    // x: element whose floor is to find
    int findFloor(vector<long long> &v, long long n, long long x) {

        // Your code here
        int i=0,j=n-1;
        while(i<=j){
            int mid = i + (j-i)/2;
            if(mid<n-1){
            if(v[mid]<= x && v[mid+1]>x) return mid;
            else if(v[mid]<x) i = mid+1;
            else if(v[mid]>x) j = mid-1;
            }
            else{
                if(v[mid]<= x)return mid;
            }
        }
        return -1;
    }
};
```

#### 2.
```java
class Solution {

    // Function to find floor of x
    // arr: input array
    // n is the size of array
    static int findFloor(long arr[], int n, long x) {
        int i=0,j=n-1,ans=-1;
        while(i<=j){
            int mid = i + (j-i)/2;
            if(arr[mid] <= x){
                ans = mid;
                i=mid+1;
            }
            else j = mid-1;
        }
        return ans;
    }
}
```

## 3. Using Algorithm
```cpp
class Solution {
  public:
    // Function to find floor of x
    // n: size of vector
    // x: element whose floor is to find
    int findFloor(vector<long long> &v, long long n, long long x) {

        // Your code here
        int up = upper_bound(v.begin(),v.end(),x)-v.begin();
        if(up == 0) up=-1;
        else
        up--;
        return up;
    }
};
```

> upper_bound() is a standard library function in C++ defined in the header. It returns an iterator pointing to the first element in the range [first, last] that is greater than value, or last if no such element is found. The elements in the range shall already be sorted or at least partitioned with respect to val.
