### Perfect Sum Problem
[Link](https://www.geeksforgeeks.org/problems/perfect-sum-problem5633/1)
Difficulty: **Medium**Accuracy: **20.58%**Submissions: **445K+**Points: **4**

Given an array **`arr`** of non-negative integers and an integer **`target`**, the task is to count all subsets of the array whose sum is equal to the given `target`.

**Examples:**

**Input**: arr[] = [5, 2, 3, 10, 6, 8], target = 10
**Output:** 3
**Explanation**: The subsets {5, 2, 3}, {2, 8}, and {10} sum up to the target 10.

**Input**: arr[] = [2, 5, 1, 4, 3], target = 10
**Output:** 3
**Explanation**: The subsets {2, 1, 4, 3}, {5, 1, 4}, and {2, 5, 3} sum up to the target 10.

**Input**: arr[] = [5, 7, 8], target = 3  
**Output:** 0
**Explanation**: There are no subsets of the array that sum up to the target 3.

**Input**: arr[] = [35, 2, 8, 22], target = 0  
**Output:** 1
**Explanation**: The empty subset is the only subset with a sum of 0.

**Constraints:**  
1 ≤ arr.size() ≤ 103  
0 ≤ arr[i] ≤ 103  
0 ≤ target ≤ 103

#### To count the no. of subsequence

#Explaination
---
![[Pasted image 20250103120801.png|400]]

```java
import java.util.Scanner;
class p1{
    static int printAllSub(int[] arr,int idx,int sum,int target){
        if(idx== arr.length){
            if(sum==target){
                return 1;
            }
            return 0;
        }
        //not pick
        int a = printAllSub(arr,idx+1,sum,target);
        //pick
        int b = printAllSub(arr,idx+1,sum+arr[idx],target);
        return a+b;
    }
    public static void main(String[] args) {
        int n;
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        int arr[]  = new int[n];
        for(int i=0;i<n;i++){
            arr[i] = sc.nextInt();
        }
        System.out.println(printAllSub(arr,0,0,2));
    }
}
```
![[Pasted image 20250103123621.png|400]]
---
---
# Code

```java
class Solution {
    // Function to calculate the number of subsets with a given sum
    int cntSum(int[] nums,int target,int i,int sum){
        if(nums.length == i){
            if(target == sum)return 1;
            return 0;
        }
        int a = cntSum(nums,target,i+1,sum);
        int b = cntSum(nums,target,i+1,sum+nums[i]);
        return a+b;
    }
    public int perfectSum(int[] nums, int target) {
        // code here
        return cntSum(nums,target,0,0);
    }
}
```

```java
class Solution {
    // Function to calculate the number of subsets with a given sum
    private int cnt=0;
    void cntSum(int[] nums,int target,int i,int sum){
        if(nums.length == i){
            if(target == sum)cnt++;
            return;
        }
        cntSum(nums,target,i+1,sum);
        cntSum(nums,target,i+1,sum+nums[i]);
    }
    public int perfectSum(int[] nums, int target) {
        // code here
        cntSum(nums,target,0,0);
        return cnt;
    }
}
```


##### To print the array with given sum instead of count

```java
import java.util.Scanner;
import java.util.List;
import java.util.ArrayList;
class p1{
    static void printAllSub(int[] arr,int idx,List<Integer> li,int sum,int target){
        if(idx== arr.length){
            if(sum==target){
                for (int i = 0; i < li.size(); i++)
                    System.out.print(li.get(i));
                System.out.println();
            }
            return;
        }
        //not pick
        printAllSub(arr,idx+1,li,sum,target);
        //pick
        li.add(arr[idx]);
        printAllSub(arr,idx+1,li,sum+arr[idx],target);
        li.remove(li.size()-1);
    }
    public static void main(String[] args) {
        int n;
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        int arr[]  = new int[n];
        for(int i=0;i<n;i++){
            arr[i] = sc.nextInt();
        }
        printAllSub(arr,0,new ArrayList<>(),0,2);
    }
}
```

#### To print only 1 subsequence with given sum

- Basically if we get that subsequence where sum equals to target then stop the recursion

```java
import java.util.Scanner;
import java.util.List;
import java.util.ArrayList;
class p1{
    static boolean printAllSub(int[] arr,int idx,List<Integer> li,int sum,int target){
        if(idx== arr.length){
        //If condition satisfied return true
            if(sum==target){
                for (int i = 0; i < li.size(); i++)System.out.print(li.get(i));
                System.out.println();
                return true;
            }
            //condition not satisfied
            return false;
        }
        //not pick
        if(printAllSub(arr,idx+1,li,sum,target)==true)return true;
        //pick
        li.add(arr[idx]);
        if(printAllSub(arr,idx+1,li,sum+arr[idx],target)==true)return true;
        li.remove(li.size()-1);
        return false;
    }
    public static void main(String[] args) {
        int n;
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        int arr[]  = new int[n];
        for(int i=0;i<n;i++){
            arr[i] = sc.nextInt();
        }
        printAllSub(arr,0,new ArrayList<>(),0,2);
    }
}
```

# Optimal

```java
class Solution {
    // Function to calculate the number of subsets with a given sum
    public int perfectSum(int[] nums, int target) {
        // code here
        int n = nums.length;
        int dp[]  = new int[target+1];
        dp[0] = 1;
        for(int i=0;i<n;i++){
            int ele = nums[i];
            for(int j=target;j>=ele;j--){
                dp[j]+=dp[j-ele];
            }
        }
        return dp[target];
    }
}
```