[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = `[[1,3],[2,6],[8,10],[15,18]]`
**Output:** `[[1,6],[8,10],[15,18]]`
**Explanation:** Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

**Example 2:**

**Input:** intervals =` [[1,4],[4,5]]`
**Output:** `[[1,5]]`
**Explanation:** Intervals [1,4] and [4,5] are considered overlapping.

**Constraints:**

- `1 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 104`

# Brute
**Time Complexity:** O(N*logN) + O(2*N), where N = the size of the given array.  
**Reason:** Sorting the given array takes  O(N*logN) time complexity. Now, after that, we are using 2 loops i and j. But while using loop i, we skip all the intervals that are merged with loop j. So, we can conclude that every interval is roughly visited twice(roughly, once for checking or skipping and once for merging). So, the time complexity will be 2*N instead of N2.

**Space Complexity:** O(N), as we are using an answer list to store the merged intervals. Except for the answer array, we are not using any extra space.

```java
import java.util.*;

public class tUf {

    public static List<List<Integer>> mergeOverlappingIntervals(int[][] arr) {
        int n = arr.length; // size of the array
        //sort the given intervals:
        Arrays.sort(arr, new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                return a[0] - b[0];
            }
        });

        List<List<Integer>> ans = new ArrayList<>();

        for (int i = 0; i < n; i++) { // select an interval:
            int start = arr[i][0];
            int end = arr[i][1];

            //Skip all the merged intervals:
            if (!ans.isEmpty() && end <= ans.get(ans.size() - 1).get(1)) {
                continue;
            }

            //check the rest of the intervals:
            for (int j = i + 1; j < n; j++) {
                if (arr[j][0] <= end) {
                    end = Math.max(end, arr[j][1]);
                } else {
                    break;
                }
            }
            ans.add(Arrays.asList(start, end));
        }
        return ans;
    }

    public static void main(String[] args) {
        int[][] arr = {{1, 3}, {8, 10}, {2, 6}, {15, 18}};
        List<List<Integer>> ans = mergeOverlappingIntervals(arr);
        System.out.print("The merged intervals are: \n");
        for (List<Integer> it : ans) {
            System.out.print("[" + it.get(0) + ", " + it.get(1) + "] ");
        }
        System.out.println();
    }

}
```



# Optimal
**Time Complexity:** O(N*logN) + O(N), where N = the size of the given array.  
**Reason:** Sorting the given array takes  O(N*logN) time complexity. Now, after that, we are just using a single loop that runs for N times. So, the time complexity will be O(N).

**Space Complexity:** O(N), as we are using an answer list to store the merged intervals. Except for the answer array, we are not using any extra space.

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> ans;
        
        sort(intervals.begin(),intervals.end());
        
        for(int i=0;i<intervals.size();i++){
            if(ans.empty() || intervals[i][0] > ans.back()[1]){
                ans.push_back(intervals[i]);
            }
            else {
                ans.back()[1] = max(ans.back()[1],intervals[i][1]);
            } 
        }
        return ans;
    }
};
```

```cpp
//without the following if block the code will work but it saves bit of time in few cases
        if(intervals.size()==1){
            ans.push_back({intervals[0][0],intervals[0][1]});
            return ans;
        }
```

OR
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals,(a,b)->a[0]-b[0]);
        int[] temp = intervals[0];
        int n = intervals.length;
        List<int[]> li = new ArrayList<>();
        for(int i=1;i<n;i++){
            int[] interval = intervals[i];
            if(interval[0]>temp[1]){
                li.add(temp);
                temp = interval;
            }
            else{
                temp[1] = Math.max(temp[1],interval[1]);
            }
        }
        li.add(temp);
        int [][] ans = new int[li.size()][2];
        for(int i=0;i<li.size();i++){
            ans[i] = li.get(i);
        }
        return ans;
    }
}
```


OR

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        ArrayList<int[]> li = new ArrayList<>();
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        int prev[] = {intervals[0][0], intervals[0][1]};
        int n = intervals.length;
        for (int i = 1; i < n ; i++) {
            int cur[] = intervals[i];
            if (prev[1] >= cur[0]) {
                prev[1] = Math.max(prev[1], cur[1]);
            } else {
                li.add(prev);
                prev = cur;
            }
        }
        li.add(prev);
        int ans[][] = new int[li.size()][2];
        for (int i = 0; i < li.size(); i++) {
            ans[i] = li.get(i);
        }
        return ans;
    }
}
```