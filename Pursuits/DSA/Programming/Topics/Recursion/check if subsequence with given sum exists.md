[Link](https://www.naukri.com/code360/problems/subset-sum_630213?leftPanelTabValue=PROBLEM)
## Problem statement

Send feedback

You are given an array 'A' of 'N' integers. You have to return true if there exists a subset of elements of 'A' that sums up to 'K'. Otherwise, return false.

  

**For Example**

```
'N' = 3, 'K' = 5, 'A' = [1, 2, 3].
Subset [2, 3] has sum equal to 'K'.
So our answer is True.
```

Detailed explanation ( Input/output format, Notes, Images )

**Sample Input 1 :**

```
4 13
4 3 5 2
```

**Sample Output 1 :**

```
No
```

**Sample Input 2 :**

```
5 14
4 2 5 6 7
```

**Sample Output 2 :**

```
Yes
```

**Constraints :**

```
1 <= 'N' <= 10^3
1 <= 'A[i]' <= 10^3
1 <= 'K' <= 10^3
Time Limit: 1 sec
```

# Using Recursion
TC-> O(2^n)
```java
public class Solution {
    static boolean checkSubset(int[] arr,int target,int i){
        if(target==0)return true;
        if(i==0)return (target==arr[i]);
        //not pick
        if(checkSubset(arr,target,i-1))return true;
        //pick
        if(arr[i]<=target){
            if(checkSubset(arr,target-arr[i],i-1))return true;
        }
        return false;
    }
    public static boolean isSubsetPresent(int n, int k,int []a) {
        // Write your code here
        return checkSubset(a,k,n-1);
    }
}
```

Little Better
```java
public class Solution {
    static boolean check(int i,int target,int[] arr,int sum){
        if(target<sum)return false;
        if(i==arr.length){
            if(target==sum)return true;
            return false;
        }
        if(check(i+1,target,arr,sum+arr[i]))return true;
        if(check(i+1,target,arr,sum))return true;
        return false;
    }
    public static boolean isSubsetPresent(int n, int k,int []a) {
        // Write your code here
        return check(0,k,a,0);
    }
}
```


# Optimal

```java
public class Solution {
 
    public static boolean isSubsetPresent(int n, int k,int []a) {
        // Write your code here
        int dp[] = new int[k+1];
        dp[0] = 1;
        for(int i=0;i<n;i++){
            for(int j=k;j>=a[i];j--){
                dp[j] += dp[j - a[i]];
            }
        }
        if(dp[k]!=0)return true;
        return false;
    }
}
```

Even better
```java
public class Solution {
 
    public static boolean isSubsetPresent(int n, int k,int []a) {
        // Write your code here
        boolean dp[] = new boolean[k+1];
        dp[0] = true;
        for(int i=0;i<n;i++){
            for(int j=k;j>=a[i];j--){
                dp[j] = dp[j] || dp[j - a[i]];
                if(dp[k])return true;
            }
        }
        
        return false;
    }
}
```