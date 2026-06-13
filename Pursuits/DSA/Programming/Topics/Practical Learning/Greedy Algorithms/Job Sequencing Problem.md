[Link](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1)

You are given three arrays: `id`, `deadline`, and `profit`, where each job is associated with an ID, a deadline, and a profit. Each job takes 1 unit of time to complete, and only one job can be scheduled at a time. You will earn the profit associated with a job only if it is completed by its deadline.

Your task is to find:

1. The maximum number of jobs that can be completed within their deadlines.
2. The total maximum profit earned by completing those jobs.

**Examples :**

**Input:** id = [1, 2, 3, 4], deadline = [4, 1, 1, 1], profit = [20, 1, 40, 30]
**Output:** [2, 60]
**Explanation:** Job1 and Job3 can be done with maximum profit of 60 (20+40).

**Input:** id = [1, 2, 3, 4, 5], deadline = [2, 1, 2, 1, 1], profit = [100, 19, 27, 25, 15]
**Output:** [2, 127]
**Explanation:** Job1 and Job3 can be done with maximum profit of 127 (100+27).

**Input:** id = [1, 2, 3, 4], deadline = [3, 1, 2, 2], profit = [50, 10, 20, 30]
**Output:** [3, 100]
**Explanation:** Job1, Job3 and Job4 can be completed with a maximum profit of 100 (50 + 20 + 30).

**Constraints:**  
1 <=  id.size() == deadline.size() == profit.size() <= 105  
1 <= id[i], deadline[i] <= id.size()  
1 <= profit <= 500


# Brute

```java
class Solution {
    class Job{
        int deadline;
        int profit;
        Job(int deadline, int profit){
            this.deadline = deadline;
            this.profit = profit;
        }
    }
    class Time implements Comparator<Job>{
        @Override
        public int compare(Job a,Job b){
            return b.profit - a.profit;
        }
    }
    public ArrayList<Integer> JobSequencing(int[] id, int[] deadline, int[] profit) {
        // code here..
        int n = id.length;
        Job[] job = new Job[n];
        int maxi=0;
        for(int i=0;i<n;i++){
            job[i] = new Job(deadline[i],profit[i]);
            maxi = Math.max(maxi,deadline[i]);
        }
        Arrays.sort(job,new Time());
        int cnt=0;
        int maxProfit=0;
        int day=maxi;
        boolean didJob[] = new boolean[maxi+1];
        for(int i=0;i<n;i++){
            while(didJob[day]){
                day--;
                if(day==0)break;
            }
            if(job[i].deadline>=day){
                while(day>0 && didJob[day])day--;
                if(day==0)break;
                cnt++;
                maxProfit+=job[i].profit;
                day--;
            }
            else{
                int newDay = job[i].deadline;
                while(newDay>0 && didJob[newDay])newDay--;
                if(newDay == 0)continue;
                cnt++;
                maxProfit+=job[i].profit;
                didJob[newDay] = true;
            }
            if(day==0)break;
        }
        return new ArrayList<>(List.of(cnt,maxProfit));
    }
}
```


# Better for readability
```java
class Solution {
    class Job{
        int deadline;
        int profit;
        Job(int deadline, int profit){
            this.deadline = deadline;
            this.profit = profit;
        }
    }
    class Time implements Comparator<Job>{
        @Override
        public int compare(Job a,Job b){
            return b.profit - a.profit;
        }
    }
    public ArrayList<Integer> JobSequencing(int[] id, int[] deadline, int[] profit) {
        // code here..
        int n = id.length;
        Job[] job = new Job[n];
        int maxi=0;
        for(int i=0;i<n;i++){
            job[i] = new Job(deadline[i],profit[i]);
            maxi = Math.max(maxi,job[i].deadline);
        }
        Arrays.sort(job,new Time());
        int cnt=0;
        int maxProfit=0;
        boolean didJob[] = new boolean[maxi+1];
        for(int i=0;i<n;i++){
            int day = job[i].deadline;
            while(day>0 && didJob[day])day--;
            if(day==0)continue;
            cnt++;
            maxProfit+=job[i].profit;
            didJob[day] = true;
        }
        return new ArrayList<>(List.of(cnt,maxProfit));
    }
}
```