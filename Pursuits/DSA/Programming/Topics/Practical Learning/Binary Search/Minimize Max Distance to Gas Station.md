[Link](https://www.geeksforgeeks.org/problems/minimize-max-distance-to-gas-station/1)
Difficulty: **Hard**Accuracy: **38.36%**Submissions: **60K+**Points: **8**

We have a horizontal number line. On that number line, we have gas **stations** at positions stations[0], stations[1], ..., stations[N-1], where **n** = size of the stations array. Now, we add **k** more gas stations so that **d**, the maximum distance between adjacent gas stations, is minimized. We have to find the smallest possible value of d. Find the answer **exactly** to 2 decimal places.

**Example 1:**

**Input:**
n = 10
stations = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
k = 9
**Output:** 0.50
**Explanation:** Each of the 9 stations can be added mid way between all the existing adjacent stations.

**Example 2:**

**Input:**
n = 10
stations = `[3,6,12,19,33,44,67,72,89,95]`   
k = 2   
**Output:** 14.00   
**Explanation:** Construction of gas stations at 8th(between 72 and 89) and 6th(between 44 and 67) locations.

**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **findSmallestMaxDist()** which takes a list of stations and integer k as inputs and returns the smallest possible value of d. Find the answer **exactly** to 2 decimal places.

**Expected Time Complexity**: O(n*log k)  
**Expected Auxiliary Space**: O(1)

**Constraint:**  
10 <= n <= 5000   
0 <= stations[i] <= 109   
0 <= k <= 105

**`stations`** is sorted in a **strictly increasing** order.



# Brute
**Time Complexity:** O(k*n) + O(n), n = size of the given array, k = no. of gas stations to be placed.  
**Reason:** O(k*n) to insert k gas stations between the existing stations with maximum distance. Another O(n) for finding the answer i.e. the maximum distance.

**Space Complexity:** O(n-1) as we are using an array to keep track of placed gas stations.
```cpp
class Solution {
  public:
    double findSmallestMaxDist(vector<int> &stations, int k) {
        // Code here
        int n = stations.size();
    
        int index=0;
        double maxi=-1;
        vector<int> arr(n-1,0);
        for(int j=0;j<k;j++){
            maxi=-1;
            index=-1;
            for(int i=0;i<n-1;i++){
                double diff = stations[i+1]-stations[i];
                double dist = diff/(arr[i]+1);
                if(dist>maxi){
                    maxi = dist;
                    index=i;
                }
            }
            arr[index]++;
        }
        maxi=-1;
        for(int i=0;i<n-1;i++){
                double diff = stations[i+1]-stations[i];
                double dist = diff/(arr[i]+1);
                maxi = max(maxi,dist);
            }
        return maxi;
    }
};
```

```cpp
class Solution {
  public:
    double findSmallestMaxDist(vector<int> &stations, int k) {
        int n = stations.size();
    
        int index=0;
        double maxi=-1;
        vector<int> arr(n-1,0);
        for(int j=0;j<k+1;j++){
            maxi=-1;
            index=-1;
            for(int i=0;i<n-1;i++){
                double diff = stations[i+1]-stations[i];
                double dist = diff/(arr[i]+1);
                if(dist>maxi){
                    maxi = dist;
                    index=i;
                }
            }
            arr[index]++;
        }
        return maxi;
    }
};
```
# Better
**Time Complexity:** O(nlogn + klogn),  n = size of the given array, k = no. of gas stations to be placed.  
**Reason:** Insert operation of priority queue takes logn time complexity. O(nlogn) for inserting all the indices with distance values and O(klogn) for placing the gas stations.

**Space Complexity:** O(n-1)+O(n-1)  
**Reason:** The first O(n-1) is for the array to keep track of placed gas stations and the second one is for the priority queue.
###### **Use Priority Queue**
```cpp
class Solution {
  public:
    double findSmallestMaxDist(vector<int> &stations, int k) {
        // Code here
        int n = stations.size();
    
        priority_queue<pair<double,int>> pq;
        for(int i=0;i<n-1;i++){
            pq.push({stations[i+1]-stations[i],i});
        }
        vector<int> count(n-1,1);
        for(int j=1;j<=k;j++){
            int ind = pq.top().second;
            pq.pop();
            count[ind]++;
            double original = stations[ind+1]-stations[ind];
            double new_diff = original/count[ind];
            pq.push({new_diff,ind});
        }
        return pq.top().first;
    }
};
```

```java
import java.util.*;

public class tUf {
    public static class Pair {
        double first;
        int second;

        Pair(double first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    public static double minimiseMaxDistance(int[] arr, int k) {
        int n = arr.length; // size of array.
        int[] howMany = new int[n - 1];
        PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> Double.compare(b.first, a.first));

        // insert the first n-1 elements into pq
        // with respective distance values:
        for (int i = 0; i < n - 1; i++) {
            pq.add(new Pair(arr[i + 1] - arr[i], i));
        }

        // Pick and place k gas stations:
        for (int gasStations = 1; gasStations <= k; gasStations++) {
            // Find the maximum section
            // and insert the gas station:
            Pair tp = pq.poll();
            int secInd = tp.second;

            // insert the current gas station:
            howMany[secInd]++;

            double inidiff = arr[secInd + 1] - arr[secInd];
            double newSecLen = inidiff / (double) (howMany[secInd] + 1);
            pq.add(new Pair(newSecLen, secInd));
        }

        return pq.peek().first;
    }
}
```

OR
```java
class Solution {
    private static class station{
        double dist;
        int split;
        station(double dist){
            this.dist = dist;
            split=1;
        }
        double getDist(){
            return dist/split;
        }
    }
    public static double findSmallestMaxDist(int stations[], int k) {
        // code here
        PriorityQueue<station> pq = new PriorityQueue<>((a,b)->Double.compare(b.getDist(),a.getDist()));
        int n= stations.length;
        for(int i=1;i<n;i++){
            pq.offer(new station((double)stations[i]-stations[i-1]));
        }
        while(k-->0){
            station cur = pq.poll();
            cur.split++;
            pq.offer(cur);
        }
        return pq.peek().getDist();
    }
}   
```
# Optimal
**Time Complexity:** O(n*log(Len)) + O(n), n = size of the given array, Len = length of the answer space.  
**Reason:** We are applying binary search on the answer space. For every possible answer, we are calling the function **numberOfGasStationsRequired()** that takes O(n) time complexity. And another O(n) for finding the maximum distance initially.

**Space Complexity:** O(1) as we are using no extra space to solve this problem.
![[Pasted image 20240928010245.png|300]]

```cpp
class Solution {
  public:
    int func(vector<int> &v,double limit){
        int ans=0;
        for(int i=0;i<v.size()-1;i++){
            int diff = double(v[i+1]-v[i])/limit;
            ans +=diff;
        }
        return ans;
    }
    double findSmallestMaxDist(vector<int> &v, int k) {
        double low=0;
        double high=-1;
        for(int i=0;i<v.size()-1;i++){
            high = max(high,double(v[i+1])-v[i]);
        }
        double diff = 0.000001;
        while(high-low>diff){
            double mid = (high+low)/2;
            if(func(v,mid)>k) low =mid;
            else high = mid;
        }
        return high;
    }
};
```

```cpp
class Solution {
  public:
    int func(vector<int> arr,long double n){
        int ans=0;
        for(int i=1;i<arr.size();i++){
            int diff = (arr[i]- arr[i-1])/n;
            if(diff*n == (arr[i]- arr[i-1])) diff--;
            ans +=diff;
        }
        return ans;
    }
    double findSmallestMaxDist(vector<int> &stations, int k) {
        // Code here
        int n = stations.size();
        long double low =0;
        long double high =0;
        for(int i=0;i<n-1;i++){
            high = max(high,(long double)stations[i+1]-stations[i]);
        }
        long double diff = 0.000001;
        while(high-low > diff){
            long double mid = (low+high)/(2.0);
            int check = func(stations,mid);
            if(check > k) low = mid;
            else high = mid;
        }
        return low;
    }//there might be cases not working due to 0.01 value less
};
```

# Optimal in java

```java
// User function Template for Java

class Solution {
    private static int cntStations(int[] arr,double minDist){
        int cnt=0;
        int n=  arr.length;
        for(int i=1;i<n;i++){
            cnt+= (arr[i] - arr[i-1])/minDist;
        }
        return cnt;
    }
    public static double findSmallestMaxDist(int stations[], int k) {
        // code here
        double low = 0;
        double high =-1;
        for(int ele:stations){
            high = Math.max(high,ele);
        }
        while(0.0000001<high-low){ //ensure we are keeping high-low greater bcz in double -ve value can pose an error
            double mid = low + (high-low)/2;
            if(cntStations(stations,mid)>k)low = mid;
            else high = mid;
        }
        return high;
    }
}

```