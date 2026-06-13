- This algorithm divides the array hypothetically in two parts.
- Merge Sort is a **divide-and-conquer algorithm** that is widely used for sorting. Its significance lies in its efficiency, stability, and suitability for various use cases, especially with large datasets.
- TC => O(N x log N) ||| SC=> O(N)
- Merge Sort has a time complexity of O(nlog⁡n) in all cases (best, worst, and average), making it consistently efficient for sorting large datasets.
- **Space Complexity**: It uses additional space proportional to the size of the array being sorted (O(n)O(n)O(n)), which is the trade-off for its time efficiency.
##### Explanation
![[Pasted image 20240708185811.png|400]]

##### Pseudocode
![[Pasted image 20240708190749.png]]

##### Algorithm
```java
import java.util.*;
public class j{

    static void merge(int arr[],int low,int mid,int high){
        int left = low;
        int right = mid+1;
        List<Integer> li = new ArrayList<>();
        while(left<=mid && right<=high){
            if(arr[left]<=arr[right]){
                li.add(arr[left]);
                left++;
            }
            else{
                li.add(arr[right]);
                right++;
            }
        }
        while(left<=mid){
            li.add(arr[left]);
            left++;
        }
        while(right<=high){
            li.add(arr[right]);
            right++;
        }
        for(int i=low;i<=high;i++){
            arr[i] = li.get(i-low);
        }
    }
    static void merge_sort(int arr[],int low,int high){
        if(low>=high)return;
        int mid = (low+high)/2;
        merge_sort(arr, low, mid);
        merge_sort(arr, mid+1, high);
        merge(arr,low,mid,high);
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int arr[] = new int[n];
        for(int i=0;i<n;i++){
            arr[i] = sc.nextInt();
        }
        merge_sort(arr,0,n-1);
        for(int i=0;i<n;i++){
            System.out.print(arr[i]+" ");
        }
    }
}
```
![[Pasted image 20240708204447.png|300]]
