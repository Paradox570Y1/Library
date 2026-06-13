[Link](https://www.naukri.com/code360/problems/unbounded-knapsack_1215029?leftPanelTabValue=PROBLEM)
## Problem statement

Send feedback

You are given _**‘n’**_ items with certain _**‘profit’**_ and _**‘weight’**_ and a knapsack with weight capacity _**‘w’**_.
You need to fill the knapsack with the items in such a way that you get the maximum profit. You are allowed to take one item multiple times.

**Example:**

```
Input: 
'n' = 3, 'w' = 10, 
'profit' = [5, 11, 13]
'weight' = [2, 4, 6]

Output: 27

Explanation:
We can fill the knapsack as:

1 item of weight 6 and 1 item of weight 4.
1 item of weight 6 and 2 items of weight 2.
2 items of weight 4 and 1 item of weight 2.
5 items of weight 2.

The maximum profit will be from case 3 = 11 + 11 + 5 = 27. Therefore maximum profit = 27.
```

Detailed explanation ( Input/output format, Notes, Images )

**Sample Input 1:**

```
3 15
7 2 4
5 10 20
```


**Expected Answer:**

```
21
```

  

**Output on console:**

```
21
```

**Explanation of Sample Input 1**

```
The given knapsack capacity is 15. We can fill the knapsack as [1, 1, 1] giving us profit 21 and as [1,2] giving us profit 9. Thus maximum profit will be 21.
```

**Sample Input 2**

```
2 3
6 12
4 17
```

**Expected Answer:**

```
0
```

**Output on console:**

```
0
```


**Explanation of Sample Input 2:**

```
We can clearly see that no item has weight less than knapsack capacity. Therefore we can not fill knapsack with any item.
```


**Expected Time Complexity:**

```
Try to solve this in O(n*w).
```


**Constraints**

```
1 <= n <= 10^3
1 <= w <= 10^3
1 <= profit[i] , weight[i] <= 10^8

Time Limit: 1 sec
```


# Using Heaps

```java
import java.util.Comparator;
import java.util.PriorityQueue;
public class Solution {
    static class Item{
        int profit;
        int weight;
        Item(int profit,int weight){
            this.profit = profit;
            this.weight = weight;
        }
        double worth(){
            return profit/(double)weight;
        }
    }
    static class compareItem implements Comparator<Item>{
        public int compare(Item t1,Item t2){
            return Double.compare(t2.worth(),t1.worth());
        }
    }
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        // Write your code here.
        PriorityQueue<Item> maxHeap = new PriorityQueue<>(new compareItem());
        for(int i=0;i<n;i++){
            Item item = new Item(profit[i],weight[i]);
            maxHeap.offer(item);
        }
        int maxProfit = 0;
        while(!maxHeap.isEmpty() && w>0){
            Item item = maxHeap.poll();
            if(w>=item.weight){
                int itemCnt = w/item.weight;
                maxProfit += item.profit*itemCnt;
                w -= item.weight*itemCnt;
            }
        }
        return maxProfit;
    }
}

```
# Using memoization

```java
public class Solution {
    private static int helper(int[] profit,int[] weight,int i,int w,int[][] memo){
        if(i==0){
            if(w==0)return 0;
            else if(w%weight[0]==0)return profit[0]*(w/weight[0]);
            return Integer.MIN_VALUE;
        }
        if(memo[i][w]!=0)return memo[i][w];
        int pick=0;
        if(weight[i]<=w)pick =profit[i] + helper(profit,weight,i,w-weight[i],memo);
        int notPick = helper(profit,weight,i-1,w,memo);
        return memo[i][w] = Math.max(pick,notPick);
    }
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        // Write your code here.
        int memo[][] = new int[n][w+1];
        return helper(profit,weight,n-1,w,memo);
    }
}
```

OR

```java
public class Solution {
    private static int helper(int[] profit,int[] weight,int i,int w,int[][] memo){
        if(i==0){
            return profit[0]*(w/weight[0]);
        }
        if(memo[i][w]!=0)return memo[i][w];
        int pick=0;
        if(weight[i]<=w)pick =profit[i] + helper(profit,weight,i,w-weight[i],memo);
        int notPick = helper(profit,weight,i-1,w,memo);
        return memo[i][w] = Math.max(pick,notPick);
    }
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        // Write your code here.
        int memo[][] = new int[n][w+1];
        return helper(profit,weight,n-1,w,memo);
    }
}
```

OR

```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        // Write your code here.
        int memo[][] = new int[n][w+1];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= w; j++) {
                memo[i][j] = -1;
            }
        }
        int val= helper(profit, weight, n-1, w, memo);
        if (val < 0) return 0;
        return val;
    }
    private static int helper(int[] profit, int[] weight, int i, int T, int[][] memo) {
        if(T == 0) return 0;
        if(i < 0 || T < 0) return (int) -1e9;
        if(memo[i][T] != -1) return memo[i][T];
        int p1 = helper(profit, weight, i-1, T, memo);
        int p2 = profit[i] + helper(profit, weight, i, T-weight[i], memo);
        return memo[i][T] = Math.max(p1, p2);
    }
}

```
# Using Tabulation

```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
      
        int prev[] = new int[w+1];
        for(int i=1;i<=w;i++){
            if(i%weight[0] == 0) prev[i] = profit[0] * (i/weight[0]);
            else prev[i] = Integer.MIN_VALUE;
        }

        for(int i=1;i<n;i++){
            int cur[] = new int[w+1];
            for(int j=0;j<=w;j++){
                int notpick = prev[j];
                int pick=0;
                if(weight[i]<=j)pick =profit[i] + cur[j-weight[i]];
                cur[j] = Math.max(pick,notpick);
            }
            prev = cur;
        }
        return prev[w];
    }
}
```

OR

```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
      
        int prev[] = new int[w+1];
        for(int i=0;i<=w;i++){
            prev[i] = profit[0] * (i/weight[0]);
        }

        for(int i=1;i<n;i++){
            int cur[] = new int[w+1];
            for(int j=0;j<=w;j++){
                int notpick = prev[j];
                int pick=0;
                if(weight[i]<=j)pick =profit[i] + cur[j-weight[i]];
                cur[j] = Math.max(pick,notpick);
            }
            prev = cur;
        }
        return prev[w];
    }
}
```

OR

```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        // Write your code here.
        int dp[] = new int[w+1];
        for(int i=0;i<n;i++){
            for(int j=0;j<=w;j++){
                int existingProfit = dp[j];
                int newProfit = 0;
                if(weight[i]<=j)newProfit = dp[j-weight[i]] + profit[i];
                dp[j] = Math.max(existingProfit,newProfit);
            }
        }
        return dp[w];
    }
}
```

OR

```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        // Write your code here.
        int dp[] = new int[w+1];
        for(int i=0;i<n;i++){
            for(int j=weight[i];j<=w;j++){
                dp[j] = Math.max(dp[j],dp[j-weight[i]] + profit[i]);
            }
        }
        return dp[w];
    }
}
```