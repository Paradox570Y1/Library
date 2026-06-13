Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

**Example 1:**

**Input:** nums = [2,7,11,15], target = 9
**Output:** [0,1]
**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].


**Example 2:**

**Input:** nums = [3,2,4], target = 6
**Output:** [1,2]

**Example 3:**

**Input:** nums = [3,3], target = 6
**Output:** [0,1]

**Constraints:**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **Only one valid answer exists.**
## Brute Force
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int ans[] = new int[2];
        int n = nums.length;
        for(int i=0;i<n;i++)   {
            for(int j=i+1;j<n;j++){
                if(nums[i]+nums[j] == target){
                    ans[0]=i;
                    ans[1]=j;
                    return ans;
                }
            }
        }
        return ans;
    }
}
```
- Slightly better but still O(N²)
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int ans[] = new int[2];
        int n = nums.length;
        for(int i=0;i<n;i++)   {
            for(int j=i+1;j<n;j++){
                if(nums[i]+nums[j] == target){
                    ans[0]=i;
                    ans[1]=j;
                    return ans;
                }
            }
        }
        return ans;
    }
}
```
![[Pasted image 20240715115337.png|200]]

## Better Approach (Using Hashing with map)
#### ### **Single-Pass Hash Table Approach**

**Time Complexity:** O(N), where N = size of the array.  
**Reason:** The loop runs N times in the worst case and searching in a hashmap takes O(1) generally. So the time complexity is O(N).

**Note:** In the worst case(which rarely happens), the unordered_map takes **O(N)** to find an element. In that case, the time complexity will be **O(N****2****)**. If we use map instead of unordered_map, the time complexity will be **O(N* logN)** as the map data structure takes logN time to find an element.

**Space Complexity:** O(N) as we use the map data structure.

**Note:** We have optimized this problem enough. But if in the interview, we are not allowed to use the map data structure, then we should move on to the following approach i.e. two pointer approach. This approach will have the same time complexity as the better approach.

- Varity 1 : To find the Index
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int ans[] = new int[2];
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            int rem = target - nums[i];
            if(map.containsKey(rem)){
                ans[0] = map.get(rem);
                ans[1] = i;
            }
            map.put(nums[i],i);
        }
        return ans;
    }
}
```

- Variety 2: To find if sum is equal to target or not
```java

public class tUf {
    public static String twoSum(int n, int []arr, int target) {
        HashMap<Integer, Integer> mpp = new HashMap<>();
        for (int i = 0; i < n; i++) {
            int num = arr[i];
            int moreNeeded = target - num;
            if (mpp.containsKey(moreNeeded)) {
                return "YES";
            }

            mpp.put(arr[i], i);
        }
        return "NO";
    }
```

## Optimal Approach (Only for variety 2)
Variety 2: To find if sum is equal to target or not
```cpp
string read(int n, vector<int> book, int target)
{
    int i=0,j=n-1;
    sort(book.begin(),book.end());
    while(i<j){
        int sum = book[i]+book[j];
        if(sum>target){
            j--;
        }
        else if(sum<target){
            i++;
        }
        else{
            return "YES";
        }
    }
    return "NO";
}
```

**Note:** _For variety 1, we can store the elements of the array along with its index in a new array. Then the rest of the code will be similar. And while returning, we need to return the stored indices instead of returning “YES”. But for this variant, the recommended approach is approach 2 otherwise it will increase the space complexity i.e. hashing approach._