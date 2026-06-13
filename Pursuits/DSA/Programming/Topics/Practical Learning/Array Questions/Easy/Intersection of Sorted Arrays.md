[Link](https://www.geeksforgeeks.org/problems/intersection-of-two-sorted-array-1587115620/1)
- Brute Force
```cpp
#include <bits/stdc++.h>
using namespace std;
void print(vector<int> a)
{
    for (auto i : a)
    {
        cout << i << " ";
    }
}
int main()
{
    int a[] = {1, 2, 2, 3, 3, 4, 5, 6};
    int b[] = {2, 3, 3, 5, 6, 6, 7};
    vector<int> v;
    int n = 8;
    int m = 7;
    int temp[m] = {0};

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (a[i] == b[j] && temp[j] == 0)
            {
                v.push_back(a[i]);
                temp[j] = 1;
                break;
            }
            if(b[j]>a[i]) break;
        }
    }
    print(v);
    return 0;
}
```

- Optimal (TC =>O(n+m))
```cpp
#include<bits/stdc++.h>
using namespace std;
void print(vector<int> a){
    for(auto i:a){
        cout << i << " ";
    }
}
int main(){
    int a[] = {1,2,2,3,3,4,5,6};
    int b[] = {2,3,3,5,6,6,7};
    vector<int> v;
    int n = 8;
    int m = 7;
    int i=0,j=0;
    while(i<n && j<m){
        if(a[i]>b[j]){
            j++;
        }
        else if(a[i]<b[j]){
            i++;
        }
        else{
            v.push_back(a[i]);
            j++;i++;
        }
    }
    print(v);
    return 0;
}
```
![[Pasted image 20240711190633.png|200]]

```java
class Solution {
    // Function to return a list containing the intersection of two arrays.
    static ArrayList<Integer> intersection(int arr1[], int arr2[]) {
        // add your code here
        int n = arr1.length;
        int m = arr2.length;
        int i=0,j=0;
        ArrayList<Integer> ans = new ArrayList<>();
        while(i<n && j<m){
            if(arr1[i] > arr2[j]){
                j++;
            }
            else if(arr1[i]< arr2[j]){
                i++;
            }
            else{
                int size = ans.size();
                if(size==0 || ans.get(size-1) != arr1[i])ans.add(arr1[i]);
                i++;j++;
            }
        }
        return ans;
    }
}
```