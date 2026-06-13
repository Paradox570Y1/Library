[Link](https://www.geeksforgeeks.org/problems/find-missing-and-repeating2512/1)

Difficulty: **Medium**Accuracy: **24.83%**Submissions: **460K+**Points: **4**

Given an unsorted array _arr_ of size n of positive integers. One number '**A**' from set {1, 2,....,N} is missing and one number '**B**' occurs twice in array. Find these two numbers.  
Your task is to complete the function _findTwoElement()_ which takes the array of integers arr and n as parameters and returns an array of integers of size 2 denoting the answer (_The first index contains B and second index contains A_)  

**Examples  
**

**Input:** n = 2 arr[] = {2, 2}
**Output:** 2 1
**Explanation:** Repeating number is 2 and smallest positive missing number is 1.

**Input:** n = 3 arr[] = {1, 3, 3} 
**Output:** 3 2
**Explanation:** Repeating number is 3 and smallest positive missing number is 2.

**Expected Time Complexity:** O(n)  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
2 ≤ n ≤ 105  
1 ≤ arr[i] ≤ n

# Brute
**Time Complexity:** O(N2), where N = size of the given array.  
**Reason:** Here, we are using nested loops to count occurrences of every element between 1 to N.

**Space Complexity:** O(1) as we are not using any extra space.
```java
import java.util.*;

public class tUf {

    public static int[] findMissingRepeatingNumbers(int[] a) {
        int n = a.length; // size of the array
        int repeating = -1, missing = -1;

        //Find the repeating and missing number:
        for (int i = 1; i <= n; i++) {
            //Count the occurrences:
            int cnt = 0;
            for (int j = 0; j < n; j++) {
                if (a[j] == i) cnt++;
            }

            if (cnt == 2) repeating = i;
            else if (cnt == 0) missing = i;

            if (repeating != -1 && missing != -1)
                break;
        }
        int[] ans = {repeating, missing};
        return ans;
    }

    public static void main(String[] args) {
        int[] a = {3, 1, 2, 5, 4, 6, 7, 5};
        int[] ans = findMissingRepeatingNumbers(a);
        System.out.println("The repeating and missing numbers are: {"
                           + ans[0] + ", " + ans[1] + "}");
    }
}
```

# Better
**Time Complexity:** O(2N), where N = the size of the given array.  
**Reason:** We are using two loops each running for N times. So, the time complexity will be O(2N).

**Space Complexity:** O(N) as we are using a hash array to solve this problem.
```java
class Solve {
    int[] findTwoElement(int arr[]) {
        // code here
        int[] ans = new int[2];
        int[] hash = new int[arr.length+1];
        for(int i=0;i<arr.length;i++){
            hash[arr[i]]++;
        }
        for(int i=1;i<=arr.length;i++){
            if(hash[i] ==2) ans[0]=i;
            else if(hash[i]==0) ans[1] =i;
        }
        return ans;
    }
}
```

# Optimal Approach 1 (math)
- use long long to minimize integer overflow.
- For very large input overflow happens.
**Time Complexity:** O(N), where N = the size of the given array.  
**Reason:** We are using only one loop running for N times. So, the time complexity will be O(N).

**Space Complexity:** O(1) as we are not using any extra space to solve this problem.
```cpp
class Solution{
public:
    vector<int> findTwoElement(vector<int> arr, int n) {
        // code here
        long long SN = (n*(n+1))/2;
        long long S2N = (n*(n+1)*(2*n+1))/6;
        long long S=0,S2=0;
        for(int i=0;i<n;i++){
            S += arr[i];
            S2 += ((long long)arr[i] * (long long)arr[i]);
        }
        long long diff = S-SN;
        long long add = (S2-S2N) / diff;
        long long x = (add+diff)/2;
        long long y = x-diff;
        return {(int)x,(int)y };
    }
};
```

OR

```java
class Solution {
    // Function to find two elements in array
    ArrayList<Integer> findTwoElement(int arr[]) {
        // code here
        int n = arr.length;
        long sum = (long)n*(n+1)/2;
        long sumSq = (long)n*(n+1)*(2*n+1)/6;
        long cursum = 0;
        long cursumSq = 0;
        for(int ele:arr){
            cursum += ele;
            cursumSq += ((long)ele*(long)ele);
        }
        long diffSum = sum-cursum;
        long diffSumSq = sumSq - cursumSq;
        long addSum = diffSumSq/diffSum;
        long miss = (diffSum+addSum)/2;
        long repeat = (addSum - miss);
        return new ArrayList<>(List.of((int)repeat,(int)miss));
    }
}
```

# Optimal Approach 2 (xor)
**Time Complexity:** O(N), where N = the size of the given array.  
**Reason:** We are just using some loops running for N times. So, the time complexity will be approximately O(N).

**Space Complexity:** O(1) as we are not using any extra space to solve this problem.
![[Pasted image 20240823125503.png|350]]
![[Pasted image 20240823125636.png|100]]

```cpp
class Solution {
	public:
    vector<int> findTwoElement(vector<int>& arr) {
        // code here
        int xr=0;
        for(int i=0;i<arr.size();i++){
            xr ^= i+1;
            xr ^= arr[i];
        }
        int bit=0;
        
        while(xr>0){
            if(xr&1) break;
            else bit++;
            xr = xr >> 1;
        }
        int x=0,y=0;
        for(int i=0;i<arr.size();i++){
            if((arr[i]>>bit)&1) x^= arr[i];
            else y ^= arr[i];
            if(((i+1)>>bit)&1) x^= i+1;
            else y ^=i+1;
        }
        for(int i=0;i<arr.size();i++){
            if(arr[i] == y) swap(x,y);
        }
        return {x,y};
    }
};
```

```java
class Solve {
    int[] findTwoElement(int arr[], int n) {
        // code here
        int xr=0;
        for(int i=0;i<n;i++){
            xr ^= arr[i];
            xr ^= i+1;
        }
        int bitno=0;
        while((xr & (1<<bitno)) == 0){
            bitno++;
        }
        int zero =0;
        int one = 0;
        for(int i=0;i<n;i++){
            if((arr[i] & (1<<bitno))!=0) one ^= arr[i];
            else zero ^= arr[i];
            
            if((i+1 & (1<<bitno))!=0) one^= i+1;
            else zero ^= i+1;
        }
        // to check which one is repeating no.
        int count=0;
        for(int i=0;i<n;i++){
            if(arr[i] == one) count++;
        }
        if(count==2){
            return new int[]{one,zero};
        }
        else{
            return new int[]{zero,one};
        }
    }
}
```

```java
class Solve {
    int[] findTwoElement(int arr[], int n) {
        // code here
        int xr=0;
        for(int i=0;i<n;i++){
            xr ^= arr[i];
            xr ^= i+1;
        }
        int no= xr & ~(xr-1); // Do xr & -xr
        int zero =0;
        int one = 0;
        for(int i=0;i<n;i++){
            if((arr[i] & no)!=0) one ^= arr[i];
            else zero ^= arr[i];
            
            if((i+1 & no)!=0) one^= i+1;
            else zero ^= i+1;
        }
        // to check which one is repeating no.
        int count=0;
        for(int i=0;i<n;i++){
            if(arr[i] == one) count++;
        }
        if(count==2){
            return new int[]{one,zero};
        }
        else{
            return new int[]{zero,one};
        }
    }
}
```

The expression `~(xr-1)` involves two operations: the bitwise NOT operation (`~`) and the subtraction operation (`- 1`).

1. **`xr - 1`**: This subtracts 1 from the value of `xr`.
    
2. **`~(xr - 1)`**: The `~` operator is the bitwise NOT operator in C++. It inverts all the bits of its operand.


```js
class Solution {
    // Function to find two repeating elements in an array of size n.
    findTwoElement(arr) {
        // code here
        let xor = 0;
        arr.forEach((val,i)=>{
            xor^=val;
            xor^=i+1;
        });
        let bit = xor & ~(xor-1);
        let a=0,b=0;
        arr.forEach((val,i)=>{
            if((val & bit) == 0) a^=val;
            else b^=val;
            if((i+1 & bit) == 0) a^=i+1;
            else b^=i+1;
        });
        for(let ele of arr){
            if(ele==b)[a,b] =[b,a]
        }
        var arr = [a,b];
        return arr;
    }
}
```


OR

```java
class Solution {
    // Function to find two elements in array
    ArrayList<Integer> findTwoElement(int arr[]) {
        // code here
        int n = arr.length;
        int xor=0;
        for(int i=0;i<n;i++){
            xor^=i+1;
            xor^=arr[i];
        }
        int bit = xor & -xor;
        int miss=0;
        int repeat=0;
        for(int i=0;i<n;i++){
            if((arr[i] & bit) !=0){
                miss^=arr[i];
            }
            else{
                repeat^=arr[i];
            }
            if((i+1 & bit)!=0){
                miss^=i+1;
            }
            else repeat^=i+1;
        }
        for(int ele:arr){
            if(repeat==ele)return new ArrayList<>(List.of(repeat,miss));
        }
        return new ArrayList<>(List.of(miss,repeat));
    }
}
```