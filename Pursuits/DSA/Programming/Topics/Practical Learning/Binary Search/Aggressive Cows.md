[Link](https://www.geeksforgeeks.org/problems/aggressive-cows/1)
Difficulty: **Hard**

You are given an **array** consisting of **n integers** which denote the position of a **stall**. You are also given an **integer** **k** which denotes the number of aggressive cows. You are given the task of **assigning stalls to k cows** such that the **minimum distance between any two of them is the maximum possible**.  
The first line of input contains two space-separated integers **n** and **k**.  
The second line contains **n** space-separated integers denoting the position of the stalls.

**Example 1:**

**Input:**
n=5 
k=3
stalls = [1 2 4 8 9]
**Output:**
3
**Explanation:**
The first cow can be placed at stalls[0], 
the second cow can be placed at stalls[2] and 
the third cow can be placed at stalls[3]. 
The minimum distance between cows, in this case, is 3, 
which also is the largest among all possible ways.

**Example 2:**

**Input:**
n=5 
k=3
stalls = [10 1 2 7 5]
**Output:**
4
**Explanation:**
The first cow can be placed at stalls[0],
the second cow can be placed at stalls[1] and
the third cow can be placed at stalls[4].
The minimum distance between cows, in this case, is 4,
which also is the largest among all possible ways.

**Your Task:**  
Complete the function int solve(), which takes integer n, k, and a vector stalls with n integers as input and returns the largest possible minimum distance between cows.

**Expected Time Complexity:** O(n*log(10^9)).  
**Expected Auxiliary Space:** O(1).  
  
**Constraints:**  
2 <= n <= 10^5  
2 <= k <= n  
0 <= stalls[i] <= 10^9


# Brute
```java
import java.util.*;
public class tUf {
    public static boolean canWePlace(int[] stalls, int dist, int cows) {
        int n = stalls.length; //size of array
        int cntCows = 1; //no. of cows placed
        int last = stalls[0]; //position of last placed cow.
        for (int i = 1; i < n; i++) {
            if (stalls[i] - last >= dist) {
                cntCows++; //place next cow.
                last = stalls[i]; //update the last location.
            }
            if (cntCows >= cows) return true;
        }
        return false;
    }
    public static int aggressiveCows(int[] stalls, int k) {
        int n = stalls.length; //size of array
        //sort the stalls[]:
        Arrays.sort(stalls);

        int limit = stalls[n - 1] - stalls[0];
        for (int i = 1; i <= limit; i++) {
            if (canWePlace(stalls, i, k) == false) {
                return (i - 1);
            }
        }
        return limit;
    }
}
```
# Optimal

```js
class Solution {
        public static int cntCows(int arr[],int threshold){
            int cnt=1;
            int start=0;
            for(int i=1;i<arr.length;i++){
                if(arr[i]-arr[start] >=threshold){
                    cnt++;
                    start = i;
                }
            }
            return cnt;
        }
        public static int aggressiveCows(int[] stalls, int k) {
            // code here
            Arrays.sort(stalls);
            int low = 1;
            int high = stalls[stalls.length-1] - stalls[0];
            int ans=0;
            while(low<=high){
                int mid = (low+high)>>1;
                int cowsCnt = cntCows(stalls,mid);
                if(cowsCnt>=k){
                    ans = mid;
                    low = mid+1;
                }
                else high = mid-1;
            }
            return ans;
        }
    }
```

```cpp
class Solution {
public:
    int func(vector<int> &v,int limit){
        int cnt=1,last=v[0];
        for(int i=1;i<v.size();i++){
            if(v[i]-last>=limit){
                cnt++;
                last = v[i];
            }
        }
        return cnt;
    }
    int solve(int n, int k, vector<int> &v) {
    
        // Write your code here
        sort(v.begin(),v.end());
        int low = 1;
        int high = v[n-1]-v[0];
        while(low<=high){
            int mid = (low+high)>>1;
            if(func(v,mid)<k){
                high = mid-1;
            }
            else low = mid+1;
        }
        return high;
    }
};

```

```java
class Solution {
    static int func(int[] arr,int gap,int c){
		int last = arr[0],n=arr.length;
		for(int i=1;i<n;i++){
			int diff = arr[i] -last;
			if(diff>=gap){
			    c--;
			    last=arr[i];
			}
			if(c==0 )return 1;
		}
		return 0;
	}
    public static int solve(int n, int k, int[] arr) {
        Arrays.sort(arr);
		int low = 1, high = arr[n-1]-arr[0];
		if(k>n)return -1;
		int ans=-1;
		while(low<=high){
			int mid = low + (high-low)/2;
			if(func(arr,mid,k-1)==1){
			    ans = mid;
			    low = mid+1;
			}
			else high = mid-1;
		}
		return ans; // can also return high
    }
}
```

```java
// User function Template for Java
class Solution {
    static int func(int[] arr,int gap,int c){
		int last = 0,n=arr.length;
		for(int i=1;i<n;i++){
			int diff = arr[i] -arr[last];
			if(diff>=gap){
			    c--;
			    last=i;
			}
			if(c==0 )return 1;
		}
		return 0;
	}
    public static int solve(int n, int k, int[] arr) {
        Arrays.sort(arr);
		int low = 1, high = arr[n-1]-arr[0];
		if(k>n)return -1;
		int ans=-1;
		while(low<=high){
			int mid = low + (high-low)/2;
			if(func(arr,mid,k-1)==1){
			    low = mid+1;
			}
			else high = mid-1;
		}
		return high;
    }
}
```



```java
// User function Template for Java
class Solution {
    private static int cntCows(int[] arr,int dist){
        int cows=1;
        int p=0;
        int n= arr.length;
        for(int i=1;i<n;i++){
            if(arr[i]-arr[p]>=dist){
                cows++;
                p=i;
            }
        }
        return cows;
    }
    public static int aggressiveCows(int[] stalls, int k) {
        // code here
        int n = stalls.length;
        Arrays.sort(stalls);
        int low = 1;
        int high = stalls[n-1] - stalls[0];
        while(low<=high){
            int mid = low + (high-low)/2;
            if(cntCows(stalls,mid)>=k){
                low = mid+1;
            }
            else high = mid-1;
        }
        return low-1;
    }
}
```