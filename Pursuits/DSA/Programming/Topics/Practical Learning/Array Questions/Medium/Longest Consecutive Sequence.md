[128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]
**Output:** 4
**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]
**Output:** 9

**Constraints:**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`

# Brute Force
**Time Complexity:** O(N²), N = size of the given array.  
**Reason:** We are using nested loops each running for approximately N times.

**Space Complexity:** O(1), as we are not using any extra space to solve this problem.

```cpp
#include <bits/stdc++.h>
using namespace std;

bool linearSearch(vector<int>&a, int num) {
    int n = a.size(); //size of array
    for (int i = 0; i < n; i++) {
        if (a[i] == num)
            return true;
    }
    return false;
}
int longestSuccessiveElements(vector<int>&a) {
    int n = a.size(); //size of array
    int longest = 1;
    //pick a element and search for its
    //consecutive numbers:
    for (int i = 0; i < n; i++) {
        int x = a[i];
        int cnt = 1;
        //search for consecutive numbers
        //using linear search:
        while (linearSearch(a, x + 1) == true) {
            x += 1;
            cnt += 1;
        }

        longest = max(longest, cnt);
    }
    return longest;
}

int main()
{
    vector<int> a = {100, 200, 1, 2, 3, 4};
    int ans = longestSuccessiveElements(a);
    cout << "The longest consecutive sequence is " << ans << "\n";
    return 0;
}
```


# Better Approach
**Time Complexity:** O(NlogN) + O(N), N = size of the given array.  
**Reason:** O(NlogN) for sorting the array. To find the longest sequence, we are using a loop that results in O(N).

**Space Complexity:** O(1), as we are not using any extra space to solve this problem.

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Arrays.sort(nums);
        int cnt=1;
        int max=1;
        int n =nums.length;
        if(n==0) return 0;
        for(int i=0;i<n-1;i++){
            if(nums[i]==nums[i+1]) continue;
            if(nums[i]+1 != nums[i+1]){
                cnt=1;
            }
            else{
                cnt++;
            }
            max = Math.max(cnt,max);
        }
        return max;
    }
}
```

# Best Approach
**Time Complexity:** O(N) + O(2*N) ~ O(3*N), where N = size of the array.  
**Reason:** O(N) for putting all the elements into the set data structure. After that for every starting element, we are finding the consecutive elements. Though we are using nested loops, the set will be traversed at most twice in the worst case. So, the time complexity is O(2*N) instead of O(N2).

**Space Complexity:** O(N), as we are using the set data structure to solve this problem.

**Note:** The time complexity is computed under the assumption that we are using unordered_set and it is taking O(1) for the set operations. 

- If we consider the worst case the set operations will take O(N) in that case and the total time complexity will be approximately O(N²). 
- And if we use the set instead of unordered_set, the time complexity for the set operations will be O(logN) and the total time complexity will be O(NlogN).
```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> st;
        int cnt =0,maxi=INT_MIN;
        if(nums.size()==0) return 0;
        for(auto i:nums) st.insert(i);
        for(auto i:st){
            if(st.find(i-1) == st.end()){
                cnt=1;
                while(st.find(i+1) != st.end()){
                    i++;cnt++;
                }
                maxi = max(cnt,maxi);
            }
        }
        return maxi;
    }
};
```

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Arrays.sort(nums);
        int cnt=0;
        int maxi=-2147483648;
        int n =nums.length;
        HashSet<Integer> hs = new HashSet<>();
        if(n==0) return 0;
        for(int i=0;i<n;i++){
            hs.add(nums[i]);
        }
        for(Integer i:hs){
            if(hs.contains(i-1)== false){
                cnt=1;
                while(hs.contains(i+1)){
                    i++;cnt++;
                }
                maxi = Math.max(cnt,maxi);
            }
        }
        return maxi;
    }
}
```

OR

```java

import java.util.HashSet;
public class pro3 {
    public static void main(String[] args){
       HashSet<Integer> hs = new HashSet<>();
       int arr[] = { 0, 3, 7, 2, 5, 8, 4, 6, 0, 1};
       int n =arr.length;
       for(int i:arr){
        hs.add(i);
       }
       int max_cnt=0;
       for(int ele:arr){
        int cnt=1;
        if(!hs.contains(ele-1)){
            int val = ele;
            while(hs.contains(val+1)){
                val++;
                cnt++;
            }
        }
        max_cnt = Math.max(cnt,max_cnt);
       }
       System.out.print(max_cnt);
    }
}

```