  
[1539. Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number/)

Given an array `arr` of positive integers sorted in a **strictly increasing order**, and an integer `k`.

Return _the_ `kth` _**positive** integer that is **missing** from this array._

**Example 1:**

**Input:** arr = [2,3,4,7,11], k = 5
**Output:** 9
**Explanation:** The missing positive integers are [1,5,6,8,9,10,12,13,...]. The 5th missing positive integer is 9.

**Example 2:**

**Input:** arr = [1,2,3,4], k = 2
**Output:** 6
**Explanation:** The missing positive integers are [5,6,7,...]. The 2nd missing positive integer is 6.

**Constraints:**

- `1 <= arr.length <= 1000`
- `1 <= arr[i] <= 1000`
- `1 <= k <= 1000`
- `arr[i] < arr[j]` for `1 <= i < j <= arr.length`


# Brute
TC=> n log n
```java
class Solution {
    boolean search(int[] arr,int target){
        int i=0,j=arr.length-1;
        while(i<=j){
            int m = i + (j-i)/2;
            if(target == arr[m]) return true;
            else if(target>arr[m]) i = m+1;
            else j = m-1;
        }
        return false;
    }
    public int findKthPositive(int[] arr, int k) {
	    int l = arr[arr.length-1];
        int cnt=0;
        for(int i=1;i<=l+k;i++){
            if(search(arr,i))continue;
            else cnt++;
            if(cnt==k) return i;
        }
        return -1;
    }
}
```

TC => O(N)
```java
class Solution {

    public int findKthPositive(int[] arr, int k) {
        if(arr[0]-1 > 0){
            if(arr[0]-1 >= k) return k;
            else k = k- (arr[0]-1);
        }
        int cnt=0;
        for(int i=1;i<arr.length;i++){
            if(arr[i]-arr[i-1]>1){
                int diff = arr[i]-arr[i-1]-1;
                if(k>diff)k-=diff;
                else return arr[i-1]+k;
            }
        }
        return arr[arr.length-1]+k;
    }
}
```

```java
class Solution {
public:
    int findKthPositive(vector<int>& arr, int k) {
        int missCnt =0;
        int i=0;
        int missNo = 1;
        while(i<arr.size()){
            if(arr[i] == missNo) i++;
            else missCnt++;
            if(missCnt == k) return missNo;
            missNo++;
        }
        missCnt++;
        while(missCnt<k){
             missNo++;
             missCnt++;
        }
        return missNo;
    }
};
```
# Better

```java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        int st=1;
        int cnt=0;
        for(int ele:arr){
            if(ele!=st){
                if(cnt+ele-st>=k){
                    return st+k-cnt-1;
                }
                cnt+=(ele-st);
                st=ele+1;
            }
            else st++;
        }
        return st+k-cnt-1;
    }
}
```

```java
class Solution {

    public int findKthPositive(int[] arr, int k) {
        for(int i=0;i<arr.length;i++){
            if(arr[i]>k)return k;
            else k++;
        }
        return k;
    }
}
```

# Optimal
```java
class Solution {

    public int findKthPositive(int[] arr, int k) {
        int n=  arr.length;
        int low=0,high=n-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int diff=arr[mid]-mid-1;
            if(diff>=k) high=mid-1;
            else low = mid+1;
        }
        if(high==-1) return k;
        return high+k+1;
        // arr[high]+k-(arr[high]-high-1)
    }
}
```

```java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        int n=  arr.length;
         int low = 0, high = n - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
            int missing = arr[mid] - (mid + 1);
            if (missing < k) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return k + high + 1; //or low +1
    }
}
```

```java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        int n=  arr.length;
        int low=0,high=n-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            int diff=arr[mid]-mid-1;
            if(diff>=k) high=mid-1;
            else low = mid+1;
        }

        return low+k; // or high+k+1
    }
}
```