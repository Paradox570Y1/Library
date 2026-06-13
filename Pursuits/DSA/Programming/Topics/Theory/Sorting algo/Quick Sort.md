- TC => O(N x log N) ||| SC=> O(1)
#### Explanation
- Pick a pivot(any element in array but we will take 1st element).
- Place it in correct place in sorted way.
- Smaller on the left and larger on the right.
- Repeat the above steps again and again
![[Pasted image 20240709004845.png|500]]
![[Pasted image 20240709004917.png|150]]
![[Pasted image 20240709004948.png|200]]
![[Pasted image 20240709005355.png|400]]

### Algorithm
```cpp
#include <bits/stdc++.h>
using namespace std;
int partition(vector<int> &arr,int low , int high){
    int pivot = arr[low];
    int i = low;
    int j = high;
    while (i < j)
    {
        while (arr[i] <= pivot && i <= high - 1)
        {
            i++;
        }
        while (arr[j] >= pivot && j >= low + 1)
        {
            j--;
        }
        if(i<j) swap(arr[i],arr[j]);
    }
    swap(arr[j],arr[low]);
    return j;
}
void qs(vector<int> &arr,int low,int high){
    if(low<high){
        int Pindex=partition(arr,low,high);
        qs(arr,low,Pindex-1);
        qs(arr,Pindex+1,high);
    }
    }
vector<int> Q_sort(vector<int> v){
    qs(v,0,v.size()-1);
    return v;
}
int main(){
    int n;
    cin >> n;
    vector<int> v(n);
    for(int i=0;i<n;i++){
        cin >> v[i];
    }
    v=Q_sort(v);
    int fix = n;
    for(int i=0;i<n;i++){
        cout << v[i] << " ";
    }
}
```

