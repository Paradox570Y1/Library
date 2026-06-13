[84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)


Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return _the area of the largest rectangle in the histogram_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

**Input:** heights = [2,1,5,6,2,3]
**Output:** 10
**Explanation:** The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

**Input:** heights = [2,4]
**Output:** 4

**Constraints:**

- `1 <= heights.length <= 105`
- `0 <= heights[i] <= 104`

# using Stack
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        if(n==1)return heights[0];
        Stack<Integer> st = new Stack<>();
        int nse[] = new int[n];
        for(int i=0;i<n;i++){
            nse[i] = n;
            while(!st.isEmpty() && heights[st.peek()]>heights[i]){
                nse[st.pop()] = i;
            }
            st.push(i);
        }
        int maxi = 0;
        st.clear();
        for(int i=0;i<n;i++){
            while(!st.isEmpty() && heights[st.peek()]>heights[i])st.pop();
            int pse = (st.isEmpty())?-1:st.peek();
            int area = heights[i]*(nse[i]-pse-1);
            maxi = Math.max(maxi,area);
            st.push(i);
        }
        return maxi;
    }
}
```

# Implementing Stack using array 
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        if(n==1)return heights[0];
        int[] st = new int[n];
        int nse[] = new int[n];
        int k=-1;
        for(int i=0;i<n;i++){
            nse[i] = n;
            while(k!=-1 && heights[st[k]]>heights[i]){
                nse[st[k--]] = i;
            }
            st[++k] = i;
        }
        int maxi = 0;
        k=-1;
        for(int i=0;i<n;i++){
            while(k!=-1 && heights[st[k]]>heights[i])k--;
            int pse = (k==-1)?-1:st[k];
            int area = heights[i]*(nse[i]-pse-1);
            maxi = Math.max(maxi,area);
            st[++k] = i;
        }
        return maxi;
    }
}
```


# Using Recursion

```java
class Solution {
    int[] heights;
    private int findMin(int i,int j){
        int mini=i;
        for(int k=i;k<=j;k++){
            if(heights[k]<heights[mini]){
                mini = k;
            }
        }
        return mini;
    }
    private int helper(int i,int j){
        if(i==j)return heights[i];
        int idx = findMin(i,j);
        int area = (j-i+1)*heights[idx];
        int left = 0;
        int right = 0;
        if(idx-1>=i)left = helper(i,idx-1);
        if(idx+1<=j)right = helper(idx+1,j);
        return Math.max(area,Math.max(left,right));
    }
    public int largestRectangleArea(int[] heights) {
        this.heights = heights;
        return helper(0,heights.length-1);
    }
}
```


# Using Segmented Trees

```java

```