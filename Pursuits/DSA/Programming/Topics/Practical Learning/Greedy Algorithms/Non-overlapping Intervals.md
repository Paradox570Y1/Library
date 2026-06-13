	[435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return _the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping_.

**Note** that intervals which only touch at a point are **non-overlapping**. For example, `[1, 2]` and `[2, 3]` are non-overlapping.

**Example 1:**

**Input:** intervals = [[1,2],[2,3],[3,4],[1,3]]
**Output:** 1
**Explanation:** [1,3] can be removed and the rest of the intervals are non-overlapping.

**Example 2:**

**Input:** intervals = [[1,2],[1,2],[1,2]]
**Output:** 2
**Explanation:** You need to remove two [1,2] to make the rest of the intervals non-overlapping.

**Example 3:**

**Input:** intervals = [[1,2],[2,3]]
**Output:** 0
**Explanation:** You don't need to remove any of the intervals since they're already non-overlapping.

**Constraints:**

- `1 <= intervals.length <= 105`
- `intervals[i].length == 2`
- `-5 * 104 <= starti < endi <= 5 * 104`

# Better

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals,(a,b)->a[0]-b[0]);
        int[] newInterval = intervals[0];
        int n = intervals.length;
        int cnt=0;
        for(int i=1;i<n;i++){
            if(newInterval[1]>intervals[i][0]){
                newInterval[1] = Math.min(newInterval[1],intervals[i][1]);
                cnt++;
            }
            else newInterval = intervals[i];
        }
        return cnt;
    }
}
```


# Optimal
sorting according to end of interval will lead to minimum overlapping during process as lesser the end time then lesser is the interval for overlapping
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals,(a,b)->a[1]-b[1]);
        int[] newInterval = intervals[0];
        int n = intervals.length;
        int cnt=0;
        for(int i=1;i<n;i++){
            if(newInterval[1]>intervals[i][0]){
                cnt++;
            }
            else newInterval = intervals[i];
        }
        return cnt;
    }
}
```

OR

After more optimizations
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals,(a,b)->a[1]-b[1]);
        int lastExecTime = intervals[0][1];
        int n = intervals.length;
        int cnt=0;
        for(int i=1;i<n;i++){
            if(lastExecTime>intervals[i][0]){
                cnt++;
            }
            else lastExecTime = intervals[i][1];
        }
        return cnt;
    }
}
```