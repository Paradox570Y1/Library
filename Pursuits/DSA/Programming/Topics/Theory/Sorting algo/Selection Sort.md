- It brings the minimum number in front.
- TC => O(N²)
- ![[Pasted image 20240705205035.png|500]]
![[Pasted image 20240705192148.png|400]]
```cpp
#include <iostream>
#include <algorithm>
using namespace std;
void Sel_sort(int size,int *arr){
    int mini;
    for(int i=0;i<size-1;i++){
        mini = i;
        for(int j=i;j<size;j++){
            if(arr[j]<arr[mini]){
                mini = j;
            }
        }
        swap(arr[i],arr[mini]);
    }
}
int main(){
    int n;
    cin >> n;
    int arr[n];
    for(int i=0;i<n;i++){
        cin >> arr[i];
    }
    Sel_sort(n,arr);
    for (int i = 0; i < n; i++){
        cout << arr[i] << " ";
    }
    return 0;
}
```

![[Pasted image 20240708122556.png|220]]

```java
class Solution
{
	int  select(int arr[], int i)
	{
        // code here such that selectionSort() sorts arr[]
        int mini=i;
        for(int j=i;j<arr.length;j++){
            if(arr[j] < arr[mini]){
                mini=j;
            }
        }
        return mini;
	}
	
	void selectionSort(int arr[], int n)
	{
	    //code here
	    for(int i=0;i<n-1;i++){
	        int mini=select(arr,i);
	        int t = arr[i];
	        arr[i]=arr[mini];
	        arr[mini]=t;
	    }
	}
}
```





