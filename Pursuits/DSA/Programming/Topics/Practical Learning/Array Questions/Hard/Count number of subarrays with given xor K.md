[Link](https://www.geeksforgeeks.org/problems/count-subarray-with-given-xor/1)
Given an array of integers A and an integer B.

Find the total number of subarrays having bitwise XOR of all elements equals to B.


Problem Constraints
1 <= length of the array <= 105

1 <= A[i], B <= 109


Example Input
Input 1:

 A = [4, 2, 2, 6, 4]
 B = 6
Input 2:

 A = [5, 6, 7, 8, 9]
 B = 5


Example Output
Output 1:

 4
Output 2:

 2
![[Pasted image 20241206084756.png|300]]

# Brute
**Time Complexity:** O(N3) approx., where N = size of the array.  
**Reason:** We are using three nested loops, each running approximately N times.

**Space Complexity:** O(1) as we are not using any extra space.

```java
import java.util.*;

public class tUf {

    public static int subarraysWithXorK(int []a, int k) {
        int n = a.length; //size of the given array.
        int cnt = 0;

        // Step 1: Generating subarrays:
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {

                //step 2:calculate XOR of all
                // elements:
                int xorr = 0;
                for (int K = i; K <= j; K++) {
                    xorr = xorr ^ a[K];
                }

                // step 3:check XOR and count:
                if (xorr == k) cnt++;
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] a = {4, 2, 2, 6, 4};
        int k = 6;
        int ans = subarraysWithXorK(a, k);
        System.out.println("The number of subarrays with XOR k is: " + ans);
    }
}
```


# Better
**Time Complexity:** O(N2), where N = size of the array.  
**Reason:** We are using two nested loops here. As each of them is running for N times, the time complexity will be approximately O(N2).

**Space Complexity:** O(1) as we are not using any extra space.

```java
import java.util.*;

public class tUf {

    public static int subarraysWithXorK(int []a, int k) {
        int n = a.length; //size of the given array.
        int cnt = 0;

        // Step 1: Generating subarrays:
        for (int i = 0; i < n; i++) {
            int xorr = 0;
            for (int j = i; j < n; j++) {

                //step 2:calculate XOR of all
                // elements:
                xorr = xorr ^ a[j];

                // step 3:check XOR and count:
                if (xorr == k) cnt++;
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] a = {4, 2, 2, 6, 4};
        int k = 6;
        int ans = subarraysWithXorK(a, k);
        System.out.println("The number of subarrays with XOR k is: " + ans);
    }
}  
```

# Optimal
**Time Complexity:** O(N) or O(N*logN) depending on which map data structure we are using, where N = size of the array.  
**Reason:** For example, if we are using an unordered_map data structure in C++ the time complexity will be O(N) but if we are using a map data structure, the time complexity will be O(N*logN). The least complexity will be O(N) as we are using a loop to traverse the array. Point to remember for unordered_map in the worst case, the searching time increases to O(N), and hence the overall time complexity increases to O(N2). 

**Space Complexity:** O(N) as we are using a map data structure.

```cpp
int Solution::solve(vector<int> &A, int B) {
    int ans=0;
    unordered_map<int,int> mp;
    int x=0;
    mp[0] = 1;
    for(int i=0;i<A.size();i++){
        x ^= A[i];
        if(mp.find(x^B)!= mp.end()){
            ans += mp[x^B];
        }
        mp[x]++;
    }
    return ans;
}
```

OR

```java
class Solution {
    public long subarrayXor(int arr[], int k) {
        // code here
        int n = arr.length;
        HashMap<Integer,Integer> hm =new HashMap<>();
        int xor=0;
        int ans=0;
        hm.put(0,1);
        for(int i=0;i<n;i++){
            xor^=arr[i];
            ans += hm.getOrDefault(xor^k,0);
            hm.put(xor,hm.getOrDefault(xor,0)+1);
        }
        return ans;
    }
}
```