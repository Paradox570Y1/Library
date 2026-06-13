[78. Subsets](https://leetcode.com/problems/subsets/)

Given an integer array `nums` of **unique** elements, return _all possible_ 

_subsets_

 _(the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** `[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]`

**Example 2:**

**Input:** nums = [0]
**Output:** `[[],[0]]`

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.

>**NOTE**
>There are primarily Three ways of generating sets:
>	1. Make the use of previous generated sets , by adding current element to them.
>	2. Calculate total number of sets then using bit manipulation ,by iterating over the array and figure out whether to add the element or not.
>	3. Use recursion to generate all possible combinations by picking and not picking the element.
# Brute

TC -> O(n x 2^n)
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(new ArrayList<>());
        for(int i=0;i<nums.length;i++){
            ans.add(Arrays.asList(nums[i]));
            int n = ans.size();
            for(int j=1;j<n-1;j++){
                List<Integer> temp = new ArrayList<>(ans.get(j));
                temp.add(nums[i]);
                ans.add(temp);
            }
        }
        return ans;
    }
}
```

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans;
        ans.push_back({});
        for(int i=0;i<nums.size();i++){
            ans.push_back({nums[i]});
            int n = ans.size();
            for(int j=1;j<n-1;j++){
                vector<int> temp(ans[j]);
                temp.push_back(nums[i]);
                ans.push_back(temp);
            }
        }
        return ans;
    }
};
```



# Using Recursion

In Java  (remember that list is passed like a reference even though it is value)

TC -> O(2^n)
**Space Complexity:** O(n), recursion stack.
```java
class Solution {
    void generate(int[] nums,List<List<Integer>> li,List<Integer> temp,int curr){
        if(curr==nums.length){
            li.add(new ArrayList<>(temp));
            return;
        }
        generate(nums,li,temp,curr+1);

        List<Integer> newTemp = new ArrayList<>(temp);
        newTemp.add(nums[curr]);
        generate(nums,li,newTemp,curr+1);
        
    }
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> li = new ArrayList<>();
        generate(nums,li,new ArrayList<>(),0);
        return li;
    }
}
```

More runtime as you are adding then removing also
```java
class Solution {
    void generate(int[] nums,List<List<Integer>> li,List<Integer> temp,int curr){
        if(curr==nums.length){
            li.add(new ArrayList<>(temp));
            return;
        }
        generate(nums,li,temp,curr+1);

        temp.add(nums[curr]);
        generate(nums,li,temp,curr+1);
        temp.remove(temp.size()-1);
    }
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> li = new ArrayList<>();
        generate(nums,li,new ArrayList<>(),0);
        return li;
    }
}
```



In C++
We have only passed answer array as reference
```cpp
class Solution {
private:
    void generate(vector<int> nums,vector<int> subset,vector<vector<int>>& ans,int index){
        if(index == nums.size()){
            ans.push_back(subset);
            return;
        }
        //exclude
        generate(nums,subset,ans,index+1);

        //include
        subset.push_back(nums[index]);
        generate(nums,subset,ans,index+1);
    }
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans;
        vector<int> subset;
        generate(nums,subset,ans,0);
        return ans;
    }
};
```

```java
class Solution {
    public void generate(List<List<Integer>> store,int[] nums,List<Integer> li,int i){
        if(nums.length==i){
            store.add(new ArrayList<>(li));
            return;
        }
        generate(store,nums,li,i+1);
        li.add(nums[nums.length-1-i]);
        generate(store,nums,li,i+1);
        li.remove(li.size()-1);
    }
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> li = new ArrayList<>();
        generate(li,nums,new ArrayList<>(),0);
        return li;
    }
}
```
# Using Bit Manipulation
TC-> O(2^N \* n)
SC-> O(1)   required space for solution O(2^n * N) N is roughly  the size of each subset 
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        int n = nums.length;
        int subsets = 1<<n;
        List<List<Integer>> ans = new ArrayList<>();
        for(int i=0;i<subsets;i++){
            List<Integer> li = new ArrayList<>();
            for(int j=0;j<n;j++){
                if((i&(1<<j))>0)li.add(nums[j]);
            }
            ans.add(li);
        }
        return ans;
    }
}
```