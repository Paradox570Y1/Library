- Push the max element to the last.
- ![[Pasted image 20240705204548.png|100]]
- TC => O(N²) worst as well average TC. But you can optimize the code to get  best TC => O(N)
- Brute Force
```cpp
#include <iostream>
#include <algorithm>
using namespace std;
void Bubble_sort(int n,int *arr){
    for(int i=n-1;i>0;i--){
        for(int j=0;j<i;j++){
            if(arr[j] > arr[j+1]){
                swap(arr[j],arr[j+1]);
            }
        }
    }
}
int main(){
    int n;
    cin >> n;
    int arr[n];
    for(int i=0;i<n;i++){
        cin >> arr[i];
    }
    Bubble_sort(n,arr);
    for (int i = 0; i < n; i++){
        cout << arr[i] << " ";
    }
    return 0;
}
```

- After Optimizing
```cpp
void Bubble_sort(int n,int *arr){
    for(int i=n-1;i>0;i--){
        int didSwap=0;
        for(int j=0;j<i;j++){
            if(arr[j] > arr[j+1]){
                swap(arr[j],arr[j+1]);
                didSwap=1;
            }
        }
        if(didSwap==0){
            break;
        }
    }
}
int main(){
    int n;
    cin >> n;
    int arr[n];
    for(int i=0;i<n;i++){
        cin >> arr[i];
    }
    Bubble_sort(n,arr);
    for (int i = 0; i < n; i++){
        cout << arr[i] << " ";
    }
    return 0;
}
```