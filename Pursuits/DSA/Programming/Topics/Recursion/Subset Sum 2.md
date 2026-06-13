[90. Subsets II](https://leetcode.com/problems/subsets-ii/)

Given an integer array `nums` that may contain duplicates, return _all possible_ 

_subsets_

 _(the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,2]
**Output:** `[[],[1],[1,2],[1,2,2],[2],[2,2]]`

**Example 2:**

**Input:** nums = [0]
**Output:** `[[],[0]]`

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`


# Brute

```java
class Solution {
    void generate(int[] arr,int i,List<Integer> li,List<List<Integer>> ans){
        if(i==arr.length){
            if(!ans.contains(li))ans.add(new ArrayList<>(li));
            return;
        }
        generate(arr,i+1,li,ans);
        li.add(arr[i]);
        generate(arr,i+1,li,ans);
        li.remove(li.size()-1);
    }
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        generate(nums,0,new ArrayList<>(),ans);
        return ans;
    }
}
```

# Optimal
TC-> O(2^n\*n)
SC-> O(2^n\*n)

Using recursion
```java
class Solution {
    void generate(int[] arr,int idx,List<Integer> li,List<List<Integer>> ans){
        ans.add(new ArrayList<>(li));
        for(int i=idx;i<arr.length;i++){
            if(idx!=i && arr[i] == arr[i-1])continue;
            li.add(arr[i]);
            generate(arr,i+1,li,ans);
            li.remove(li.size()-1);
        }
    }
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        generate(nums,0,new ArrayList<>(),ans);
        return ans;
    }
}
```


Using iterative approach

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(new ArrayList<>());
        int st=0;
        int end=0;
        for(int i=0;i<nums.length;i++){
            if(i>0 && nums[i]==nums[i-1]){
                st= end+1;
            }
            end = ans.size()-1;
            int n = ans.size();
            for(int j=st;j<n;j++){
                List<Integer> temp = new ArrayList<>(ans.get(j));
                temp.add(nums[i]);
                ans.add(new ArrayList<>(temp));
            }
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);
        int st = 0;
        int end = 0;
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(new ArrayList<>());
        for(int i=0;i<n;i++){
            st=0;
            if(i>0 && nums[i] == nums[i-1])st = end;
            end = ans.size();
            for(int j=st;j<end;j++){
                List<Integer> li = new ArrayList<>(ans.get(j));
                li.add(nums[i]);
                ans.add(li);
            }
        }
        return ans;
    }
}
```