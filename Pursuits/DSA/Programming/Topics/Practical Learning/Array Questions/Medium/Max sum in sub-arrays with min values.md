Given an array **arr[]**, with index ranging from **0 to n-1**, select any two indexes, **i** and **j** such that **i < j** . From the subarray **arr[i...j]**, select the **two minimum numbers** and add them, you will get the **score** for that subarray. Return the **maximum possible score** across all the subarrays of array **arr[]**.  
 

**Examples :**

**Input :** arr[] = [4, 3, 1, 5, 6]
**Output :** 11
**Explanation :** Subarrays with smallest and second smallest are:- [4, 3] smallest = 3,second smallest = 4
[4, 3, 1] smallest = 1, second smallest = 3
[4, 3, 1, 5] smallest = 1, second smallest = 3
[4, 3, 1, 5, 6] smallest = 1, second smallest = 3
[3, 1] smallest = 1, second smallest = 3
[3, 1, 5] smallest = 1, second smallest = 3
[3, 1, 5, 6] smallest = 1, second smallest = 3
[1, 5] smallest = 1, second smallest = 5
[1, 5, 6] smallest = 1, second smallest = 5
[5, 6] smallest = 5, second smallest = 6
Maximum sum among all above choices is, 5 + 6 = 11.

**Input :** arr[] = [5, 4, 3, 1, 6] 
**Output :** 9

  
**Expected Time Complexity:** O(n)  
**Expected Auxiliary Space:** O(1)  
  
**Constraints:**  
2 ≤ n ≤ 105  
1 ≤ arr[i] ≤ 1018

## Brute Force
```java
typedef long long ll;
class Solution {
  public:
    long long pairWithMaxSum(long long arr[], long long N) {
        // Your code goes here
        ll min;
        ll n = N;
        int s_min=0;
        ll maxi=0;
        for(int i=0;i<n-1;i++){
            min =arr[i];
            for(int j=i+1;j<n;j++){
                if(i+1 == j) s_min=arr[j];
                if(min >arr[j] ) {
                    s_min = min;
                    min = arr[j];
                }
                int sum = min + s_min;
                if(sum > maxi) maxi = sum;
            }
        }
        return maxi;
    }
};
```

## Optimal
```cpp
typedef long long ll;
class Solution {
  public:
    long long pairWithMaxSum(long long arr[], long long N) {
        // Your code goes here
        ll  a = arr[0];
        ll b= arr[1];
        ll n = N;
        ll sum = a+b;
        ll l_sum = sum;
        for(int i=1;i<n-1;i++){
            a = arr[i];
            b= arr[i+1];
            sum = a+b;
            if(sum>l_sum) l_sum = sum;
        }
        return l_sum;
    }
};
```
