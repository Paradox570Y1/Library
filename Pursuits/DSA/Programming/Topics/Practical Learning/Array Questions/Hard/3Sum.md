[15. 3Sum](https://leetcode.com/problems/3sum/)
Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]
**Output:** [[-1,-1,2],[-1,0,1]]
**Explanation:** 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

**Example 2:**

**Input:** nums = [0,1,1]
**Output:** []
**Explanation:** The only possible triplet does not sum up to 0.

**Example 3:**

**Input:** nums = [0,0,0]
**Output:** [[0,0,0]]
**Explanation:** The only possible triplet sums up to 0.

**Constraints:**

- `3 <= nums.length <= 3000`
- `-105 <= nums[i] <= 105`

# Brute
Complexity Analysis

**Time Complexity:** O(N ³* log(no. of unique triplets)), where N = size of the array.  
**Reason:** Here, we are mainly using 3 nested loops. And inserting triplets into the set takes O(log(no. of unique triplets)) time complexity. But we are not considering the time complexity of sorting as we are just sorting 3 elements every time.

**Space Complexity:** O(2 * no. of the unique triplets) as we are using a set data structure and a list to store the triplets.
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        set<vector<int>> st;
        for(int i=0;i<nums.size()-2;i++){
            for(int j=i+1;j<nums.size()-1;j++){
                for(int k=j+1;k<nums.size();k++){
                    if(nums[i]+nums[j]+nums[k] == 0){
                        vector<int> v = {nums[i],nums[j],nums[k]};
                        sort(v.begin(),v.end());
                        st.insert(v);
                    }
                    
                }
            }
        }
        vector<vector<int>> ans(st.begin(),st.end());
        return ans;
    }
};
```

# Better
**Time Complexity:** O(N² * log(no. of unique triplets)), where N = size of the array.  
**Reason:** Here, we are mainly using 3 nested loops. And inserting triplets into the set takes O(log(no. of unique triplets)) time complexity. But we are not considering the time complexity of sorting as we are just sorting 3 elements every time.

**Space Complexity:** O(2 * no. of the unique triplets) + O(N) as we are using a set data structure and a list to store the triplets and extra O(N) for storing the array elements in another set.
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        set<vector<int>> st;
        for(int i=0;i<nums.size()-2;i++){
            set<int> check;
            for(int j=i+1;j<nums.size();j++){
                int num3 = -(nums[i]+nums[j]);
                if(check.find(num3) != check.end()){
                    vector<int> v = {nums[i],nums[j],num3};
                    sort(v.begin(),v.end());
                    st.insert(v);
                }
                check.insert(nums[j]);
                
            }
        }
        vector<vector<int>> ans(st.begin(),st.end());
        return ans;
    }
};
```

OR
- Not very optimal due to using HashSet and then copying elements to ArrayList
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        HashSet<List<Integer>> ans = new LinkedHashSet<>(); 
        //or just Hashset<>()
        int n = nums.length;
        
        for(int i=0;i<n-2;i++){
            HashSet<Integer> hs = new HashSet<>();
            for(int j=i+1;j<n;j++){
                int rem = -(nums[i]+nums[j]);
                if(hs.contains(rem)){
                    List<Integer> li = new ArrayList<>(List.of(nums[i],nums[j],rem));
                    Collections.sort(li);
                    ans.add(li);
                }
                hs.add(nums[j]);
            }
        }
        List<List<Integer>> li = new ArrayList<>(ans);
        return li;
    }
}
```
# Optimal
**Time Complexity:** O(NlogN)+O(N2), where N = size of the array.  
**Reason:** The pointer i, is running for approximately N times. And both the pointers j and k combined can run for approximately N times including the operation of skipping duplicates. So the total time complexity will be O(N2). 

**Space Complexity:** O(no. of quadruplets), **_This space is only used to store the answer. We are not using any extra space to solve this problem._** So, from that perspective, space complexity can be written as O(1).

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        for(int i=0;i<nums.length-2;i++){
            if(i>0 && nums[i] == nums[i-1]) continue;
            int j=i+1,k=nums.length-1;
            while(j<k){
                int sum = nums[i]+nums[j]+nums[k];
                if(sum == 0){
                    List<Integer> li = new ArrayList<>(Arrays.asList(nums[i],nums[j],nums[k]));
                    ans.add(new ArrayList<>(li));
                    j++;k--;
                    while(j<k && nums[j] == nums[j-1])j++;
                    while(j<k && nums[k] == nums[k+1])k--;
                }
                else if(sum>0) k--;
                else j++;
            }
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        int n = nums.length;
        Arrays.sort(nums);
        for(int i=0;i<n-2;i++){
            if(i>0 && nums[i-1] ==nums[i])continue;
            int j=i+1;
            int k=n-1;
            while(j<k){
                int val = nums[i] + nums[j] + nums[k];
                if(val>0){
                    k--;
                }
                else if(val<0){
                    j++;
                }
                else {
                    ans.add(List.of(nums[i],nums[j],nums[k]));
                    k--;j++;
                    while(j<k && nums[j] == nums[j-1])j++;
                    while(j<k && nums[k] == nums[k+1])k--;
                }
            }
        }
        return ans;
    }
}
```


- Using HashSet also you can remove duplicates, but very bad runtime

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        HashSet<List<Integer>> hs = new HashSet<>();
        int n = nums.length;
        Arrays.sort(nums);
        for(int i=0;i<n-2;i++){
            int j=i+1;
            int k=n-1;
            while(j<k){
                int val = nums[i] + nums[j] + nums[k];
                if(val>0){
                    k--;
                }
                else if(val<0){
                    j++;
                }
                else {
                    hs.add(List.of(nums[i],nums[j],nums[k]));
                    k--;j++;
                }
            }
        }
        List<List<Integer>> ans = new ArrayList<>(hs);
        return ans;
    }
}
```