[Link](https://www.geeksforgeeks.org/problems/union-of-two-sorted-arrays-1587115621/1)

Difficulty: **Medium**

Given two sorted arrays of size **n** and **m** respectively, find their union. The Union of two arrays can be defined as the **common** and **distinct** elements in the two arrays. Return the elements in **sorted** order.

**Example 1:**

**Input**: 
n = 5, arr1\[] = {1, 2, 3, 4, 5}  
m = 5, arr2 \[] = {1, 2, 3, 6, 7}
**Output**:   
1 2 3 4 5 6 7
**Explanation**:   
Distinct elements including both the arrays are: 1 2 3 4 5 6 7.

**Example 2:**

**Input**: 
n = 5, arr1\[] = {2, 2, 3, 4, 5}  
m = 5, arr2\[] = {1, 1, 2, 3, 4}
**Output**:   
1 2 3 4 5
**Explanation**:   
Distinct elements including both the arrays are: 1 2 3 4 5.

**Example 3:**

**Input**:
n = 5, arr1\[] = {1, 1, 1, 1, 1}
m = 5, arr2\[] = {2, 2, 2, 2, 2}
**Output**:   
1 2
**Explanation**:   
Distinct elements including both the arrays are: 1 2.

**Your Task:**   
You do not need to read input or print anything. Complete the function **findUnion()** that takes two arrays **arr1[]**, **arr2[],** and their size **n** and **m** as input parameters and returns a list containing the **union of the two arrays**.

**Expected Time Complexity:** O(n+m).  
**Expected Auxiliary Space:** O(n+m).

**Constraints:**  
1 <= n, m <= 105  
-109 <= arr1[i], arr2[i] <= 109
### Brute Force
```cpp
class Solution{
    public:
    //arr1,arr2 : the arrays
    // n, m: size of arrays
    //Function to return a list containing the union of the two arrays. 
    vector<int> findUnion(int arr1[], int arr2[], int n, int m)
    {
        //Your code here
        //return vector with correct order of elements
        set<int> st;
        for(int i=0;i<n;i++){
            st.insert(arr1[i]);
        }
        for(int i=0;i<m;i++){
            st.insert(arr2[i]);
        }
        vector<int> arr;
        int j=0;
        for(auto i:st){
            arr.push_back(i);
        }
        return arr;
    }
};
```

### Optimized Way (TC=> O(n+m))
```cpp
 
//User function Template for Java

//arr1,arr2 : the arrays
// n, m: size of arrays
class Solution
{
    //Function to return a list containing the union of the two arrays.
 public static ArrayList<Integer> findUnion(int arr1[], int arr2[], int n, int m)
    {
        int i=0,j=0;
        int e=0;
        ArrayList<Integer> arr = new ArrayList<>();
        if(arr1[i]>arr2[j]){
            arr.add(arr2[j]);j++;
        }
        else{
            arr.add(arr1[i]);i++;
        }
        while(j<m && i<n ){
            if(arr1[i]>arr2[j]){
                if(arr.get(e) != arr2[j])
                {arr.add(arr2[j]);
                e++;}
                j++;
            }
            else{
                if(arr.get(e)!=arr1[i]){
                    arr.add(arr1[i]);e++;
                }
                i++;
            }
            
        }
        while(i<n){
                    if(arr.get(e)!=arr1[i]){
                        arr.add(arr1[i]);e++;
                    }
                    i++;
                }
        while(j<m){
                    if(arr.get(e)!=arr2[j]){
                        arr.add(arr2[j]);e++;
                    }
                    j++;
                }
        return arr;
    }
}
```

```cpp
class Solution
{
    //Function to return a list containing the union of the two arrays.
    public static ArrayList<Integer> findUnion(int arr1[], int arr2[], int n, int m)
    {
        int i=0,j=0;
        int e=-1;
        ArrayList<Integer> arr = new ArrayList<>();
        while(j<m && i<n ){
            if(arr1[i]>arr2[j]){
                if(arr.size()==0 || arr.get(e) != arr2[j])
                {arr.add(arr2[j]);
                e++;}
                j++;
            }
            else{
                if(arr.size()==0|| arr.get(e)!=arr1[i]){
                    arr.add(arr1[i]);e++;
                }
                i++;
            }
            
        }
        while(i<n){
                    if(arr.get(e)!=arr1[i]){
                        arr.add(arr1[i]);e++;
                    }
                    i++;
                }
        while(j<m){
                    if(arr.get(e)!=arr2[j]){
                        arr.add(arr2[j]);e++;
                    }
                    j++;
                }
        return arr;
    }
}

```