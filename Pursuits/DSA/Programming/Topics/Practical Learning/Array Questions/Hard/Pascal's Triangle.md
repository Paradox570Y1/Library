[118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)
Given an integer `numRows`, return the first numRows of **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

**Example 1:**

**Input:** numRows = 5
**Output:** [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

**Example 2:**

**Input:** numRows = 1
**Output:** [[1]]

**Constraints:**

- `1 <= numRows <= 30`

# Types of problem
1. To find particular number in pascal's triangle where row = r and column = c.
2. To print Nth row of Pascal's triangle.
3. To print Pascal triangle up to Nth place.

### To find particular no. where r & c are given
Formula:
![[Pasted image 20240803184745.png|100]]

![[Pasted image 20240803184722.png|200]]
- In such problem take data type as  `long long` to prevent Overflow.
#### Optimal
```cpp
#include <bits/stdc++.h>
using namespace std;

int nCr(int n, int r) {
    long long res = 1;

    // calculating nCr:
    for (int i = 0; i < r; i++) {
        res *= (n - i);
        res /= (i + 1);
    }
    return res;
}

int pascalTriangle(int r, int c) {
    int element = nCr(r - 1, c - 1);
    return element;
}

int main()
{
    int r = 5; // row number
    int c = 3; // col number
    int element = pascalTriangle(r, c);
    cout << "The element at position (r,c) is: "
            << element << "n";
    return 0;
} 
```
### To print Nth row of Pascal Triangle
#### Brute Force
```java
import java.util.*;
public class main{
    public static void main(String[]args){
        int row=31;
        int n = row-1;
        long ans=1;
        for(int r=0;r<row;r++){
            ans=1;
            for (int j = 0; j < r; j++) {
                ans *= n - j;
                ans /= j + 1;
            }
            System.out.print(ans+" ");
        }
        
    }
}
```

```java

import java.util.*;

public class Main {

    public static long nCr(int n, int r) {
        long res = 1;

        // calculating nCr:
        for (int i = 0; i < r; i++) {
            res = res * (n - i);
            res = res / (i + 1);
        }
        return res;
    }

    public static void pascalTriangle(int n) {
        // printing the entire row n:
        for (int c = 1; c <= n; c++) {
            System.out.print(nCr(n - 1, c - 1) + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int n = 5;
        pascalTriangle(n);
    }
}
    
```
#### Optimal
```java
//row is 1->n  col is taken 0->n
import java.util.*;
public class main{
    public static void main(String[]args){
        int row = 5;
        long ans=1;
        System.out.print(ans+" ");
        for(int col=1;col<row;col++){
            ans*= (row-col);
            ans /= col;
            System.out.print(ans+" ");
        }
    }
}
```


### To print Pascal Triangle up to Nth Place.
#### Brute
```cpp

#include <bits/stdc++.h>
using namespace std;

int nCr(int n, int r) {
    long long res = 1;

    // calculating nCr:
    for (int i = 0; i < r; i++) {
        res = res * (n - i);
        res = res / (i + 1);
    }
    return (int)(res);
}

vector<vector<int>> pascalTriangle(int n) {
    vector<vector<int>> ans;

    //Store the entire pascal's triangle:
    for (int row = 1; row <= n; row++) {
        vector<int> tempLst; // temporary list
        for (int col = 1; col <= row; col++) {
            tempLst.push_back(nCr(row - 1, col - 1));
        }
        ans.push_back(tempLst);
    }
    return ans;
}

int main()
{
    int n = 5;
    vector<vector<int>> ans = pascalTriangle(n);
    for (auto it : ans) {
        for (auto ele : it) {
            cout << ele << " ";
        }
        cout << "n";
    }
    return 0;
}

```
#### Better
```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(Arrays.asList(1));
        if(numRows==1)return ans;
        ans.add(Arrays.asList(1,1));
        if(numRows==2)return ans;
        for(int i=2;i<numRows;i++){
            int p=1;
            List<Integer> li = new ArrayList<>();
            li.add(1);
            while(p<i){
                List<Integer> last = ans.get(i-1);
                li.add(last.get(p-1)+last.get(p));
                p++;
            }
            li.add(1);
            ans.add(li);
        }
        return ans;
    }
}
```

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> li = new ArrayList<>();
        if(numRows==1){
            li.add(new ArrayList<>(List.of(1)));
        }
        else{
            li.add(new ArrayList<>(List.of(1)));
            li.add(new ArrayList<>(List.of(1,1)));
        }

        for(int i=2;i<numRows;i++){
            List<Integer> row = new ArrayList<>();
            row.add(li.get(i-1).get(0));
            for(int j=0;j<i-1;j++){
                row.add(li.get(i-1).get(j)+li.get(i-1).get(j+1));
            }
            row.add(li.get(i-1).get(i-1));
            li.add(new ArrayList<>(row));
        }
        return li;
    }
}
```
#### Optimal
```cpp
class Solution {
public:
    vector<int> generate_row(int row){
        vector<int> curr_row;
        long long ans = 1;
        curr_row.push_back(ans);
        for(int col=1;col<row;col++){
            ans *= row-col;
            ans /= col;
            curr_row.push_back(ans);
        }
        return curr_row;
    }
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> ans;
        vector<int> rows;
        for(int row=1;row<=numRows;row++){
            ans.push_back(generate_row(row));
        }
        return ans;
    }
};
```
OR

```java
class Solution {
    
    public List<List<Integer>> generate(int n) {
        List<List<Integer>> ans= new ArrayList<>();
        for(int i=0;i<n;i++){
            List<Integer> li = new ArrayList<>(List.of(1));
            int val=1;
            for(int j=1;j<=i;j++){
                val*=(i-j+1);
                val/=j;
                li.add(val);
            }
            ans.add(li);
        }
        return ans;
    }
}
```

# DP approach
```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> li = new ArrayList<>();
        for(int i=0;i<numRows;i++){
            List<Integer> temp=new ArrayList<>(Arrays.asList(1));
            for(int j=1;j<i+1;j++){
                temp.add(temp.get(j-1)*(i-j+1)/j);
            }
            li.add(temp);
        }
        return li;
    }
}
```

OR
Most Optimized
```java
class Solution {
    public List<List<Integer>> generate(int n) {
        List<List<Integer>> ans  = new ArrayList<>();
        for(int i=0;i<n;i++){
            List<Integer> li = new ArrayList<>();
            int val=1;
            for(int j=0;j<=i;j++){
                li.add(val);
                val = val*(i-j)/(j+1);
            }
            ans.add(li);
        }
        return ans;
    }
}
```