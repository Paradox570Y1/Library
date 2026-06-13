```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cout << "input no. of elements: ";
    cin >> n;
    int arr[n];
    cout << "input elements of array: ";
    for(int i=0;i<n;i++){
        cin >> arr[i];
    }
    //preprocess Let max element be 12 then do 13(12+1)
    int hash[13] = {0};
    for (int i = 0; i < n; i++){
        hash[arr[i]]++;
    }
    cout << "enter no. of queries: ";
    int q;
    cin >> q;
    int ele;
    cout << "Enter the queries:" << endl;
    while(q--){
        cout << ">";
        cin >> ele;
        cout << " ->" << hash[ele] << endl;
    }
    return 0;
}
```


![[Pasted image 20240708114311.png|200]]

```java
import java.util.*;
 
public class tuf {
 
public static void main(String args[]){  
   
   int arr[] = {10,5,10,15,10,5};
     int n = arr.length;
     Frequency(arr, n);
  }
static void Frequency(int arr[], int n)
{
    Map<Integer, Integer> map = new HashMap<>();
 
    for (int i = 0; i < n; i++)
    {
        if (map.containsKey(arr[i]))
        {
            map.put(arr[i], map.get(arr[i]) + 1);
        }
        else
        {
            map.put(arr[i], 1);
        }
    }
    // Traverse through map and print frequencies
    for (Map.Entry<Integer,Integer> entry : map.entrySet())
    {
        System.out.println(entry.getKey() + " " + entry.getValue());
    }
}
}
```