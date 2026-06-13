**Problem Statement:** Given an **integer N** and an array of size **N-1** containing N-1 numbers between 1 to N. Find the number(_between 1 to N_), that is not present in the given array.

#### Naive Approach(Brute-force approach):
```cpp
#include <bits/stdc++.h>
using namespace std;

int missingNumber(vector<int>&a, int N) {

    // Outer loop that runs from 1 to N:
    for (int i = 1; i <= N; i++) {
        // flag variable to check
        //if an element exists
        int flag = 0;
        //Search the element using linear search:
        for (int j = 0; j < N - 1; j++) {
            if (a[j] == i) {
                // i is present in the array:
                flag = 1;
                break;
            }
        }
        // check if the element is missing
        //i.e flag == 0:

        if (flag == 0) return i;
    }

    // The following line will never execute.
    // It is just to avoid warnings.
    return -1;
}

int main()
{
    int N = 5;
    vector<int> a = {1, 2, 4, 5};
    int ans = missingNumber(a, N);
    cout << "The missing number is: " << ans << endl;
    return 0;
}


```


#### Better Approach (using Hashing):
Complexity Analysis

**Time Complexity:** O(N) + O(N) ~ O(2*N),  where N = size of the array+1.  
**Reason:** For storing the frequencies in the hash array, the program takes O(N) time complexity and for checking the frequencies in the second step again O(N) is required. So, the total time complexity is O(N) + O(N).

**Space Complexity:** O(N), where N = size of the array+1. Here we are using an extra hash array of size N+1.

```cpp
#include <bits/stdc++.h>
using namespace std;

int missingNumber(vector<int>&a, int N) {

    int hash[N + 1] = {0}; //hash array

    // storing the frequencies:
    for (int i = 0; i < N - 1; i++)
        hash[a[i]]++;

    //checking the freqencies for numbers 1 to N:
    for (int i = 1; i <= N; i++) {
        if (hash[i] == 0) {
            return i;
        }
    }

    // The following line will never execute.
    // It is just to avoid warnings.
    return -1;
}

int main()
{
    int N = 5;
    vector<int> a = {1, 2, 4, 5};
    int ans = missingNumber(a, N);
    cout << "The missing number is: " << ans << endl;
    return 0;
}


```

---
**Note:** _Among the optimal approaches, the XOR approach is slightly better than the summation one because the term (N * (N+1))/2 used in the summation method cannot be stored in an integer if the value of N is big (like 105). In that case, we have to use some bigger data types. But we will face no issues like this while using the XOR approach_
#### Optimal Approach 1
##### Summation Approach:
**Intuition:**
Sum of first N numbers(S1) = (N*(N+1))/2
Sum of all array elements(S2) = i = 0n-2a[i]
The missing number = S1-S2

**Time Complexity**
O(N), where N = size of array+1.  
**Reason:** Here, we need only 1 loop to get the sum of the array elements. The loop runs for approx. N times. So, the time complexity is O(N).

**Space Complexity:** O(1) as we are not using any extra space.
```cpp
#include <bits/stdc++.h>
using namespace std;

int missingNumber(vector<int>&a, int N) {

    //Summation of first N numbers:
    int sum = (N * (N + 1)) / 2;

    //Summation of all array elements:
    int s2 = 0;
    for (int i = 0; i < N - 1; i++) {
        s2 += a[i];
    }

    int missingNum = sum - s2;
    return missingNum;
}

int main()
{
    int N = 5;
    vector<int> a = {1, 2, 4, 5};
    int ans = missingNumber(a, N);
    cout << "The missing number is: " << ans << endl;
    return 0;
}


```

#### Optimal Approach 2
##### XOR Approach:
**Intuition:**

Two important properties of XOR are the following:

XOR of two same numbers is always 0 i.e. a ^ a = 0. ←Property 1.  
XOR of a number with 0 will result in the number itself i.e. 0 ^ a = a.  ←Property 2

Now, let’s XOR all the numbers between 1 to N.  
xor1 = 1^2^.......^N

Let’s XOR all the numbers in the given array.  
xor2 = 1^2^......^N (contains all the numbers except the missing one).

Now, if we again perform XOR between xor1 and xor2, we will get:  
xor1 ^ xor2 = (1^1)^(2^2)^........^(missing Number)^.....^(N^N)  
  
Here all the numbers except the missing number will form a pair and each pair will result in 0 according to the XOR property. The result will be = 0 ^ (missing number) = missing number (according to property 2).

**_So, if we perform the XOR of the numbers 1 to N with the XOR of the array elements, we will be left with the missing number._**

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int x1=0,x2=0;
        int n = nums.size();
        for(int i=0;i<n;i++){
            x1 ^= nums[i];
            x2 ^= i+1;
        }
        return x1^x2;
    }
};
```

__Complexity Analysis__

**Time Complexity:** O(N), where N = size of array+1.  
**Reason:** Here, we need only 1 loop to calculate the XOR. The loop runs for approx. N times. So, the time complexity is O(N).

**Space Complexity:** O(1) as we are not using any extra space.