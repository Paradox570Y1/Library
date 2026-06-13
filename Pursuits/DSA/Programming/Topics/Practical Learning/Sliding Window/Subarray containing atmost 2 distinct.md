[Link](https://www.geeksforgeeks.org/problems/fruit-into-baskets-1663137462/1)
### Find length of the longest subarray containing atmost two distinct integers

Difficulty: **Medium**Accuracy: **47.98%**Submissions: **91K+**Points: **4**Average Time: **30m**

Given an array **arr[]** containing positive elements, the task is to find the length of the longest subarray of an input array containing at most two distinct integers.

**Examples:**

**Input:** arr[]= [2, 1, 2]  
**Output:** 3  
**Explanation**: The entire array [2, 1, 2] contains at most two distinct integers (2 and 1). Hence, the length of the longest subarray is 3.

**Input**: arr[] = [3, 1, 2, 2, 2, 2]  
**Output:** 5  
**Explanation**: The longest subarray containing at most two distinct integers is [1, 2, 2, 2, 2], which has a length of 5. The subarray starts at the second element 1 and ends at the last element. It contains at most two distinct integers (1 and 2).

**Constraints:**  
1 ≤ arr.size() ≤ 105  
1 ≤ arr[i] <=105


# Brute

```java
class Solution {
    public static int totalElements(Integer[] arr) {
        // code here
        int maxi=0;
        for(int i=0;i<arr.length;i++){
            HashSet<Integer> st = new HashSet<>();
            for(int j=i;j<arr.length;j++){
                st.add(arr[j]);
                if(st.size()<=2)maxi= Math.max(maxi,j-i+1);
                else break;
            }
        }
        return maxi;
    }
}
```

# Better
TC-> O(2N)
SC-> O(3)
```java
class Solution {
    public static int totalElements(Integer[] arr) {
        // code here
        int maxi=0;
        HashMap<Integer,Integer> hm = new HashMap<>();
        int j=0;
        for(int i=0;i<arr.length;i++){
            hm.put(arr[i],hm.getOrDefault(arr[i],0)+1);
            while(hm.size()>2){
                hm.put(arr[j],hm.get(arr[j])-1);
                if(hm.get(arr[j])==0)hm.remove(arr[j]);
                j++;
            }
            maxi = Math.max(maxi,i-j+1);
        }
        return maxi;
    }
}
```


# Optimal

TC-> O(N)
SC -> O(3)
```java
class Solution {
    public static int totalElements(Integer[] arr) {
        // code here
        int maxi=0;
        HashMap<Integer,Integer> hm = new HashMap<>();
        int j=0;
        for(int i=0;i<arr.length;i++){
            hm.put(arr[i],hm.getOrDefault(arr[i],0)+1);
            if(hm.size()>2){
                hm.put(arr[j],hm.get(arr[j])-1);
                if(hm.get(arr[j])==0)hm.remove(arr[j]);
                j++;
            }
            else maxi = Math.max(maxi,i-j+1);
        }
        return maxi;
    }
}
```