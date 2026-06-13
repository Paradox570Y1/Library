[Link](https://www.naukri.com/code360/problems/allocate-books_1090540?utm_source=youtube&utm_medium=affiliate&utm_campaign=codestudio_Striver_BinarySeries&leftPanelTabValue=PROBLEM)
Given an array _**‘arr’**_ of integer numbers, ‘arr[i]’ represents the number of pages in the ‘i-th’ book.
There are _**‘m’**_ number of students, and the task is to allocate all the books to the students.

Allocate books in such a way that:

```
1. Each student gets at least one book.
2. Each book should be allocated to only one student.
3. Book allocation should be in a contiguous manner.
```

You have to allocate the book to ‘m’ students such that the maximum number of pages assigned to a student is minimum.

If the allocation of books is not possible, return -1.
**Example:**

```
Input: ‘n’ = 4 ‘m’ = 2 
‘arr’ = [12, 34, 67, 90]

Output: 113

Explanation: All possible ways to allocate the ‘4’ books to '2' students are:

12 | 34, 67, 90 - the sum of all the pages of books allocated to student 1 is ‘12’, and student two is ‘34+ 67+ 90 = 191’, so the maximum is ‘max(12, 191)= 191’.

12, 34 | 67, 90 - the sum of all the pages of books allocated to student 1 is ‘12+ 34 = 46’, and student two is ‘67+ 90 = 157’, so the maximum is ‘max(46, 157)= 157’.

12, 34, 67 | 90 - the sum of all the pages of books allocated to student 1 is ‘12+ 34 +67 = 113’, and student two is ‘90’, so the maximum is ‘max(113, 90)= 113’.

We are getting the minimum in the last case.

Hence answer is ‘113’.
```

# Brute
```java



import java.util.*;

public class Main {
    public static int countStudents(ArrayList<Integer> arr, int pages) {
        int n = arr.size(); // size of array
        int students = 1;
        long pagesStudent = 0;
        for (int i = 0; i < n; i++) {
            if (pagesStudent + arr.get(i) <= pages) {
                // add pages to current student
                pagesStudent += arr.get(i);
            } else {
                // add pages to next student
                students++;
                pagesStudent = arr.get(i);
            }
        }
        return students;
    }

    public static int findPages(ArrayList<Integer> arr, int n, int m) {
        // book allocation impossible
        if (m > n)
            return -1;

        int low = Collections.max(arr);
        int high = arr.stream().mapToInt(Integer::intValue).sum();

        for (int pages = low; pages <= high; pages++) {
            if (countStudents(arr, pages) == m) {
                return pages;
            }
        }
        return low;
    }
}
```

# Optimal
```cpp
int func(vector<int>& arr,int limit){
   int cnt=1,sum=0;
   for(int i=0;i<arr.size();i++){
       if(sum+arr[i]>limit){
           cnt++;
           sum = arr[i];
       }
       else sum+= arr[i];
   }
   return cnt;
}
int findPages(vector<int>& arr, int n, int m) {
    // Write your code here.
    if(n<m)return -1;
    int low = *max_element(arr.begin(),arr.end());
    int high= accumulate(arr.begin(),arr.end(),0);
    while (low <= high) {
       int mid = (high + low) >> 1;
       if (func(arr, mid) > m)
           low = mid + 1;
       else
           high = mid - 1;
    }
    return low;
}
```

```java

int func(vector<int>& arr,int limit,int k){
    int sum=0,cnt=1;
    for(int i=0;i<arr.size();i++){
        if(sum+arr[i]<=limit) sum+=arr[i];
        else {
          cnt++;
          sum =arr[i];
        }
    }
    return cnt;
}
int findPages(vector<int>& arr, int n, int m) {
    // Write your code here.
    int low=-1,high = 0;
    for(int i=0;i<n;i++){
        low = max(low,arr[i]);
        high += arr[i];
    }
    if(n<m)return -1;
    while(low<=high){
        int mid = low + (high-low)/2;
        int check = func(arr,mid,m);
        if(check<=m){
            high = mid-1;
        }
        else low = mid +1;
    }
    return low;
}
```

# Library functions for ArrayList

![[Pasted image 20250612135352.png|500]]

![[Pasted image 20250612135402.png|500]]


```java
import java.util.ArrayList;
public class Solution {
    private static int studentCnt(ArrayList<Integer> arr,int limit){
        int cnt=0;
        int pages=0;
        for(int page:arr){
            if(pages+page>limit){
                cnt++;
                pages = page;
            }
            else pages+=page;
        }
        return cnt+1;
    }
    public static int findPages(ArrayList<Integer> arr, int n, int m) {
        // Write your code here.
        if(n<m)return -1;
        int low=arr.stream().mapToInt(Integer::intValue).max().orElse(Integer.MAX_VALUE);
        int high= arr.stream().mapToInt(Integer::intValue).sum();
        while(low<=high){
            int mid = low + (high-low)/2;
            if(studentCnt(arr,mid)<=m)high = mid-1;
            else low = mid+1;
        }
        return high+1;
    }
}
```