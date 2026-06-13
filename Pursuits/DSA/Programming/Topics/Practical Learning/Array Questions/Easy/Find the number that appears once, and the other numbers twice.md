**Problem Statement:** Given a non-empty array of integers **arr**, every element appears twice except for one. Find that single one.

**Example 1:Input Format: arr[] = {2,2,1}
**Result:** 1
**Explanation:** In this array, only the element 1 appear once and so it is the answer.

**Example 2:****Input Format:** arr[] = {4,1,2,1,2}
**Result:** 4
**Explanation:** In this array, only element 4 appear once and the other elements appear twice. So, 4 is the answer.
## Brute Force
```java



import java.util.*;

public class tUf {
    public static int getSingleElement(int []arr) {
        // Size of the array:
        int n = arr.length;

        //Run a loop for selecting elements:
        for (int i = 0; i < n; i++) {
            int num = arr[i]; // selected element
            int cnt = 0;

            //find the occurrence using linear search:
            for (int j = 0; j < n; j++) {
                if (arr[j] == num)
                    cnt++;
            }

            // if the occurrence is 1 return ans:
            if (cnt == 1) return num;
        }

        //This line will never execute
        //if the array contains a single element.
        return -1;
    }

    public static void main(String args[]) {
        int[] arr = {4, 1, 2, 1, 2};
        int ans = getSingleElement(arr);
        System.out.println("The single element is: " + ans);

    }
}
```

**Time Complexity:** O(N²), where N = size of the given array.  
**Reason:** For every element, we are performing a linear search to count its occurrence. The linear search takes O(N) time complexity. And there are N elements in the array. So, the total time complexity will be O(N2).

**Space Complexity:** O(1) as we are not using any extra space.

## Better Approach 1 (Using Hashing):
```java
import java.util.*;

public class tUf {
    public static int getSingleElement(int []arr) {
        //size of the array:
        int n = arr.length;

        // Find the maximum element:
        int maxi = arr[0];
        for (int i = 0; i < n; i++) {
            maxi = Math.max(maxi, arr[i]);
        }

        // Declare hash array of size maxi+1
        // And hash the given array:
        int[] hash = new int[maxi + 1];
        for (int i = 0; i < n; i++) {
            hash[arr[i]]++;
        }

        //Find the single element and return the answer:
        for (int i = 0; i < n; i++) {
            if (hash[arr[i]] == 1)
                return arr[i];
        }

        //This line will never execute
        //if the array contains a single element.
        return -1;
    }

    public static void main(String args[]) {
        int[] arr = {4, 1, 2, 1, 2};
        int ans = getSingleElement(arr);
        System.out.println("The single element is: " + ans);

    }
}
```
**Time Complexity:** O(N)+O(N)+O(N), where N = size of the array  
**Reason:** One O(N) is for finding the maximum, the second one is to hash the elements and the third one is to search the single element in the array.

**Space Complexity:** O(maxElement+1) where maxElement = the maximum element of the array.

**Note:** While searching for the answer finally, we can either use a loop from 0 to n(i.e. Size of the array) or use a loop from 0 to maxElement. So, the time complexity will change accordingly.

Now, using array hashing it is difficult to hash the elements of the array if it contains negative numbers or a very large number. So to avoid these problems, we will be using the map data structure to hash the array elements.

## Better Approach 2 (Using map data structure)
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        map<int,int> mp;
        for(int i=0;i<nums.size();i++){
            mp[nums[i]]++;
        }
        for(auto i:mp){
            if(i.second==1) return i.first;
        }
        return -1;
    }
};
```

![[Pasted image 20240712134718.png|200]]

**Time Complexity:** O(N*logM) + O(M), where M = size of the map i.e. M = (N/2)+1. N = size of the array.  
**Reason:** We are inserting N elements in the map data structure and insertion takes logM time(where M = size of the map). So this results in the first term O(N*logM). The second term is to iterate the map and search the single element. In Java, HashMap generally takes O(1) time complexity for insertion and search. In that case, the time complexity will be O(N) + O(M).

**Note:** The time complexity will be changed depending on which map data structure we are using. If we use unordered_map in C++, the time complexity will be O(N) for the best and average case instead of O(N*logM). But in the worst case(which rarely happens), it will be nearly O(N2).

**Space Complexity:** O(M) as we are using a map data structure. Here M = size of the map i.e. M = (N/2)+1.


## Optimized Approach
```java
class Solution {
public int singleNumber(int[] nums) {
        int n=0;
        for(int i=0;i<nums.length;i++){
            n=n^nums[i];
        }
        return n;
    }
}
```
**Time Complexity:** O(N), where N = size of the array.  
**Reason:** We are iterating the array only once.

**Space Complexity:** O(1) as we are not using any extra space.