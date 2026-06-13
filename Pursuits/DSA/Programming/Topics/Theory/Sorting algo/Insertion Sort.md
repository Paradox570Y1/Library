- Takes an element and place it in correct order. 
- TC => O(N²) (average, worst)
- TC => O(N) (best)
**Approach:** 
1. Select an element in each iteration from the unsorted array(using a loop).
2. Place it in its corresponding position in the sorted part and shift the remaining elements accordingly (using an inner loop and swapping).
3. The “inner while loop” basically shifts the elements using swapping.
*[Dry Run](https://takeuforward.org/data-structure/insertion-sort-algorithm/)*
```cpp
void insertion_sort(int n,int *arr){
    for(int i=0;i<n;i++){
        int j =i;
        while(j>0 && arr[j] < arr[j-1]){
            swap(arr[j-1],arr[j]);
            j--;
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
    insertion_sort(n,arr);
    for (int i = 0; i < n; i++){
        cout << arr[i] << " ";
    }
    return 0;
}
```
![[Pasted image 20240708124944.png|200]]
