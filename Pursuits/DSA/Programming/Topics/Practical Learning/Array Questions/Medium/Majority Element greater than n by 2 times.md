[169. Majority Element](https://leetcode.com/problems/majority-element/)

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** 3

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]
**Output:** 2

**Constraints:**

- `n == nums.length`
- `1 <= n <= 5 * 104`
- `-109 <= nums[i] <= 109`

## Brute Force (TC=>O(N²))
```java
import java.util.*;

public class tUf {
    public static int majorityElement(int []v) {
        //size of the given array:
        int n = v.length;

        for (int i = 0; i < n; i++) {
            //selected element is v[i]
            int cnt = 0;
            for (int j = 0; j < n; j++) {
                // counting the frequency of v[i]
                if (v[j] == v[i]) {
                    cnt++;
                }
            }

            // check if frquency is greater than n/2:
            if (cnt > (n / 2))
                return v[i];
        }

        return -1;
    }

    public static void main(String args[]) {
        int[] arr = {2, 2, 1, 1, 1, 2, 2};
        int ans = majorityElement(arr);
        System.out.println("The majority element is: " + ans);

    }

} 
```

## Better Approach (Use Hashing)
- For unordered_map mostly TC=> O(N)
- SC=> O(N)
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int,int> mp;
        for(int i=0;i<nums.size();i++){
            mp[nums[i]]++;
        }
        for(auto i:mp){
            if(i.second > nums.size()/2){
                return i.first;
            }
        }
        return -1;
    }
};
```


# Moore's Voting Algorithm
[Link](obsidian://open?vault=Lessons&file=DSA%2FProgramming%2FTopics%2FArray%20Questions%2FAlgo%2FMoore's%20Voting%20Algorithm)
## Optimal
In our question we know that majority element exist so we can directly apply this algo.
But in case we don't know then we should check if the count of that element(we got by using this algo) is greater than n/2 , if it is then that element is majority element otherwise majority element doesn't exist.
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int cnt=0;
        int ele;
        for(int i=0;i<nums.size();i++){
            if(cnt == 0){
                cnt++;
                ele=nums[i];
            }
            else if(ele == nums[i]) cnt++;
            else cnt--;
        }
        return ele;
    }
};
```

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int cnt=0;
        int ele;
        for(int i=0;i<nums.size();i++){
            if(cnt == 0){
                ele=nums[i];
            }
            cnt += (ele == nums[i])?1:-1;
        }
        return ele;
    }
};
```

**Time Complexity:** O(N) + O(N), where N = size of the given array.  
**Reason:** The first O(N) is to calculate the count and find the expected majority element. The second one is to check if the expected element is the majority one or not.

**Note:** _If the question states that the array must contain a majority element, in that case, we do not need the second check. Then the time complexity will boil down to O(N)._

**Space Complexity:** O(1) as we are not using any extra space.