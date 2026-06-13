[Link](https://www.geeksforgeeks.org/problems/find-nth-root-of-m5843/1)
You are given 2 numbers **(n , m)**; the task is to find **n√m** (nth root of m).  
 
**Example 1:**

**Input:** n = 2, m = 9
**Output:** 3
**Explanation:** 32 = 9

**Example 2:**

**Input:** n = 3, m = 9
**Output:** -1
**Explanation:** 3rd root of 9 is not
integer.

**Your Task:**  
You don't need to read or print anyhting. Your task is to complete the function **NthRoot()** which takes n and m as input parameter and returns the nth root of m. If the root is not integer then returns -1.  
 

**Expected Time Complexity:** O(n* log(m))  
**Expected Space Complexity:** O(1)  
 

**Constraints:**  
1 <= n <= 30  
1 <= m <= 109

# Brute
```java
import java.util.*;
public class tUf {
    // Power exponential method:
    public static long func(int b, int exp) {
        long  ans = 1;
        long base = b;
        while (exp > 0) {
            if (exp % 2 == 1) {
                exp--;
                ans = ans * base;
            } else {
                exp /= 2;
                base = base * base;
            }
        }
        return ans;
    }

    public static int NthRoot(int n, int m) {
        //Use linear search on the answer space:
        for (int i = 1; i <= m; i++) {
            long val = func(i, n);
            if (val == (long)m) return i;
            else if (val > (long)m) break;
        }
        return -1;
    }
}
```
# Optimal
**Time Complexity:** O(log M*logN) = size of the given array.**Reason:** We are basically using binary search to find the minimum.

**Space Complexity:** O(1)**Reason:** We have not used any extra data structures, this makes space complexity, even in the worst case as O(1).

Striver's
```cpp
#include<bits/stdc++.h>
using namespace std;
class Solution{
	public:
	int func(int f,int num,int m){
	    long long ans=1;
	    for(int i=1;i<=f;i++){
	        ans*=num;
	        if(ans>m) return 2;
	    }
	    if(ans==m)return 1;
	    return 0;
	}
	int NthRoot(int n, int m)
	{
	    // Code here.
	    int low = 1,high=m;
	    int ans=-1;
	    while(low<=high){
	        int mid=low+(high-low)/2;
	        if(func(n,mid,m)==1) return mid;
	        else if(func(n,mid,m)==2) high = mid-1;
	        else low = mid+1;
	    }
	    return ans;
	}  
};
```

my way
```cpp
class Solution{
	public:
	int NthRoot(int n, int m)
	{
	    // Code here.
	    int low = 1,high=m;
	    int ans=-1;
	    while(low<=high){
	        int flag=0;
	        int mid= low+(high-low)/2;
	        long long cmp=1;
	        for(int i=0;i<n;i++) {cmp *=mid;
	            if(cmp>m){flag=1;break;}
	        }
	        if(flag==0 && cmp<=m){
	            if(cmp==m){
	            ans = mid;
	            break;
	            }
	            low++;
	        }
	        else high=mid-1;
	    }
	    return ans;
	}  
};
```

OR

```java
class Solution {
    public int nthRoot(int n, int m) {
        // code here
        int low = 1;
        int high = m;
        int ans=-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int pow = (int)Math.pow(mid,n);
            if(pow <= m){
                if(pow==m)ans=mid;
                low=mid+1;
            }
            else high = mid-1;
        }
        return ans;
    }
}
```