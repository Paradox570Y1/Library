Brute Force
![[Pasted image 20240704115921.png|400]]

Using Hashing
```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n;
    cout << "input no. of elements: ";
    cin >> n;
    char arr[n];
    cout << "input elements of array: ";
    for(int i=0;i<n;i++){
        cin >> arr[i];
    }
    //preprocess index is 27 as alphabets(lowercase)=26
    int hash[27] = {0};
    for (int i = 0; i < n; i++){
        hash[arr[i]-'a']++;
    }
    cout << "enter no. of queries: ";
    int q;
    cin >> q;
    char ele;
    cout << "Enter the queries:" << endl;
    while(q--){
        cout << ">";
        cin >> ele;
        cout << "->" << hash[ele-'a'] << endl;
    }
    return 0;
}
```
![[Pasted image 20240708115046.png|200]]

- Taking a String Input
```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s;
    cin >> s;
    int hash[27] = {0};
    for (int i = 0; i<s.size(); i++){
        hash[s[i] - 'a']++;
    }
    
    cout << "enter no. of queries: ";
    int q;
    cin >> q;
    char ele;
    cout << "Enter the queries:" << endl;
    while(q--){
        cout << ">";
        cin >> ele;
        cout << "->" << hash[ele-'a'] << endl;
    }
    return 0;
}
```
![[Pasted image 20240708115530.png|200]]
