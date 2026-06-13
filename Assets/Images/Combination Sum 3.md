[216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)

Find all valid combinations of `k` numbers that sum up to `n` such that the following conditions are true:

- Only numbers `1` through `9` are used.
- Each number is used **at most once**.

Return _a list of all possible valid combinations_. The list must not contain the same combination twice, and the combinations may be returned in any order.

**Example 1:**

**Input:** k = 3, n = 7
**Output:** `[[1,2,4]]`
**Explanation:**
1 + 2 + 4 = 7
There are no other valid combinations.

**Example 2:**

**Input:** k = 3, n = 9
**Output:** `[[1,2,6],[1,3,5],[2,3,4]]`
**Explanation:**
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
There are no other valid combinations.

**Example 3:**

**Input:** k = 4, n = 1
**Output:** []
**Explanation:** There are no valid combinations.
Using 4 different numbers in the range [1,9], the smallest sum we can get is 1+2+3+4 = 10 and since 10 > 1, there are no valid combination.

**Constraints:**

- `2 <= k <= 9`
- `1 <= n <= 60`


# Brute

![[Pasted image 20250105114527.png|300]]

```java
class Solution {
    void generate(int len,int target,List<List<Integer>> ans,List<Integer> li,int num){
        if(len == li.size()){
            if(target == 0)ans.add(new ArrayList<>(li));
            return;
        }
        if(num>9)return;
        generate(len,target,ans,li,num+1);
        if(num<=target){
            li.add(num);
            generate(len,target-num,ans,li,num+1);
            li.remove(li.size()-1);
        }
    }
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> ans= new ArrayList<>();
        generate(k,n,ans,new ArrayList<>(),1);
        return ans;
    }
}
```

# Better

![[Pasted image 20250105115245.png]]
```java
class Solution {
    void generate(int len,int target,List<List<Integer>> ans,List<Integer> li,int num){
        if(target<0)return;
        if(len == li.size()){
            if(target == 0)ans.add(new ArrayList<>(li));
            return;
        }
        if(num>9)return;
        generate(len,target,ans,li,num+1);
        if(num<=target){
            li.add(num);
            generate(len,target-num,ans,li,num+1);
            li.remove(li.size()-1);
        }
    }
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> ans= new ArrayList<>();
        generate(k,n,ans,new ArrayList<>(),1);
        return ans;
    }
}
```


```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> ans = new ArrayList<>();
        helper(ans,new ArrayList<>(),k,n,1,0);
        return ans;
    }
    void helper(List<List<Integer>> ans,List<Integer> li,int k,int target,int i,int sum){
        if(li.size()==k || i==10){
            if(sum==target && li.size()==k)
            ans.add(new ArrayList<>(li));
            return;
        }
        li.add(i);
        helper(ans,li,k,target,i+1,sum+i);
        li.remove(li.size()-1);
        helper(ans,li,k,target,i+1,sum);
    }
}
```


# Optimal

```java
class Solution {
    int target;
    int numLen;
    private void generate(List<List<Integer>> ans,int curLen,int num,List<Integer> li,int sum){
        if(numLen == curLen){
            if(sum == target)ans.add(new ArrayList<>(li));
            return;
        }
        for(int i=num;i<=9;i++){
            if(sum+num>target)return;
            li.add(num);
            generate(ans,curLen+1,i+1,li,sum+num);
            li.remove(li.size()-1);
        }
    }
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> ans = new ArrayList<>();
        this.target = n;
        this.numLen = k;
        generate(ans,0,1,new ArrayList<>(),0);
        return ans;
    }
}
```