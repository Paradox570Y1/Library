[Link](https://www.naukri.com/code360/problems/ninja-s-training_3621003?leftPanelTabValue=PROBLEM)
## Problem statement

Send feedback

Ninja is planning this ‘N’ days-long training schedule. Each day, he can perform any one of these three activities. (Running, Fighting Practice or Learning New Moves). Each activity has some merit points on each day. As Ninja has to improve all his skills, he can’t do the same activity in two consecutive days. Can you help Ninja find out the maximum merit points Ninja can earn?

You are given a 2D array of size N*3 ‘POINTS’ with the points corresponding to each day and activity. Your task is to calculate the maximum number of merit points that Ninja can earn.

**For Example**

```
If the given ‘POINTS’ array is [[1,2,5], [3 ,1 ,1] ,[3,3,3] ],the answer will be 11 as 5 + 3 + 3.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= T <= 10
1 <= N <= 100000.
1 <= values of POINTS arrays <= 100 .

Time limit: 1 sec
```

##### Sample Input 1:

```
2
3
1 2 5 
3 1 1
3 3 3
3
10 40 70
20 50 80
30 60 90
```

##### Sample Output 1:

```
11
210
```

##### Explanation of sample input 1:

```
For the first test case,
One of the answers can be:
On the first day, Ninja will learn new moves and earn 5 merit points. 
On the second day, Ninja will do running and earn 3 merit points. 
On the third day, Ninja will do fighting and earn 3 merit points. 
The total merit point is 11 which is the maximum. 
Hence, the answer is 11.

For the second test case:
One of the answers can be:
On the first day, Ninja will learn new moves and earn 70 merit points. 
On the second day, Ninja will do fighting and earn 50 merit points. 
On the third day, Ninja will learn new moves and earn 90 merit points. 
The total merit point is 210 which is the maximum. 
Hence, the answer is 210.
```

##### Sample Input 2:

```
2
3
18 11 19
4 13 7
1 8 13
2
10 50 1
5 100 11
```

##### Sample Output 2:

```
45
110
```


# Using Memoization
Results in `StackOverFlow` , need to optimize space
```java
public class Solution {
    
    private static int helper(int[][] points,int i,int j,int[][] memo){
        if(i==0)return points[i][j];
        if(memo[i][j]!=0)return memo[i][j];
        int max=0;
        for(int t=0;t<=2;t++){
            if(t==j)continue;
            max=Math.max(helper(points,i-1,t,memo),max);
        }
        return memo[i][j] = max+points[i][j];
    }
    public static int ninjaTraining(int n, int points[][]) {

        // Write your code here..
        int memo[][] = new int[n][3];
        int maxpoints=0;
        for(int i=0;i<3;i++){
            maxpoints=Math.max(helper(points,n-1,i,memo),maxpoints);
        }
        return maxpoints;
    }

}
```


OR

```java
public class Solution {
    private static int helper(int[][] points,int i,int last,int[][] memo){
        if(i<0)return 0;
        if(memo[i][last]!=0)return memo[i][last];
        int maxPt=0;
        for(int j=0;j<3;j++){
            if(j==last)continue;
            int point = points[i][j]+helper(points,i-1,j,memo);
            maxPt=Math.max(point,maxPt);
        }
        return memo[i][last] = maxPt;
    }
    public static int ninjaTraining(int n, int points[][]) {

        // Write your code here..
        int memo[][] = new int[n][4];
        return helper(points,points.length-1,3,memo);
    }

}
```

OR

```java
public class Solution {
    private static int helper(int[][] points,int i,int last,int[][] memo){
        if(i==0){
            int maxi=0;
            for(int j=0;j<3;j++){
                if(j==last)continue;
                maxi = Math.max(maxi,points[i][j]);
            }
            return maxi;
        }
        if(memo[i][last]!=0)return memo[i][last];
        int maxPt=0;
        for(int j=0;j<3;j++){
            if(j==last)continue;
            int point = points[i][j]+helper(points,i-1,j,memo);
            maxPt=Math.max(point,maxPt);
        }
        return memo[i][last] = maxPt;
    }
    public static int ninjaTraining(int n, int points[][]) {

        // Write your code here..
        int memo[][] = new int[n][4];
        return helper(points,points.length-1,3,memo);
    }

}
```

OR

```java
public class Solution {
    static int memo[][];
    public static int ninjaTraining(int n, int points[][]) {

        // Write your code here..
        memo = new int[n][3];
        for (int i = 0; i < points.length; i++) {
            memo[i][0] = -1;
            memo[i][1] = -1;
            memo[i][2] = -1;
        }
        int res = 0;
        for (int i = 0; i < 3; i++) {
            res = Math.max(res, helper(points, n-1, i));
        }
        return res;
    }
    private static int helper(int[][] points, int i, int j) {
        if(i < 0) return 0;
        if (memo[i][j] != -1) return memo[i][j];
        int res = 0;
        for (int k = 0; k < 3; k++) {
            if(j == k) continue;
            res = Math.max(res, points[i][j] + helper(points, i-1, k));
        }
        return memo[i][j] = res;
    }
}
```


# Using Tabulation 
my approach little different than standard
```java
public class Solution {
    
    public static int ninjaTraining(int n, int points[][]) {
        int dp[][] = new int[n][3];
        dp[0] = points[0];
        for(int i=1;i<n;i++){
            for(int j=0;j<3;j++){
                int maxi=0;
                for(int k=0;k<3;k++){
                    if(k==j)continue;
                    maxi = Math.max(dp[i-1][k],maxi);
                }
                dp[i][j] = points[i][j]+maxi;
            }
        }
        int ans=0;
        for(int i=0;i<3;i++){
            ans = Math.max(ans,dp[n-1][i]);
        }
        return ans;
    }

}
```

OR

```java
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        int dp[][] = new int[n][3];
        dp[0] = points[0];
        for(int day=1;day<n;day++){
            for(int last=0;last<3;last++){
                int maxi=0;
                for(int task=0;task<3;task++){
                    if(task==last)continue;
                    int point = dp[day-1][task]+points[day][last];
                    maxi = Math.max(point,maxi);
                }
                dp[day][last] = maxi;
            }
        }
        return Math.max(dp[n-1][0],Math.max(dp[n-1][1],dp[n-1][2]));
    }
}
```

After space optimization

```java
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        int dp[] = new int[3];
        dp = points[0];
        for(int day=1;day<n;day++){
            int[] buffer = new int[3];
            for(int last=0;last<3;last++){
                int maxi=0;
                for(int task=0;task<3;task++){
                    if(task==last)continue;
                    int point = dp[task]+points[day][last];
                    maxi = Math.max(point,maxi);
                }
                buffer[last] = maxi;
            }
            dp=buffer;
        }
        return Math.max(dp[0],Math.max(dp[1],dp[2]));
    }
}
```
# Standard Tabulation 

Striver's way

```java
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        int dp[][] = new int[n][4];
        dp[0][0] = Math.max(points[0][1],points[0][2]);
        dp[0][1] = Math.max(points[0][0],points[0][2]);
        dp[0][2] = Math.max(points[0][0],points[0][1]);
        dp[0][3] = Math.max(points[0][0],Math.max(points[0][1],points[0][2]));
        for(int day=1;day<n;day++){
            for(int last=0;last<4;last++){
                int maxi=0;
                for(int task=0;task<3;task++){
                    if(task==last)continue;
                    int point = dp[day-1][task]+points[day][task];
                    maxi = Math.max(point,maxi);
                }
                dp[day][last] = maxi;
            }
        }
        return dp[n-1][3];
    }
}
```


After space optimization

```java
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        int dp[] = new int[4];
        dp[0] = Math.max(points[0][1],points[0][2]);
        dp[1] = Math.max(points[0][0],points[0][2]);
        dp[2] = Math.max(points[0][0],points[0][1]);
        dp[3] = Math.max(points[0][0],Math.max(points[0][1],points[0][2]));
        for(int day=1;day<n;day++){
            int temp[] = new int[4];
            for(int last=0;last<4;last++){
                int maxi=0;
                for(int task=0;task<3;task++){
                    if(task==last)continue;
                    int point = dp[task]+points[day][task];
                    maxi = Math.max(point,maxi);
                }
                temp[last] = maxi;
            }
            dp = temp;
        }
        return dp[3];
    }
}
```

or

```java
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        // Write your code here..
        int dp[][] = new int[n+1][4];
        for(int i=0;i<n;i++){
           int curMax=0;
           for(int j=0;j<3;j++){
                int maxi=0;
                for(int k=0;k<3;k++){
                   if(j==k)continue;
                   maxi = Math.max(dp[i][k],maxi);
                }
                dp[i+1][j] = maxi+points[i][j];
                curMax = Math.max(dp[i+1][j],curMax);
           }
           dp[i+1][3] = curMax;
        }
        return dp[n][3];
    }
}
```

OR

```java
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {

        // Write your code here..
        int dp[] = new int[4];
        for(int i=0;i<n;i++){
           int curMax=0;
           int copy[] = new int[4];
           for(int j=0;j<4;j++){
               copy[j] = dp[j];
           }
           for(int j=0;j<3;j++){
                int maxi=0;
                for(int k=0;k<3;k++){
                   if(j==k)continue;
                   maxi = Math.max(copy[k],maxi);
                }
                dp[j] = maxi+points[i][j];
                curMax = Math.max(dp[j],curMax);
           }
           dp[3] = curMax;
        }
        return dp[3];
    }

}
```

OR

```java
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {

        // Write your code here..
        int dp[] = new int[3];
        int ans=0;
        for(int i=0;i<n;i++){
           int copy[] = new int[3];
           for(int j=0;j<3;j++){
               copy[j] = dp[j];
           }
           for(int j=0;j<3;j++){
                int maxi=0;
                for(int k=0;k<3;k++){
                   if(j==k)continue;
                   maxi = Math.max(copy[k],maxi);
                }
                dp[j] = maxi+points[i][j];
                ans = Math.max(dp[j],ans);
           }
        }
        return ans;
    }
}
```


OR

```java
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {

        // Write your code here..
        int run = 0, fight = 0, newMoves = 0;
        for (int point[] : points) {
            int r = point[0] + Math.max(fight, newMoves);
            int f = point[1] + Math.max(run, newMoves);
            int nm = point[2] + Math.max(run, fight);
            run = r; fight = f; newMoves = nm;
        }
        return Math.max(run, Math.max(fight, newMoves));
    }

}
```