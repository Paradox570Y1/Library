[75. Sort Colors](https://leetcode.com/problems/sort-colors/)

Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

**Example 1:**

**Input:** nums = [2,0,2,1,1,0]
**Output:** [0,0,1,1,2,2]

**Example 2:**

**Input:** nums = [2,0,1]
**Output:** [0,1,2]

**Constraints:**

- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` is either `0`, `1`, or `2`.

## Brute Force
-  Perform any type of sorting.
- In case you perform merge sort TC=>O(n logn) SC=>O(n)

## Better Approach
- TC=>O(2N) SC=>O(1)
```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int hash[3]={0};
        for(int i=0;i<nums.size();i++){
            hash[nums[i]]++;
        }
        for(int i=0;i<hash[0];i++){
            nums[i] = 0;
        }
        for(int i=hash[0];i<hash[0]+hash[1];i++){
            nums[i] = 1;
        }
        for(int i=hash[0]+hash[1];i<nums.size();i++){
            nums[i] = 2;
        }
    }
};
```
OR

```java
class Solution {
    public void sortColors(int[] nums) {
        int hash[] = new int[3];
        for(int n:nums){
            hash[n]++;
        }
        int k=0;
        for(int i=0;i<3;i++){
            for(int j=0;j<hash[i];j++){
                nums[k] = i;
                k++;
            }
        }
    }
	}
```
# Dutch National Flag Algorithm
![[Pasted image 20240716120535.png]]

## Optimal Approach
```java
import java.util.*;

public class Main {
    public static void sortArray(ArrayList<Integer> arr, int n) {
        int low = 0, mid = 0, high = n - 1; // 3 pointers

        while (mid <= high) {
            if (arr.get(mid) == 0) {
                // swapping arr[low] and arr[mid]
                int temp = arr.get(low);
                arr.set(low, arr.get(mid));
                arr.set(mid, temp);

                low++;
                mid++;

            } else if (arr.get(mid) == 1) {
                mid++;

            } else {
                // swapping arr[mid] and arr[high]
                int temp = arr.get(mid);
                arr.set(mid, arr.get(high));
                arr.set(high, temp);

                high--;
            }
        }
    }

    public static void main(String args[]) {
        int n = 6;
        ArrayList<Integer> arr = new ArrayList<>(Arrays.asList(new Integer[] {0, 2, 1, 2, 0, 1}));
        sortArray(arr, n);
        System.out.println("After sorting:");
        for (int i = 0; i < n; i++) {
            System.out.print(arr.get(i) + " ");
        }
        System.out.println();

    }

}

```

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n = nums.size();
        int mid=0,low=0,high=n-1;
        while(mid<=high){
            if(nums[mid]==2){
                swap(nums[mid],nums[high]);
                high--;
            }
            else if(nums[mid]==1){
                mid++;
            }
            else if(nums[mid]==0){
                swap(nums[mid],nums[low]);
                low++;mid++;
            }
        }
    }
};
```

OR

```java
class Solution {
    private void swap(int[] arr,int i,int j){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    public void sortColors(int[] nums) {
        int n = nums.length;
        int low=0;
        int high=n-1;
        for(int i=0;i<=high;){
            int cur = nums[i];
            if(cur == 0){
                swap(nums,low,i);
                low++;
                i++;
            }
            else if(cur==2){
                swap(nums,high,i);
                high--;
            }
            else i++;
        }
    }
}
```