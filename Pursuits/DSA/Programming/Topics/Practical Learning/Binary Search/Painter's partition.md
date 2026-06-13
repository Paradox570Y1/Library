
Given an array/list of length _**‘n’**_, where the array/list represents the boards and each element of the given array/list represents the length of each board. Some _**‘k’**_ numbers of painters are available to paint these boards. Consider that each unit of a board takes 1 unit of time to paint.

You are supposed to return the area of the minimum time to get this job done of painting all the ‘n’ boards under a constraint that any painter will only paint the continuous sections of boards.


**Example :**

```
Input: arr = [2, 1, 5, 6, 2, 3], k = 2

Output: 11

Explanation:
First painter can paint boards 1 to 3 in 8 units of time and the second painter can paint boards 4-6 in 11 units of time. Thus both painters will paint all the boards in max(8,11) = 11 units of time. It can be shown that all the boards can't be painted in less than 11 units of time.
```


# Brute
**Time Complexity:** O(N * (sum(arr[])-max(arr[])+1)), where N = size of the array, sum(arr[]) = sum of all array elements, max(arr[]) = maximum of all array elements.  
**Reason:** We are using a loop from max(arr[]) to sum(arr[]) to check all possible values of time. Inside the loop, we are calling the countPainters() function for each number. Now, inside the countPainters() function, we are using a loop that runs for N times.

**Space Complexity:**  O(1) as we are not using any extra space to solve this problem.

```cpp
#include <bits/stdc++.h>
using namespace std;

int countPainters(vector<int> &boards, int time) {
    int n = boards.size(); //size of array.
    int painters = 1;
    long long boardsPainter = 0;
    for (int i = 0; i < n; i++) {
        if (boardsPainter + boards[i] <= time) {
            //allocate board to current painter
            boardsPainter += boards[i];
        }
        else {
            //allocate board to next painter
            painters++;
            boardsPainter = boards[i];
        }
    }
    return painters;
}

int findLargestMinDistance(vector<int> &boards, int k) {
    int low = *max_element(boards.begin(), boards.end());
    int high = accumulate(boards.begin(), boards.end(), 0);

    for (int time = low; time <= high; time++) {
        if (countPainters(boards, time) <= k) {
            return time;
        }
    }
    return low;
}
```
# Optimal

```cpp
int func(vector<int> &boards,int limit){
    int sum=0,cnt=1;
    for(int i=0;i<boards.size();i++){
        if(sum+boards[i]<=limit) sum += boards[i];
        else{
            sum=boards[i];
            cnt++;
        }
    }
    return cnt;
}
int findLargestMinDistance(vector<int> &boards, int k)
{
    //    Write your code here.
    int low = *max_element(boards.begin(),boards.end());
    int high = accumulate(boards.begin(),boards.end(),0);
    
    while(low<=high){
        int mid = low + (high-low)/2;
        if(func(boards,mid)>k) low = mid+1;
        else high = mid-1;
    }
    return low;
}
```

```java
import java.util.*;

public class tUf {
    public static int countPainters(ArrayList<Integer> boards, int time) {
        int n = boards.size(); // size of array.
        int painters = 1;
        long boardsPainter = 0;
        for (int i = 0; i < n; i++) {
            if (boardsPainter + boards.get(i) <= time) {
                // allocate board to current painter
                boardsPainter += boards.get(i);
            } else {
                // allocate board to next painter
                painters++;
                boardsPainter = boards.get(i);
            }
        }
        return painters;
    }

    public static int findLargestMinDistance(ArrayList<Integer> boards, int k) {
        int low = Collections.max(boards);
        int high = boards.stream().mapToInt(Integer::intValue).sum();

        // Apply binary search:
        while (low <= high) {
            int mid = (low + high) / 2;
            int painters = countPainters(boards, mid);
            if (painters > k) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return low;
    }
}
```


# For very large inputs

```java
public class Solution {
    private int getCnt(int[] arr,int limit){
        int cnt=0;
        int totalArea=0;
        for(int area:arr){
            if(totalArea+area > limit){
                cnt++;
                totalArea = area;
            }
            else totalArea+=area;
        }
        return cnt+1;
    }
    public int paint(int A, int B, int[] C) {
        int low = Arrays.stream(C).max().getAsInt();
        int high = Arrays.stream(C).sum()% 10000003;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(getCnt(C,mid)<=A)high = mid-1;
            else low = mid+1;
        }
        return (int)((1L * (high + 1) * B) % 10000003);
    }
}

```