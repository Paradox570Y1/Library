### Array Leaders

Difficulty: **Easy**Accuracy: **29.94%**Submissions: **682K+**Points: **2**

Given an array **arr** of **n** positive integers, your task is to find all the leaders in the array. An element of the array is considered a leader if it is greater than all the elements on its right side or if it is equal to the maximum element on its right side. The rightmost element is always a leader.

**Examples 

**Input:** n = 6, arr[] = {16,17,4,3,5,2}
**Output:** 17 5 2
**Explanation:** Note that there is nothing greater on the right side of 17, 5 and, 2.

**Input:** n = 5, arr[] = {10,4,2,4,1}
**Output:** 10 4 4 1  
**Explanation:** Note that both of the 4s are in output, as to be a leader an equal element is also allowed on the right. side

**Input:** n = 4, arr[] = {5, 10, 20, 40}   
**Output:** 40  
**Explanation:** When an array is sorted in increasing order, only the rightmost element is leader.

**Input:** n = 4, arr[] = {30, 10, 10, 5} **Output:** 30 10 10 5  
**Explanation:** When an array is sorted in non-increasing order, all elements are leaders.

**Expected Time Complexity:** O(n)  
**Expected Auxiliary Space:** O(n)

**Constraints:**  
1 <= n <= 107  
0 <= arr[i] <= 107

# Brute Force
**Time Complexity:** O(N²) { Since there are nested loops being used, at the worst case n²time would be consumed }.

**Space Complexity: O(N)** { There is no extra space being used in this approach. But, a O(N) of space for ans array will be used in the worst case }.
```cpp
#include<bits/stdc++.h>
using namespace std;

vector<int> printLeadersBruteForce(int arr[], int n) {

  vector<int> ans;
  
  for (int i = 0; i < n; i++) {
    bool leader = true;

    //Checking whether arr[i] is greater than all 
    //the elements in its right side
    for (int j = i + 1; j < n; j++)
      if (arr[j] > arr[i]) {
          
        // If any element found is greater than current leader
        // curr element is not the leader.
        leader = false;
        break;
      }

    // Push all the leaders in ans array.
    if (leader)
    ans.push_back(arr[i]);

  }
  
  return ans;
}

int main() {
    
  // Array Initialization.
  int n = 6;
  int arr[n] = {10, 22, 12, 3, 0, 6};

  vector<int> ans = printLeadersBruteForce(arr,n);
  
  for(int i = 0;i<ans.size();i++){
      
      cout<<ans[i]<<" ";
  }
  
  cout<<endl;
  return 0;
}
```

# Optimal Approach
**Time Complexity: O(N)** { Since the array is traversed single time back to front, it will consume O(N) of time where N = size of the array }.

**Space Complexity: O(N)** { There is no extra space being used in this approach. But, a O(N) of space for ans array will be used in the worst case }.
```java
class Solution {
    // Function to find the leaders in the array.
    static ArrayList<Integer> leaders(int n, int arr[]) {
        // Your code here
        int lar=arr[n-1];
        ArrayList<Integer> li = new ArrayList<>();
        for(int i=n-1;i>=0;i--){
            if(arr[i]>=lar){
                li.add(arr[i]);
                lar = arr[i];
            }
        }
        int i=0,j=li.size()-1;
        while(i<=j){
            int t = li.get(i);
            li.set(i,li.get(j));
            li.set(j,t);
            i++;j--;
        }
        return li;
    }
}
```

```cpp
#include<bits/stdc++.h>
using namespace std;

vector<int> printLeaders(int arr[], int n) {

  vector<int> ans;
  
 // Last element of an array is always a leader,
 // push into ans array.
 int max = arr[n - 1];
 ans.push_back(arr[n-1]);

  // Start checking from the end whether a number is greater
  // than max no. from right, hence leader.
  for (int i = n - 2; i >= 0; i--)
    if (arr[i] > max) {
      ans.push_back(arr[i]);
      max = arr[i];
    }

  
  return ans;
}

int main() {
    
  // Array Initialization.
  int n = 6;
  int arr[n] = {10, 22, 12, 3, 0, 6};

  vector<int> ans = printLeaders(arr,n);
  
  
  for(int i = ans.size()-1;i>=0;i--){
      
      cout<<ans[i]<<" ";
  }
  
  cout<<endl;
  return 0;
}
```

OR

```java

import java.util.Stack;
public class pro3 {
    public static void main(String[] args){
        Stack<Integer> st = new Stack<>();
        int[] arr = { 30, 10, 10, 5};
        int n =arr.length;
        int maxi = -1;
        for(int i=n-1;i>=0;i--){
            if(arr[i]>=maxi){
                st.push(arr[i]);
                maxi = arr[i];
            }
        }
        while(!st.isEmpty()){
            System.out.print(st.pop() + " ");
        }
    }
}

```