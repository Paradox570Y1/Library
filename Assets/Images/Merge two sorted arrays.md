[Link](https://www.geeksforgeeks.org/problems/merge-two-sorted-arrays-1587115620/1)
**Problem statement:** Given two sorted arrays **arr1[]** and **arr2[]** of sizes **n** and **m** in non-decreasing order. Merge them in sorted order. Modify arr1 so that it contains the first N elements and modify arr2 so that it contains the last M elements.
# Brute
**Time Complexity:** O(n+m) + O(n+m), where n and m are the sizes of the given arrays.  
**Reason:** O(n+m) is for copying the elements from arr1[] and arr2[] to arr3[]. And another O(n+m) is for filling back the two given arrays from arr3[].

**Space Complexity:** O(n+m) as we use an extra array of size n+m.

```cpp
#include <iostream>
using namespace std;
int main(){
    int arr1[] = {1,4,8,10};
    int arr2[] = {2,3,9};
    int n = sizeof(arr1)/sizeof(int);
    int m = sizeof(arr2)/sizeof(int);
    int len = m + n;
    int i=0,j=0;
    int arr3[len];
    int id=0;
    while(i<n && j<m){
        if(arr1[i]<arr2[j]){
            arr3[id++] = arr1[i++];
        }
        else arr3[id++] = arr2[j++];
    }
    while(i<n){
        arr3[id++] = arr1[i++];
    }
    while(j<m){
        arr3[id++] = arr2[j++];
    }
    for(auto i:arr3){
        cout << i << " ";
    }
}
```

```js
class Solution {
    mergeArrays(a, b) {
        // code here
        if(b.length==0) return;
        if(a.length==0) return mergeArrays(b,a);
        let j=0;
        for(let i=0;i<a.length;i++){
            let temp = a[i];
            if(a[i]<=b[j])continue;
            else{
                a[i] = b[0];
            }
            while(j+1<b.length && b[j+1]<temp){
                b[j] = b[j+1];
                j++;
            }
            b[j] = temp;
            j=0;
            
        }
    }
}
```

OR

```java
class Solution {
    // Function to merge the arrays.
    public void mergeArrays(int a[], int b[]) {
        // code here
        int n = a.length;
        int m = b.length;
        int j=0;
        for(int i=0;i<n;i++){
            if(a[i]>b[j]){
                int temp = a[i];
                a[i] = b[j];
                b[j] = temp;
                Arrays.sort(b);
            }
        }
    }
}
```
# Optimal1
**Time Complexity:** O(min(n, m)) + O(n*logn) + O(m*logm), where n and m are the sizes of the given arrays.  
**Reason:** O(min(n, m)) is for swapping the array elements. And O(n*logn) and O(m*logm) are for sorting the two arrays.

**Space Complexity:** O(1) as we are not using any extra space.
```cpp
#include <iostream>
#include <algorithm>
using namespace std;
int main(){
    int arr1[] = {1,4,8,10};
    int arr2[] = {2,3,9};
    int n = sizeof(arr1)/sizeof(int);
    int m = sizeof(arr2)/sizeof(int);
    int len = m + n;
    int i=n-1,j=0;
    
    while(arr1[i]>arr2[j] && i>=0 && j<=m){
        swap(arr1[i--],arr2[j++]);
    }
    sort(arr1,arr1+n);
    sort(arr2,arr2+m);
    for(int i=0;i<len;i++){
        if(i<n) cout << arr1[i] << " ";
        else cout << arr2[i-n] << " ";
    }
}
```

or

```java
class Solution {
    // Function to merge the arrays.
    public void mergeArrays(int a[], int b[]) {
        // code here
        int n = a.length;
        int m = b.length;
        int i=n-1;
        int j = 0;
        while(i>=0 && j<m && a[i]>b[j]){
            int temp = a[i];
            a[i] = b[j];
            b[j]= temp;
            j++;i--;
        }
        Arrays.sort(a);
        Arrays.sort(b);
    }
}
```
# Optimal2 (Modified Shell Sort Algorithm)
**Time Complexity:** O((n+m)*log(n+m)), where n and m are the sizes of the given arrays.  
**Reason:** The gap is ranging from n+m to 1 and every time the gap gets divided by 2. So, the time complexity of the outer loop will be O(log(n+m)). Now, for each value of the gap, the inner loop can at most run for (n+m) times. So, the time complexity of the inner loop will be O(n+m). So, the overall time complexity will be O((n+m)*log(n+m)).

**Space Complexity:** O(1) as we are not using any extra space.

```java
class Solution {
    // Function to merge the arrays.
    private void swapIfGreater(int[] a,int[] b,int i,int j){
        if(a[i]>b[j]){
            int temp = a[i];
            a[i] = b[j];
            b[j] = temp;
        }
    }
    public void mergeArrays(int a[], int b[]) {
        // code here
        int n = a.length;
        int m = b.length;
        int gap = (n+m)/2 + 1;
        while(gap>0){
            int i=0,j=gap;
            while(j<n+m){
                if(i<n && j<n){
                    swapIfGreater(a,a,i,j);
                }
                else if(i<n && j>=n){
                    swapIfGreater(a,b,i,j-n);
                }
                else{
                    swapIfGreater(b,b,i-n,j-n);
                }
                i++;j++;
            }
            if(gap==1)break;
            gap = gap/2 + gap%2;
        }
    }
}
```
