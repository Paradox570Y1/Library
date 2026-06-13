[42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

**Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]
**Output:** 6
**Explanation:** The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

**Example 2:**

**Input:** height = [4,2,0,3,2,5]
**Output:** 9

**Constraints:**

- `n == height.length`
- `1 <= n <= 2 * 104`
- `0 <= height[i] <= 105`

![[Pasted image 20250124182841.png|400]]

- Brute
	- Left Max can be figured with Prefix max array.
	- Right Max can be figured with Suffix max array.
	- Takes O(2N) space
- Better
	- Just calculate Suffix max array.
	- Calculate prefix max in variable on the go without storing
	- Takes O(N) space
- Optimal
	- 

# Using DP

```java
class Solution {
    public int trap(int[] height) {
        int n = height.length;
        int left[] = new int[n];
        int right[] = new int[n];
        left[0] = height[0];
        right[n-1] = height[n-1];
        for(int i=1;i<n;i++){
            int j = n-i-1;
            left[i] = Math.max(left[i-1],height[i]);
            right[j] = Math.max(right[j+1],height[j]);
        }
        int ans=0;
        for(int i=0;i<n;i++){
            ans+=(Math.min(left[i],right[i])-height[i]);
        }
        return ans;
    }
}
```

## Using Stack (Brute)

```java
class Solution {
    public int trap(int[] height) {
        Stack<Integer> st = new Stack<>();
        int ans=0;
        int n = height.length;
        for(int i=0;i<n;i++){
            while(!st.isEmpty() && height[i]>height[st.peek()]){
                int top = st.pop();
                if(st.isEmpty())break;
                int width = i- st.peek()-1;
                int hight =  Math.min(height[st.peek()],height[i])-height[top];
                ans += (hight*width);
            }
            st.push(i);
        }
        return ans;
    }
}
```
# Better DP 

TC -> O(N)
SC -> O(N)
```java
class Solution {
    public int trap(int[] height) {
        int ans=0;
        if(height.length<=2)return ans;
        int n = height.length;
        int arr[] = new int[n];
        arr[n-1]=height[n-1];
        for(int i=n-2;i>=0;i--){
            arr[i] = Math.max(height[i],arr[i+1]);
        }
        int maxi = height[0];
        
        for(int i=1;i<height.length-1;i++){
            int maxBoundry = Math.max(maxi,arr[i+1]);
            int minBoundry = Math.min(maxi,arr[i+1]);
            if(maxBoundry>height[i] && minBoundry>height[i]) ans += (minBoundry-height[i]);
            maxi = Math.max(maxi,height[i]);
        }
        return ans;
    }
}
```


# Optimal Using Two pointer

```java
class Solution {
    public int trap(int[] height) {
        int n = height.length;
        int i=0,j=n-1,cnt=0;
        int leftBound = height[i],rightBound = height[j];
        while(i!=j){
            if(leftBound<=rightBound){
                if(leftBound>height[i+1])cnt += (leftBound-height[i+1]);
                else leftBound = height[i+1];
                i++;
            }
            else{
                if(rightBound>height[j-1])cnt += (rightBound-height[j-1]);
                else rightBound = height[j-1];
                j--;                
            }
        }
        return cnt;
    }
}
```

or

```java
class Solution {
    public int trap(int[] height) {
        int n = height.length;
        int i = 0;
        int j = n-1;
        int ans = 0;
        int leftMax=height[i];
        int rightMax=height[j];
        while(i<j){
            if(leftMax<= rightMax && i+1<n){
                int val = leftMax-height[i+1];
                if(val<0)leftMax = height[i+1];
                else ans+=val;
                i++;
            }
            else if(j-1>=0){
                int val = rightMax-height[j-1];
                if(val<0)rightMax = height[j-1];
                else ans+=val;
                j--;
            }
        }
        return ans;
    }
}
```