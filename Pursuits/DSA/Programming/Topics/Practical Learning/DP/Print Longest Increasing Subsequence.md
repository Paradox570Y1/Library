[Print Longest Increasing Subsequence](https://www.geeksforgeeks.org/problems/printing-longest-increasing-subsequence/1)

Difficulty: **Medium**Accuracy: **51.81%**Submissions: **51K+**Points: **4**Average Time: **20m**

You are given an array of integers **arr[]**, return the **Longest Increasing Subsequence (LIS)** of the given array.  
**LIS** is the longest subsequence where each element is **strictly** greater than the previous one.  
**Note:** If multiple **LIS** of the same maximum length exist, return the one that appears **first** based on the **lexicographical order** of their **indices** (i.e., the earliest combination of positions from the original sequence).

**Examples:**

**Input:** arr[] = [10, 20, 3, 40]
**Output:** [10, 20, 40]
**Explanation:** [10, 20, 40] is the longest subsequence where each number is greater than the previous one, maintaining the original order.

**Input:** arr[] = [10, 22, 9, 33, 21, 50, 41, 60, 80]
**Output:** [10, 22, 33, 50, 60, 80]  
**Explanation:** There are multiple longest Increasing subsequence of length 6, that is [10, 22, 33, 50, 60, 80] and [10 22 33 41 60 80]. The first one has lexicographic smallest order of indices.

**Constraint:**  
1 ≤ n ≤ 5*103  
0 ≤ arr[i] ≤ 109


# Brute

```java
class Solution {
    ArrayList<Integer> res;
    private void helper(int[] arr, ArrayList<Integer> list, int i) {
        if (i == arr.length) {
            if (res.size() < list.size()) {
                res = new ArrayList<>(list);
            }
            return;
        }
        
        if ( list.size() == 0 || list.get(list.size()-1) < arr[i]) {
            list.add(arr[i]);
            helper(arr, list, i+1);
            list.remove(list.size()-1);
        }
        helper(arr, list, i+1);
    }
    public ArrayList<Integer> getLIS(int arr[]) {
        // Code here
        res = new ArrayList<>();
        helper(arr, new ArrayList<>(), 0);
        return res;
    }
}

```


# Optimal 

```java
class Solution {
    public ArrayList<Integer> getLIS(int arr[]) {
        // Code here
        int n = arr.length;
        int[] dp = new int[n];
        int[] parent = new int[n];
        
        int idx = 0;
        int maxLen = 0;
        for (int i = 0; i < n; i++) {
            parent[i] = i;
            for (int j = 0; j < i; j++) {
                if (arr[i] > arr[j]) {
                    if (dp[i] < dp[j]+1) {
                        dp[i] = dp[j] + 1;
                        parent[i] = j;
                    }
                }
            }
            if (maxLen < dp[i]) {
                maxLen = dp[i];
                idx = i;
            }
        }
        
        ArrayList<Integer> res = new ArrayList<>();
        while (parent[idx] != idx) {
            res.add(arr[idx]);
            idx = parent[idx];
        }
        res.add(arr[idx]);
        rev(res);
        return res;
    }
    private void rev(ArrayList<Integer> list) {
        int i = 0, j = list.size() -1;
        while (i < j) {
            int temp = list.get(i);
            list.set(i, list.get(j));
            list.set(j, temp);
            i++;j--;
        }
    }
}

```