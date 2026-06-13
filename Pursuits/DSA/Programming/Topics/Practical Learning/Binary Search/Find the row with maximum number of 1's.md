[Link](https://www.geeksforgeeks.org/problems/row-with-max-1s0023/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=row-with-max-1s)
You are given a 2D array consisting of only **1's** and **0's**, where each row is sorted in non-decreasing order. You need to find and return the index of the first row that has the most number of 1s. If no such row exists, return **-1**.  
**Note:** 0-based indexing is followed.

**Examples:**

**Input:** arr[][] = [[0, 1, 1, 1],  
               [0, 0, 1, 1],  
               [1, 1, 1, 1],  
               [0, 0, 0, 0]]
**Output:** 2
**Explanation:** Row 2 contains **4** 1's.

**Input:** arr[][] = [[0, 0],   
               [1, 1]]
**Output:** 1
**Explanation:** Row 1 contains **2** 1's.

**Expected Time Complexity:** O(n+m)   
**Expected Auxiliary Space:** O(1)

**Note :** Here n,m refers to the number of rows and columns respectively.

**Constraints:**  
1 ≤ number of rows, number of columns ≤ 103  
0 ≤ arr[i][j] ≤ 1

# Better
We can use any concept lower bound, upper bound, 
```java
import java.util.*;

public class tUf {
    public static int lowerBound(ArrayList<Integer> arr, int n, int x) {
        int low = 0, high = n - 1;
        int ans = n;

        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr.get(mid) >= x) {
                ans = mid;
                // look for smaller index on the left
                high = mid - 1;
            } else {
                low = mid + 1; // look on the right
            }
        }
        return ans;
    }
    public static int rowWithMax1s(ArrayList<ArrayList<Integer>> matrix, int n, int m) {
        int cnt_max = 0;
        int index = -1;

        // traverse the rows:
        for (int i = 0; i < n; i++) {
            // get the number of 1's:
            int cnt_ones = m - lowerBound(matrix.get(i), m, 1);
            if (cnt_ones > cnt_max) {
                cnt_max = cnt_ones;
                index = i;
            }
        }
        return index;
    }
}
```
# Optimal
my approach
```java
class Solution {
    public int rowWithMax1s(int arr[][]) {
        // code here
        int row = arr.length;
        int col = arr[0].length;
        int cnt=-1;
        int p=col-1;
        if(p<0)return -1;
        for(int i=0;i<row;i++){
            while(arr[i][p]==1){
                p--;
                cnt = i;
                if(p<0)return i;
            }
        }
        return cnt;
    }
}
```

```cpp
class Solution {
  public:
    int rowWithMax1s(vector<vector<int> > &arr) {
        // code here
        int index=arr[0].size()-1,ans=-1;
        for(int i=0;i<arr.size();i++){
            while(index>=0 && arr[i][index]==1){
                index--;ans=i;
            }
        }
        return ans;
    }
};
```