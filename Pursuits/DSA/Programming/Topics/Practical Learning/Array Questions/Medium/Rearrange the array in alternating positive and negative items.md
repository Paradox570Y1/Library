[2149. Rearrange Array Elements by Sign](https://leetcode.com/problems/rearrange-array-elements-by-sign/)
You are given a **0-indexed** integer array `nums` of **even** length consisting of an **equal** number of positive and negative integers.

You should return the array of nums such that the the array follows the given conditions:

1. Every **consecutive pair** of integers have **opposite signs**.
2. For all integers with the same sign, the **order** in which they were present in `nums` is **preserved**.
3. The rearranged array begins with a positive integer.

Return _the modified array after rearranging the elements to satisfy the aforementioned conditions_.

**Example 1:**

**Input:** nums = [3,1,-2,-5,2,-4]
**Output:** [3,-2,1,-5,2,-4]
**Explanation:**
The positive integers in nums are [3,1,2]. The negative integers are [-2,-5,-4].
The only possible way to rearrange them such that they satisfy all conditions is [3,-2,1,-5,2,-4].
Other ways such as [1,-2,2,-5,3,-4], [3,1,2,-2,-5,-4], [-2,3,-5,1,-4,2] are incorrect because they do not satisfy one or more conditions.  

**Example 2:**

**Input:** nums = [-1,1]
**Output:** [1,-1]
**Explanation:**
1 is the only positive integer and -1 the only negative integer in nums.
So nums is rearranged to [1,-1].

**Constraints:**

- `2 <= nums.length <= 2 * 105`
- `nums.length` is **even**
- `1 <= |nums[i]| <= 105`
- `nums` consists of **equal** number of positive and negative integers.
## Brute Force
```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n = nums.length;
        int p[] = new int[n/2];
        int nn[] = new int[n/2];
        int in_p =0,in_n=0;
        for(int i=0;i<n;i++){
            if(nums[i]>0){
                p[in_p++] = nums[i];
            }
            else{
                nn[in_n++] = nums[i];
            }
        }
        int ans[]= new int[n];
        int k=0;
        for(int i=0;i<n/2;i++){
            ans[k++] = p[i];
            ans[k++] = nn[i];
        }
        return ans;
    }
}
```

```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n = nums.length;
        int p[] = new int[n/2];
        int nn[] = new int[n/2];
        int in_p =0,in_n=0;
        for(int i=0;i<n;i++){
            if(nums[i]>0){
                p[in_p++] = nums[i];
            }
            else{
                nn[in_n++] = nums[i];
            }
        }
        for(int i=0;i<n/2;i++){
            nums[2*i] = p[i];
            nums[2*i+1]= nn[i];
        }
        return nums;
    }
}
```


## Optimal Approach(by very slight margins)
```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n = nums.length;
        int ans[] = new int[n];
        int P=0,N=1;
        for(int i=0;i<n;i++){
            if(nums[i]>0){
                ans[P]=nums[i];
                P+=2;
            }
            else{
                ans[N]=nums[i];
                N+=2;
            }
        }
        return ans;
    }
}
```
**Time Complexity:** O(N) { O(N) for traversing the array once and substituting positives and negatives simultaneously using pointers, where N = size of the array A}.

**Space Complexity:**  O(N) { Extra Space used to store the rearranged elements separately in an array, where N = size of array A}.
# Variety 2
In this number of positive and no. of negative numbers are not equal.

```java
import java.util.*;

public class Main {
    public static ArrayList<Integer> RearrangebySign(ArrayList<Integer> A, int n) {
        // Define 2 ArrayLists, one for storing positive 
        // and other for negative elements of the array.
        ArrayList<Integer> pos = new ArrayList<>();
        ArrayList<Integer> neg = new ArrayList<>();

        // Segregate the array into positives and negatives.
        for (int i = 0; i < n; i++) {
            if (A.get(i) > 0)
                pos.add(A.get(i));
            else
                neg.add(A.get(i));
        }

        // If positives are lesser than the negatives.
        if (pos.size() < neg.size()) {

            // First, fill array alternatively till the point 
            // where positives and negatives are equal in number.
            for (int i = 0; i < pos.size(); i++) {
                A.set(2 * i, pos.get(i));
                A.set(2 * i + 1, neg.get(i));
            }

            // Fill the remaining negatives at the end of the array.
            int index = pos.size() * 2;
            for (int i = pos.size(); i < neg.size(); i++) {
                A.set(index, neg.get(i));
                index++;
            }
        }

        // If negatives are lesser than the positives.
        else {
            // First, fill array alternatively till the point 
            // where positives and negatives are equal in number.
            for (int i = 0; i < neg.size(); i++) {
                A.set(2 * i, pos.get(i));
                A.set(2 * i + 1, neg.get(i));
            }

            // Fill the remaining positives at the end of the array.
            int index = neg.size() * 2;
            for (int i = neg.size(); i < pos.size(); i++) {
                A.set(index, pos.get(i));
                index++;
            }
        }
        return A;
    }
}
```
