[Shell sort](http://en.wikipedia.org/wiki/Shellsort) is mainly a variation of [Insertion Sort](https://www.geeksforgeeks.org/insertion-sort/). In insertion sort, we move elements only one position ahead. When an element has to be moved far ahead, many movements are involved. The idea of ShellSort is to allow the exchange of far items. In Shell sort, we make the array h-sorted for a large value of h. We keep reducing the value of h until it becomes 1. An array is said to be h-sorted if all sublists of every h’th element are sorted.

****Algorithm:****

Step 1 − Start  
Step 2 − Initialize the value of gap size, say h.  
Step 3 − Divide the list into smaller sub-part. Each must have equal intervals to h.  
Step 4 − Sort these sub-lists using insertion sort.  
Step 5 – Repeat this step 2 until the list is sorted.  
Step 6 – Print a sorted list.  
Step 7 – Stop.

****Time Complexity:**** Time complexity of the above implementation of Shell sort is O(n2). In the above implementation, the gap is reduced by half in every iteration. There are many other ways to reduce gaps which leads to better time complexity. See [this](http://en.wikipedia.org/wiki/Shellsort#Gap_sequences) for more details.

****Worst Case Complexity****  
The worst-case complexity for shell sort is O(n2)  
****Best Case Complexity****  
When the given array list is already sorted the total count of comparisons of each interval is equal to the size of the given array.  
So best case complexity is Ω(n log(n))  
****Average Case Complexity****  
The Average Case Complexity: O(n*log n)~O(n1.25)  
****Space Complexity****  
The space complexity of the shell sort is __O(1)__.


```cpp
#include <iostream>
#include <algorithm>
using namespace std;
void sortIfGreater(int a[],int b[],int i,int j){
    if(a[i]>b[j]){
        swap(a[i],b[j]);
    }
    return;
}
int main(){
    int arr1[] = {1,4,8,10};
    int arr2[] = {2,3,9};
    int n = sizeof(arr1)/sizeof(int);
    int m = sizeof(arr2)/sizeof(int);
    int len = m + n;
    int gap = len/2 + 1; // ceil of total length by 2

    while(gap>0){
        int i=0;int j=gap;
        while(j<len){
            // i & j in different array
            if(i<n && j>=n){
                sortIfGreater(arr1,arr2,i,j-n);
            }
            // i & j in arr1
            else if(j<n){
                sortIfGreater(arr1,arr1,i,j);
            }
            // i & j in arr2
            else{
                sortIfGreater(arr2,arr2,i-n,j-n);
            }
            j++;i++;
        }
        if(gap==1)break;
        gap = gap/2 + gap%2; //if even 0 will be added
                            //if odd 1 will be added
    }
    

    for(int i=0;i<len;i++){
        if(i<n) cout << arr1[i] << " ";
        else cout << arr2[i-n] << " ";
    }
}
```