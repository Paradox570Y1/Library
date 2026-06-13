[39. Combination Sum](https://leetcode.com/problems/combination-sum/)

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the 

frequency

 of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

**Input:** candidates = [2,3,6,7], target = 7
**Output:** `[[2,2,3],[7]]`
**Explanation:**
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

**Example 2:**

**Input:** candidates = [2,3,5], target = 8
**Output:** `[[2,2,2,2],[2,3,3],[3,5]]`

**Example 3:**

**Input:** candidates = [2], target = 1
**Output:** []

**Constraints:**

- `1 <= candidates.length <= 30`
- `2 <= candidates[i] <= 40`
- All elements of `candidates` are **distinct**.
- `1 <= target <= 40`



# Brute

**Time Complexity: O(2^t * k)** where t is the target, k is the average length

**Reason:** Assume if you were not allowed to pick a single element multiple times, every element will have a couple of options: pick or not pick which is 2^n different recursion calls, also assuming that the average length of every combination generated is k. (to put length k data structure into another data structure)

Why not (2^n) but (2^t) (where n is the size of an array)?

Assume that there is 1 and the target you want to reach is 10 so 10 times you can “pick or not pick” an element.

**Space Complexity: O(k\*x)**, k is the average length and x is the no. of combinations

```java
class Solution {
    void generate(int[] arr, int target,int i,List<Integer> ele,List<List<Integer>> ans){
        if(i==arr.length){
            if(target==0)ans.add(new ArrayList<>(ele));
            return;
        }
        //pick
        if(arr[i]<=target){
            ele.add(arr[i]);
            generate(arr,target-arr[i],i,ele,ans);
            ele.remove(ele.size()-1);
        }
        // not pick
        generate(arr,target,i+1,ele,ans);

    }
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        generate(candidates,target,0,new ArrayList<>(),ans);
        
        return ans;
    }
}
```


```java
class Solution {
    private void generate(List<List<Integer>> ans,List<Integer> li,int target,int[] arr,int i,int sum){   if(sum>target)return;
        if(i==arr.length){
	            if(sum==target){
                ans.add(new ArrayList<>(li));
            }
            return;
        }
        li.add(arr[i]);
        generate(ans,li,target,arr,i,sum+arr[i]);
        li.remove(li.size()-1);
        generate(ans,li,target,arr,i+1,sum);
    }
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        generate(ans,new ArrayList<>(),target,candidates,0,0);
        return ans;
    }
}
```

OR

```java
class Solution {
    int target;
    private void helper(int[] arr,int i,List<List<Integer>> ans,List<Integer> li,int sum){
        if(sum>target)return;
        if(i==arr.length){
            if(sum == target)ans.add(new ArrayList<>(li));
            return;
        }
        helper(arr,i+1,ans,li,sum);
        li.add(arr[i]);
        helper(arr,i,ans,li,sum+arr[i]);
        li.remove(li.size()-1);
    }
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        this.target=target;
        List<List<Integer>> ans = new ArrayList<>();
        helper(candidates,0,ans,new ArrayList<>(),0);
        return ans;
    }
}
```