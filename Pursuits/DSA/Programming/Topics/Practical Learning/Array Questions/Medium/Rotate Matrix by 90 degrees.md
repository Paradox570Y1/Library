[48. Rotate Image](https://leetcode.com/problems/rotate-image/)

You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)

**Input:** matrix = `[[1,2,3],[4,5,6],[7,8,9]]`
**Output:** `[[7,4,1],[8,5,2],[9,6,3]]`

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)

**Input:** matrix = `[[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]`
**Output:** `[[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]`

**Constraints:**

- `n == matrix.length == matrix[i].length`
- `1 <= n <= 20`
- `-1000 <= matrix[i][j] <= 1000`

# Brute Force
**Time Complexity:** O(N) to linearly iterate and put it into some other matrix.

**Space Complexity:** O(N) to copy it into some other matrix.
```java
import java.util.*;
class TUF {
    static int[][] rotate(int[][] matrix) {
        int n = matrix.length;
        int rotated[][] = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                rotated[j][n - i - 1] = matrix[i][j];
            }
        }
        return rotated;
    }

    public static void main(String args[]) {
        int arr[][] =  {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
        int rotated[][] = rotate(arr);
        System.out.println("Rotated Image");
        for (int i = 0; i < rotated.length; i++) {
            for (int j = 0; j < rotated.length; j++) {
                System.out.print(rotated[i][j] + " ");
            }
            System.out.println();
        }

    }
}


```


- With Space complexity O(1)
```java
class Solution {
    public void rotate(int[][] matrix) {
        int drop,store,i,init_j;
        int n = matrix.length;
        int d=0;
        if(n-3<0)d=1;
        for(int a=0;a<=n-3+d;a++){
            for(int j=a;j<=n-2-a;j++){
                i=a;
                store= matrix[i][j];
                init_j=j;
                do{
                    drop = store;
                    if(i==a){
                        i=j;
                        j=n-1-a;
                    }
                    else if(j==n-1-a){
                        j=n-1-i;
                        i=n-1-a;
                    }
                    else if(i==n-1-a){
                        i=j;
                        j=a;
                    }
                    else if(j==a){
                        j=n-1-i;
                        i=a;
                    }
                    store = matrix[i][j];
                    matrix[i][j] = drop;
                }
                while(j!=init_j || i!=a);
            
            }
        }
    }
}
```


# Best Approach
**Time Complexity:** O(N) + O(N).One O(N) is for transposing the matrix and the other is for reversing the matrix.

**Space Complexity:** O(1).
```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                int temp = matrix[j][i];
                matrix[j][i]= matrix[i][j];
                matrix[i][j] = temp;
            }
        }
        int j=0,k=n-1;
        for(int i=0;i<n;i++){
            j=0;k=n-1;
            while(j<k){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][k];
                matrix[i][k] = temp;
                j++;k--;
            }
        }
    }
}
```