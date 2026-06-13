[31. Next Permutation](https://leetcode.com/problems/next-permutation/)

A **permutation** of an array of integers is an arrangement of its members into a sequence or linear order.

- For example, for `arr = [1,2,3]`, the following are all the permutations of `arr`: `[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]`.

The **next permutation** of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the **next permutation** of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

- For example, the next permutation of `arr = [1,2,3]` is `[1,3,2]`.
- Similarly, the next permutation of `arr = [2,3,1]` is `[3,1,2]`.
- While the next permutation of `arr = [3,2,1]` is `[1,2,3]` because `[3,2,1]` does not have a lexicographical larger rearrangement.

Given an array of integers `nums`, _find the next permutation of_ `nums`.

The replacement must be **[in place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** [1,3,2]

**Example 2:**

**Input:** nums = [3,2,1]
**Output:** [1,2,3]

**Example 3:**

**Input:** nums = [1,1,5]
**Output:** [1,5,1]

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 100`

## Brute Force
Step 1: Find all possible permutations of elements present and store them.(Recursion)
Step 2: Search input from all possible permutations.(Linear Search)
Step 3: Print the next permutation present right after it.

#### Complexity Analysis

For finding, all possible permutations, it is taking N!xN. N represents the number of elements present in the input array. Also for searching input arrays from all possible permutations will take N!. Therefore, it has a Time complexity of O(N!xN).

**Space Complexity :**

Since we are not using any extra spaces except stack spaces for recursion calls. So, it has a space complexity of O(1).

Its very poor complexity code not usable.

## Better Approach
```cpp
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

int main() {
    int arr[] = {1,3,2};
    next_permutation(arr,arr+3);//using in-built function of C++
    cout<<arr[0]<<" "<<arr[1]<<" "<<arr[2];
    
    return 0;
}
```

## Optimal Approach
Complexity Analysis

**Time Complexity:** O(3N), where N = size of the given array  
Finding the break-point, finding the next greater element, and reversal at the end takes O(N) for each, where N is the number of elements in the input array. This sums up to 3*O(N) which is approximately O(3N).

**Space Complexity:** Since no extra storage is required. Thus, its space complexity is O(1).

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> nextGreaterPermutation(vector<int> &A) {
    int n = A.size(); // size of the array.

    // Step 1: Find the break point:
    int ind = -1; // break point
    for (int i = n - 2; i >= 0; i--) {
        if (A[i] < A[i + 1]) {
            // index i is the break point
            ind = i;
            break;
        }
    }

    // If break point does not exist:
    if (ind == -1) {
        // reverse the whole array:
        reverse(A.begin(), A.end());
        return A;
    }

    // Step 2: Find the next greater element
    //         and swap it with arr[ind]:

    for (int i = n - 1; i > ind; i--) {
        if (A[i] > A[ind]) {
            swap(A[i], A[ind]);
            break;
        }
    }

    // Step 3: reverse the right half:
    reverse(A.begin() + ind + 1, A.end());

    return A;
}

int main()
{
    vector<int> A = {2, 1, 5, 4, 3, 0, 0};
    vector<int> ans = nextGreaterPermutation(A);

    cout << "The next permutation is: [";
    for (auto it : ans) {
        cout << it << " ";
    }
    cout << "]n";
    return 0;
}


```

```java
class Solution {
    void swap(int[] nums,int i,int j){
        int t = nums[i];
        nums[i]=nums[j];
        nums[j]=t;
    }
    void reverse(int[] nums,int i,int j){
        if(i>=j) return;
        else{
            swap(nums,i,j);
            reverse(nums,i+1,j-1);
        }
    }
    public void nextPermutation(int[] nums) {
        int n=nums.length;
        int i= n-2;
        int p =n-1;
        while(i>=0 && nums[i+1]<= nums[i]){
            i--;
            p=i+1;
        }
        
        if(i==-1) {
            reverse(nums,0,n-1);
            return;
        }
        for(int j=i+1;j<=n-1;j++){
                if(nums[j] > nums[i] && nums[j] <= nums[p]) p=j;
        }
        swap(nums,p,i);
        if(i+1 < n-1) reverse(nums,i+1,n-1);
        }
        
    
}
```

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int i = n-1;
        while(i>0 && nums[i-1]>=nums[i]){
            i--;
        }
        i -= 1;
        if(i==-1){
            reverse(nums.begin(),nums.end());
            return;
        }
        int swap_in = n-1;
        
        for(int k=n-2;k>i;k--){
            if(nums[k]>nums[i]){
                if(nums[swap_in] <= nums[i]){
                    swap_in = k;
                }
                else{
                    swap_in = nums[swap_in]>nums[k]?k:swap_in;   
                }
                
            }
        }
        swap(nums[swap_in],nums[i]);
        reverse(nums.begin()+i+1,nums.end());

    }
};
```

```cpp
// Best space complexity
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        // //in-built function
        // next_permutation(nums.begin(),nums.end());


        int n=nums.size();
        int break_pt=-1;
        for(int i=n-2;i>=0;i--)
        {
            if(nums[i+1]>nums[i])
            {
                break_pt=i;
                break;
            }
        }
        if(break_pt==-1)
            reverse(nums.begin(),nums.end());
        else
        {
            for(int i=n-1;i>break_pt;i--)
            {
                if(nums[i]>nums[break_pt])
                {
                    swap(nums[i],nums[break_pt]);
                    break;
                }
            }
            reverse(nums.begin()+break_pt+1,nums.end());
        }
    }
};
```