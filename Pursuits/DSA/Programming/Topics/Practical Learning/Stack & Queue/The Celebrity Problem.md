[Link](https://www.geeksforgeeks.org/problems/the-celebrity-problem/1)

Difficulty: **Medium**Accuracy: **38.33%**Submissions: **301K+**Points: **4**Average Time: **30m**

A celebrity is a person who is known to all but **does not know** anyone at a party. A party is being organized by some people.  A square matrix **mat** (n*n) is used to represent people at the party such that if an element of row i and column j is set to 1 it means ith person knows jth person. You need to return the index of the celebrity in the party, if the celebrity does not exist, return **-1**.

**Note:** Follow 0-based indexing.

**Examples:**

**Input:** mat[][] = [[0 1 0], [0 0 0], [0 1 0]]
**Output:** 1
**Explanation:** 0th and 2nd person both know 1. Therefore, 1 is the celebrity. 

**Input:** mat[][] = [[0 1], [1 0]]
**Output:** -1
**Explanation:** The two people at the party both know each other. None of them is a celebrity.

**Input:** mat[][] = [[0]]
**Output:** 0

**Constraints:**  
1 <= mat.size()<= 3000  
0 <= mat[i][j]<= 1


# Brute
TC-> O(N²) + O(N)
SC -> O(2N)
```java
class Solution {
    // Function to find if there is a celebrity in the party or not.
    public int celebrity(int mat[][]) {
        // code here
        int n = mat.length;
        int[] knowMe = new int[n];
        int[] iKnow = new int[n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(mat[i][j] ==1){
                    knowMe[j]++;
                    iKnow[i]++;
                }
            }
        }
        for(int i=0;i<n;i++){
            if(knowMe[i]==n-1 && iKnow[i] ==0)return i;
        }
        return -1;
    }
}
```
TC->O(N²)
SC-> O(1)
```java
class Solution {
    // Function to find if there is a celebrity in the party or not.
    public int celebrity(int mat[][]) {
        // code here
        int n = mat.length;
        boolean flag=false;
        for(int i=0;i<n;i++){
            flag=false;
            for(int  j=0;j<n;j++){
                if(mat[i][j]==1){
                    flag= true;break;
                }
            }
            if(flag)continue;
            int cnt = 0;
            for(int k=0;k<n;k++){
                if(mat[k][i]==1)cnt++;
            }
            if(cnt==n-1)return i;
        }
        return -1;
    }
}
```

# Optimal
TC-> O(N)
SC -> O(1)
```java
class Solution {
    // Function to find if there is a celebrity in the party or not.
    public int celebrity(int mat[][]) {
        // code here
        int n = mat.length;
        int top=0,bottom=n-1;
        while(top<bottom){
            if(mat[top][bottom]==1)top++;
            else if(mat[bottom][top] ==1)bottom--;
            else{
                top++;bottom--;
            }
        }
        boolean col = true;
        int cnt=0;
        for(int i=0;i<n;i++){
            if(mat[top][i]==1)col = false;
            if(mat[i][top]==1)cnt++;
        }
        if(cnt==n-1 && col)return top;
        return -1;
    }
}
```

OR

```java
class Solution {
    public int celebrity(int mat[][]) {
        // code here
        int n = mat.length;
        int i=0;
        int j=n-1;
        while(i<j){
            if(mat[i][j]==1)i++;
            else if(mat[j][i]==1)j--;
            else{
                i++;j--;
            }
        }
        for(int t=0;t<n;t++){
            if(t!=j && mat[j][t]==1)return -1;
            if(mat[t][j]!=1)return -1;
        }
        return j;
    }
}
```