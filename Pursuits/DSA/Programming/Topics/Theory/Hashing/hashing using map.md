- TC of map
	  - Storing and Fetching both takes (log n) in worst, average and best case.
- Remember it stores data in sorted order.
- In map key can be any data type int ,string , char even pair etc..
![[Pasted image 20240705111305.png|500]]
- key is your number and how many times it appears (frequency) is your value.
![[Pasted image 20240705112052.png|500]]

- Example 1
```cpp
  #include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cout << "input no. of elements: ";
    cin >> n;
    int arr[n];
    cout << "input elements of array: ";
    //preprocess
    map<int,int> mp;
    for(int i=0;i<n;i++){
        cin >> arr[i];
        mp[arr[i]]++;
    }
    
    cout << "enter no. of queries: ";
    int q;
    cin >> q;
    int ele;
    cout << "Enter the queries:" << endl;
    while(q--){
        cout << ">";
        cin >> ele;
        cout << " ->" << mp[ele] << endl;
    }
    return 0;
}
```

- Example 2
![[Pasted image 20240705113807.png|500]]
  - you can preprocess while taking input too but doesn't affect much of TC.