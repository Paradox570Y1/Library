[Link](https://www.geeksforgeeks.org/problems/square-root/0)
Given an integer **n,** find the square root of n. If **n** is not a perfect square, then return the floor value.

> Floor value of any number is the greatest Integer which is less than or equal to that number

**Examples:**

**Input:** n = 5
**Output:** 2
**Explanation:** Since, 5 is not a perfect square, floor of square_root of 5 is 2.

**Input:** n = 4
**Output:** 2
**Explanation:** Since, 4 is a perfect square, so its square root is 2.

**Expected Time Complexity:** O(logn)  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
1 ≤ n ≤ 107

# Brute
```cpp
// Function to find square root
// x: element to find square root
class Solution {
  public:
    long long int floorSqrt(long long int n) {
        // Your code goes here
        long long i=1;
        long long ans;
        while(i*i<=n){
            ans = i;
            i++;
        }
        return ans;
    }
};
```
# Optimal
Mine
```cpp
// Function to find square root
// x: element to find square root
class Solution {
  public:
    long long int floorSqrt(long long int n) {
        // Your code goes here
        long long low = 1,high=n;
        while(low<=high){
            long long mid= low+(high-low)/2;
            if(mid*mid<=n && (mid+1)*(mid+1)>n) return mid;
            else if(mid*mid>n) high=mid-1;
            else low = mid+1;
        }
        return -1;
    }
};
```
Striver's
![[Pasted image 20240926093847.png|200]]
```cpp
class Solution {
  public:
    long long int floorSqrt(long long int n) {
        // Your code goes here
        long long low = 1,high=n;
        long long int ans=-1;
        while(low<=high){
            long long mid= low+(high-low)/2;
            if(mid*mid<=n) {
                ans = mid;
                low++;
            }
            else high =mid-1;
        }
        return ans;
    }
};
```

OR

```java
class Solution {
    int floorSqrt(int n) {
        // code here
        int i=1;
        int j=n;
        while(i<=j){
            int m= i+(j-i)/2;
            if(m*m <= n){
                i=m+1;
            }
            else j = m-1;
        }
        return j;
    }
}
```