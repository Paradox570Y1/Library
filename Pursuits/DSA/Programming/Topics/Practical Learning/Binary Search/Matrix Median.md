
Difficulty: **Hard**Accuracy: **55.05%**Submissions: **119K+**Points: **8**

Given a row wise sorted matrix of size **R*C** where R and C are always **odd**, find the median of the matrix.

**Example 1:**

**Input**:
R = 3, C = 3
M = [[1, 3, 5], 
     [2, 6, 9], 
     [3, 6, 9]]
**Output:** 5
**Explanation**: Sorting matrix elements gives 
us {1,2,3,3,5,6,6,9,9}. Hence, 5 is median. 

**Example 2:**

**Input:**
R = 3, C = 1
M = [[1], [2], [3]]
**Output:** 2
**Explanation**: Sorting matrix elements gives 
us {1,2,3}. Hence, 2 is median.

  
**Your Task:**    
You don't need to read input or print anything. Your task is to complete the function **median()** which takes the integers **R** and **C** along with the 2D **matrix** as input parameters and returns the **median** of the matrix.  
  
**Expected Time Complexity:** O(32 * R * log(C))  
**Expected Auxiliary Space:** O(1)

  
**Constraints:**  
1 <= R, C <= 400  
1 <= matrix\[i]\[j] <= 2000

# Brute
**Time Complexity:** O(MXN) + O(MXN(log(MXN))), where M = number of row in the given matrix, N = number of columns in the given matrix

**Reason:** At first, we are traversing the matrix to copy the elements. This takes O(MXN) time complexity. Then we are sorting the linear array of size (MXN), that takes O(MXN(log(MXN))) time complexity

**Space Complexity:** O(MXN) as we are using a temporary list to store the elements of the matrix.
```java                            
import java.util.*;

public class tUf {
    public static int median(int matrix[][], int m, int n) {
        List<Integer> lst = new ArrayList<>();

        // Traverse the matrix and
        // copy the elements to the list:
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                lst.add(matrix[i][j]);
            }
        }

        // Sort the list:
        Collections.sort(lst);
        return lst.get((m * n) / 2);
    }
}
```

# Optimal
**Time Complexity:** O(log(109)) X O(M(logN)), where M = number of rows in the given matrix, N = number of columns in the given matrix

**Reason:** Our search space lies between [0, 109] as the min(matrix) can be 0 and the max(matrix) can be 109. We are applying binary search in this search space and it takes O(log(109)) time complexity. Then we call countSmallEqual() function for every ‘mid’ and this function takes O(M(logN)) time complexity.

**Space Complexity :** O(1) as we are not using any extra space
```cpp
class Solution{   
public:
    int upperbound(vector<int> &arr,int limit){
        int low=0,high = arr.size()-1,ans=arr.size();
        while(low<=high){
            int mid = (low+high)/2;
            if(arr[mid]>limit){
                ans = mid;
                high=mid-1;
            }
            else low = mid+1;
        }
        return ans;
    }
    int leftHalf(vector<vector<int>> &matrix,int limit){
        int cnt=0;
        for(int i=0;i<matrix.size();i++){
            cnt += upperbound(matrix[i],limit);
        }
        return cnt;
    }
    int median(vector<vector<int>> &matrix, int R, int C){
        // code here 
        int n=matrix[0].size(),m = matrix.size();
        int low = INT_MAX, high = INT_MIN;
        for(int i=0;i<m;i++){
            low = min(low,matrix[i][0]);
            high = max(high,matrix[i][n-1]);
        }
        while(low<=high){
            int mid = (low+high)>>1;
            int left = leftHalf(matrix,mid);
            if(left>n*m/2)high =mid-1;
            else low = mid+1;
        }
        return low;
    }
};
```



OR 

```java
// User function Template for Java

class Solution {
    private int ub(int[] arr,int limit){
        int low=0,high = arr.length-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(arr[mid]>limit)high=mid-1;
            else low = mid+1;
        }
        return low;
    }
    private int leftHalf(int[][] arr,int limit){
        int cnt=0;
        for(int[] row:arr){
            cnt+=ub(row,limit);
        }
        return cnt;
    }
    int median(int mat[][]) {
        // code here
        int low = Integer.MAX_VALUE;
        int high = Integer.MIN_VALUE;
        int n= mat.length;
        int m = mat[0].length;
        for(int[] ele:mat){
            low = Math.min(low,ele[0]);
            high = Math.max(high,ele[m-1]);
        }
        while(low<=high){
            int mid= low + (high-low)/2;
            if(leftHalf(mat,mid)>m*n/2)high = mid-1;
            else low = mid+1;
        }
        return high+1;
    }
}
```