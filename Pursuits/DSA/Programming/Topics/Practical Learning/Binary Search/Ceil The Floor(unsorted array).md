**Ceil** of **x** is the smallest element which is greater than or equal to **x**. Ceil of **x** doesn’t exist if **x** is greater than greatest element of **arr[]**.

[Link of Problem](https://www.geeksforgeeks.org/problems/ceil-the-floor2802/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=ceil-the-floor)
Given an unsorted array **arr[]** of integers and an integer **x**, find the floor and ceiling of **x** in **arr[]**.

Return an array of integers denoting the `[floor, ceil]`. Return `-1` for floor or ceiling if the floor or ceiling is not present.

**Examples:**

**Input:** x = 7 , arr[] = [5, 6, 8, 9, 6, 5, 5, 6]
**Output:** 6, 8
**Explanation:** Floor of 7 is 6 and ceil of 7 is 8.

**Input:** x = 10 , arr[] = [5, 6, 8, 8, 6, 5, 5, 6]
**Output:** 8, -1
**Explanation:** Floor of 10 is 8 but ceil of 10 is not possible.

**Expected Time Complexity:** O(n)  
**Expected Auxiliary Space:** O(1)

**Constraints :**  
1 ≤ arr.size ≤ 105  
1 ≤ arr[i], x ≤ 106

# Optimal

```java
class Solution {
    public int[] getFloorAndCeil(int x, int[] arr) {
        // code here
        int[] ans = new int[2];
        ans[0]=-1;
        ans[1]=2147483647;
        boolean flag=true;
        for(int i=0;i<arr.length;i++){
            if(arr[i]<=x){
                ans[0] = Math.max(ans[0],arr[i]);
            }
            if(arr[i]>=x){
                ans[1] = Math.min(ans[1],arr[i]);
                flag=false;
            }
        }
        if(flag)ans[1] =-1;
        return ans;
    }
}

```

OR

```java
class Solution {
    public int[] getFloorAndCeil(int x, int[] arr) {
        // code here
        int ceil=Integer.MAX_VALUE,floor=Integer.MIN_VALUE;
        for(int ele:arr){
            if(ele<=x && floor<ele){
                floor = ele;
            }
            if(ele>=x && ceil>ele){
                ceil = ele;
            }
        }
        if(floor == Integer.MIN_VALUE)floor =-1;
        if(ceil == Integer.MAX_VALUE)ceil = -1;
        return new int[]{floor,ceil};
    }
}
```