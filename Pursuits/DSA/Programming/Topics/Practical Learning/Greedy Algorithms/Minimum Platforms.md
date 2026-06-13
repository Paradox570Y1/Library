[Link](https://www.geeksforgeeks.org/problems/minimum-platforms-1587115620/1)

Difficulty: **Medium**Accuracy: **26.84%**Submissions: **516K+**Points: **4**

You are given the arrival times **arr[]** and departure times **dep[]** of all trains that arrive at a railway station on the same day. Your task is to determine the minimum number of platforms required at the station to ensure that no train is kept waiting.

At any given time, the same platform cannot be used for both the arrival of one train and the departure of another. Therefore, when two trains arrive at the same time, or when one arrives before another departs, additional platforms are required to accommodate both trains.

**Examples:**

**Input**: arr[] = [900, 940, 950, 1100, 1500, 1800], dep[] = [910, 1200, 1120, 1130, 1900, 2000]
**Output**: 3
**Explanation**: There are three trains during the time 9:40 to 12:00. So we need a minimum of 3 platforms.

**Input**: arr[] = [900, 1235, 1100], dep[] = [1000, 1240, 1200]
**Output**: 1
**Explanation**: All train times are mutually exclusive. So we need only one platform

**Input**: arr[] = [1000, 935, 1100], dep[] = [1200, 1240, 1130]
**Output**: 3
**Explanation**: All 3 trains have to be there from 11:00 to 11:30

**Constraints:  
**1≤ number of trains ≤ 50000  
0000 ≤ arr[i] ≤ dep[i] ≤ 2359  
**Note:** Time intervals are in the 24-hour format(**HHMM) ,** where the first two characters represent hour (between 00 to 23 ) and the last two characters represent minutes (this will be <= 59 and >= 0).



# Brute

```java
class Solution {
    static class Train{
        int arrivalTime;
        int depTime;
        Train(int arrivalTime,int depTime){
            this.arrivalTime = arrivalTime;
            this.depTime = depTime;
        }
    }
    static class depComp implements Comparator<Train>{
        @Override
        public int compare(Train a,Train b){
            return a.depTime - b.depTime;
        }
        
    }
    static int findPlatform(int arr[], int dep[]) {
        // add your code here
        int n = arr.length;
        Train[] train = new Train[n];
        for(int i=0;i<n;i++){
            train[i] = new Train(arr[i],dep[i]);
        }
        Arrays.sort(train,new depComp());
        ArrayList<Integer> platforms = new ArrayList<>();
        
        for(int i=0;i<n;i++){
            int arrival = train[i].arrivalTime;
            int departure = train[i].depTime;
            int pt=-1;
            for(int j=0;j<platforms.size();j++){
                if(platforms.get(j)<arrival){
                    pt=j;
                }
                else break;
            }
            if(pt==-1)platforms.add(departure);
            else {
                platforms.set(pt,departure);
                for(int j=pt+1;j<platforms.size();j++){
                    if(platforms.get(j-1)>platforms.get(j)){
                        int temp = platforms.get(j-1);
                        platforms.set(j-1,platforms.get(j));
                        platforms.set(j,temp);
                    }
                    else break;
                }
            }
        }
        return platforms.size();
    }
}
```



# Better
TC -> O(2N log 2N) + O(N) + O(2N)
SC -> O(2N) 
```java
class Solution {
    // Function to find the minimum number of platforms required at the
    // railway station such that no train waits.
    static class Train{
        int time;
        boolean arrival;
        Train(int time,boolean arrival){
            this.time = time;
            this.arrival = arrival;
        }
    }
    static class Time implements Comparator<Train>{
        @Override
        public int compare(Train a,Train b){
            return a.time - b.time;
        }
    }
    static int findPlatform(int arr[], int dep[]) {
        // add your code here
        int n = arr.length;
        Train[] train = new Train[2*n];
        for(int i=0;i<n;i++){
            train[i] = new Train(arr[i],true);
            train[i+n] = new Train(dep[i],false);
        }
        Arrays.sort(train,new Time());
        int cnt=0;
        int platform = 0;
        for(int i=0;i<2*n;i++){
            if(train[i].arrival)cnt++;
            else cnt--;
            platform = Math.max(cnt,platform);
        }
        return platform;
    }
}
```

# Optimal
TC -> O(2N log N) + O(2N)
SC -> O(1)
```java
class Solution {
    static int findPlatform(int arr[], int dep[]) {
        // add your code here
        int n = arr.length;
        Arrays.sort(arr);
        Arrays.sort(dep);
        int arrival=0, dept=0;
        int cnt=0;
        int ans=0;
        while(arrival<n){
            if(arr[arrival]<=dep[dept]){
                cnt++;
                arrival++;
            }
            else {
                cnt--;
                dept++;
            }
            ans = Math.max(ans,cnt);
        }
        return ans;
    }
}
```