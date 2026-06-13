[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = [[1,3],[2,6],[8,10],[15,18]]
**Output:** [[1,6],[8,10],[15,18]]
**Explanation:** Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

**Example 2:**

**Input:** intervals = [[1,4],[4,5]]
**Output:** [[1,5]]
**Explanation:** Intervals [1,4] and [4,5] are considered overlapping.

**Constraints:**

- `1 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 104`

# Better
TC-> O(N logN) + O(N)
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals,(a,b)->a[0]-b[0]);
        ArrayList<int[]> li = new ArrayList<>();
        int n = intervals.length;
        int newInterval[] = intervals[0];
        for(int i=1;i<n;i++){
            int lx = newInterval[0];
            int ly = newInterval[1];
            int rx = intervals[i][0];
            int ry = intervals[i][1];
            if(ly>=rx){
                newInterval[0] = Math.min(lx,rx);
                newInterval[1] = Math.max(ly,ry);
            }
            else{
                li.add(newInterval);
                newInterval = intervals[i];
            }
        }
        li.add(newInterval);
        n = li.size();
        int[][] ans = new int[n][2];
        for(int i=0;i<n;i++){
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
        Arrays.sort(intervals,(a,b)->a[0]-b[0]);
        ArrayList<int[]> li = new ArrayList<>();
        int n = intervals.length;
        int newInterval[] = intervals[0];
        for(int i=1;i<n;i++){
            int ly = newInterval[1];
            if(ly>=intervals[i][0]){
                newInterval[1] = Math.max(ly,intervals[i][1]);
            }
            else{
                li.add(newInterval);
                newInterval = intervals[i];
            }
        }
        li.add(newInterval);
        n = li.size();
        int[][] ans = new int[n][2];
        for(int i=0;i<n;i++){
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
        Arrays.sort(intervals,(a,b)->a[0]-b[0]);
        ArrayList<int[]> li = new ArrayList<>();
        int n = intervals.length;
        int newInterval[] = intervals[0];
        for(int[] interval:intervals){
            if(newInterval[1]>=interval[0]){
                newInterval[1] = Math.max(newInterval[1],interval[1]);
            }
            else{
                li.add(newInterval);
                newInterval = interval;
            }
        }
        li.add(newInterval);
        n = li.size();
        int[][] ans = new int[n][2];
        for(int i=0;i<n;i++){
            ans[i] = li.get(i);
        }
        return ans;
    }
}
```

