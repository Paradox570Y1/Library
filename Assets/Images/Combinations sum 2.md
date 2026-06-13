[40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

**Example 1:**

**Input:** candidates = [10,1,2,7,6,1,5], target = 8
**Output:** 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]

**Example 2:**

**Input:** candidates = [2,5,2,1,2], target = 5
**Output:** 
[
[1,2,2],
[5]
]

**Constraints:**

- `1 <= candidates.length <= 100`
- `1 <= candidates[i] <= 50`
- `1 <= target <= 30`


# Brute
`TC-> O(nlogn+2^n⋅k⋅m)`
1. O(2n) for recursive calls.
2. O(k⋅m⋅2^n) for checking duplicates with `ans.contains(list)`.
3. O(nlog⁡n)  for sorting.

`O(2n⋅n)
`
>n is the length of the array.
k is the number of combinations already present in the `ans` list.
m is the average size of a combination.


```java
class Solution {
    void generate(int[] arr,int target,int i,List<List<Integer>> ans,List<Integer> list){
        if(i==arr.length){
            if(target == 0 && !ans.contains(list))ans.add(new ArrayList<>(list));
            return;
        }
        generate(arr,target,i+1,ans,list);
        if(arr[i]<=target){
            list.add(arr[i]);
            generate(arr,target-arr[i],i+1,ans,list);
            list.remove(list.size()-1);
        }
    }
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(candidates);
        generate(candidates,target,0,ans,new ArrayList<>());
        return ans;
    }
}
```

>Little better to use HashMap to remove duplicates

TC->O(nlogn+2^n+k⋅m)
- **Recursive Calls**: O(2^n)
- **Sorting the Array**: O(nlog⁡n)
- **Conversion to `List`**: O(k⋅m)
```java
class Solution {
    void generate(int[] arr,int target,int i,HashSet<List<Integer>> ans,List<Integer> list){
        if(i==arr.length){
            if(target == 0)ans.add(new ArrayList<>(list));
            return;
        }
        generate(arr,target,i+1,ans,list);
        if(arr[i]<=target){
            list.add(arr[i]);
            generate(arr,target-arr[i],i+1,ans,list);
            list.remove(list.size()-1);
        }
    }
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        HashSet<List<Integer>> ans = new HashSet<>();
        Arrays.sort(candidates);
        generate(candidates,target,0,ans,new ArrayList<>());
        List<List<Integer>> li = new ArrayList<>(ans);
        return li;
    }
}
```


# Better
TC-> O(2^n⋅n)
SC-> O(2^n.n)
```java
class Solution {
    void generate(int[] arr,int target,int i,List<List<Integer>> ans,List<Integer> list){

        if(target == 0){
	            ans.add(new ArrayList<>(list));
            return;
        }
        for(int j=i;j<arr.length;j++){
            if(j>i && arr[j] == arr[j-1])continue;
            if(arr[i]>target)break;
            list.add(arr[j]);
            generate(arr,target-arr[j],j+1,ans,list);
            list.remove(list.size()-1);
        }
    }
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(candidates);
        generate(candidates,target,0,ans,new ArrayList<>());
        return ans;
    }
}
```

# Optimal

```java
class Solution {
    int target;
    private void helper(int[] arr,int j,List<List<Integer>> ans,List<Integer> li,int sum){
        int n = arr.length;
        if(sum==target){
            ans.add(new ArrayList<>(li));
            return;
        }
        for(int i=j;i<n;i++){
            if(i>j && arr[i] == arr[i-1])continue;
            if(sum+arr[i]>target)return;
            li.add(arr[i]);
            helper(arr,i+1,ans,li,sum+arr[i]);
            li.remove(li.size()-1);
        }
    }
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        this.target=target;
        Arrays.sort(candidates);
        List<List<Integer>> ans = new ArrayList<>();
        helper(candidates,0,ans,new ArrayList<>(),0);
        return ans;
    }
}
```