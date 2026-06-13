[57. Insert Interval](https://leetcode.com/problems/insert-interval/)

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` _after the insertion_.

**Note** that you don't need to modify `intervals` in-place. You can make a new array and return it.

**Example 1:**

**Input:** intervals = [[1,3],[6,9]], newInterval = [2,5]
**Output:** [[1,5],[6,9]]

**Example 2:**

**Input:** intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
**Output:** [[1,2],[3,10],[12,16]]
**Explanation:** Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].


# Optimal

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        int start=-1;
        int n = intervals.length;
        if(n==0){
            return new int[][]{newInterval};
        }
        for(int i=0;i<n;i++){
            if(intervals[i][0]>newInterval[0]){
                start = i;
                break;
            }
            if(i==n-1){
                start=n;
            }
        }
        start--;
        if(start==-1)start=0;
        if(intervals[start][1]<newInterval[0])start++;
        int end = start;
        for(int i=end;i<n;i++){
            if(intervals[i][1]>newInterval[1]){
                end = i;
                break;
            }
            if(n-1==i)end=n-1;
        }
        if(end==n)end=n-1;
        if(intervals[end][0]>newInterval[1])end--;
        boolean merge = true;
        if(end==-1 || start == n){
            merge=false;
        }
        else if(intervals[start][0]>newInterval[1]){
            if(start<=end)end--;
            merge=false;
        }
        else if(intervals[end][1]<newInterval[0]){
            start++;
            merge=false;
        }
        int ans[][] = new int[n-(end-start)][2];
        int k=0;
        for(int i=0;i<start;i++){
            ans[k] = intervals[i];
            k++;
        }
        
        if(merge){
            ans[k][0] = Math.min(intervals[start][0],newInterval[0]);
            ans[k][1] = Math.max(intervals[end][1],newInterval[1]);
            k++;
        }
        else{
            ans[k] = newInterval;
            k++;
        }
        for(int i=end+1;i<n;i++){
            ans[k] = intervals[i];
            k++;
        }
        return ans;
    }
}
```


# Optimal with much better readability

Although takes O(n) extra space
```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        ArrayList<int[]> li = new ArrayList<>();
        int i=0;
        int n= intervals.length;
        while(i<n && intervals[i][1]<newInterval[0]){
            li.add(intervals[i]);
            i++;
        }
        while(i<n && intervals[i][0]<=newInterval[1]){
            newInterval[0] = Math.min(newInterval[0],intervals[i][0]);
            newInterval[1] = Math.max(newInterval[1],intervals[i][1]);
            i++;
        }
        li.add(newInterval);
        while(i<n){
            li.add(intervals[i]);
            i++;
        }
        int size = li.size();
        int ans[][] = new int[size][2];
        for(int j=0;j<size;j++){
            ans[j] = li.get(j);
        }
        return ans;
    }
}
```