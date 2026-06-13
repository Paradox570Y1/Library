[229. Majority Element II](https://leetcode.com/problems/majority-element-ii/)

Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** [3]

**Example 2:**

**Input:** nums = [1]
**Output:** [1]

**Example 3:**

**Input:** nums = [1,2]
**Output:** [1,2]

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `-109 <= nums[i] <= 109`
#### Observation: How many integers can occur more than floor(N/3) times in the given array:

If we closely observe, in the given array, there can be a maximum of two integers that can occur more than floor(N/3) times. Let’s understand it using the following scenario:  
Assume there are 8 elements in the given array. Now, if there is any majority element, it should occur more than floor(8/3) = 2 times. So, the majority of elements should occur at least 3 times. Now, if we imagine there are 3 majority elements, then the total occurrence of them will be 3X3 = 9 i.e. greater than the size of the array. But this should not happen. That is why **_there can be a maximum of 2 majority elements._**
# Brute Force 
TC => O(N²)
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> majorityElement(vector<int> v) {
    int n = v.size(); //size of the array
    vector<int> ls; // list of answers
    for (int i = 0; i < n; i++) {
        //selected element is v[i]:
        // Checking if v[i] is not already
        // a part of the answer:
        if (ls.size() == 0 || ls[0] != v[i]) {
            int cnt = 0;
            for (int j = 0; j < n; j++) {
                // counting the frequency of v[i]
                if (v[j] == v[i]) {
                    cnt++;
                }
            }
            // check if frquency is greater than n/3:
            if (cnt > (n / 3))
                ls.push_back(v[i]);
        }
        if (ls.size() == 2) break;
    }
    return ls;
}

int main()
{
    vector<int> arr = {11, 33, 33, 11, 33, 11};
    vector<int> ans = majorityElement(arr);
    cout << "The majority elements are: ";
    for (auto it : ans)
        cout << it << " ";
    cout << "\n";
    return 0;
}
```

# Better
- Use Hashing
- TC => O(N) , SC => O(N)

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        Map<Integer,Integer> mp= new HashMap<>();
        List<Integer> ans = new ArrayList<>();
        for(int i=0;i<nums.length;i++){
            if(mp.containsKey(nums[i])== true){
                mp.put(nums[i],mp.get(nums[i])+1);
            }
            else{
                mp.put(nums[i],1);
            }
        }
        for(HashMap.Entry<Integer,Integer> en:mp.entrySet()){
            if(en.getValue() > nums.length/3){
                ans.add(en.getKey());
            }
        }
        return ans;
    }
}
```

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        Map<Integer,Integer> mp= new HashMap<>();
        List<Integer> ans = new ArrayList<>();
        for(int i=0;i<nums.length;i++){
            if(mp.containsKey(nums[i])== true){
                mp.put(nums[i],mp.get(nums[i])+1);
            }
            else{
                mp.put(nums[i],1);
            }
            if(mp.get(nums[i])==nums.length/3 + 1){
                ans.add(nums[i]);
            }
            if(ans.size() == 2) break;
        }
        return ans;
    }
}
```

# Best
- TC => O(N) , SC => O(1)

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        vector<int> ans;
        int cnt1=0,cnt2=0,ele1=0,ele2=0;
        for(int i=0;i<nums.size();i++){
            if(cnt1 == 0 && nums[i]!=ele2){
                ele1= nums[i];
                cnt1 =1;
            }
            else if(cnt2==0 && nums[i]!=ele1){
                ele2 = nums[i];
                cnt2 = 1;
            }
            else if(ele1==nums[i]) cnt1++;
            else if(ele2==nums[i]) cnt2++;
            else {cnt1--;cnt2--;}
        }
        cnt1=0,cnt2=0;
        for(int i=0;i<nums.size();i++){
            if(ele1 == nums[i]) cnt1++;
            else if(ele2 == nums[i]) cnt2++;
            // use else if so that ele1 and ele2 can't be same element.
        }
        int mini = nums.size()/3 + 1;
        if(cnt1 >= mini) ans.push_back(ele1);
        if(cnt2 >= mini) ans.push_back(ele2);
        // here sort takes constant time bcz only 2 elements gets sorted
        sort(ans.begin(),ans.end());
        return ans;
    }
};
```