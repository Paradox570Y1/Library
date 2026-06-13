[621. Task Scheduler](https://leetcode.com/problems/task-scheduler/)

You are given an array of CPU `tasks`, each labeled with a letter from A to Z, and a number `n`. Each CPU interval can be idle or allow the completion of one task. Tasks can be completed in any order, but there's a constraint: there has to be a gap of **at least** `n` intervals between two tasks with the same label.

Return the **minimum** number of CPU intervals required to complete all tasks.

**Example 1:**

**Input:** tasks = ["A","A","A","B","B","B"], n = 2

**Output:** 8

**Explanation:** A possible sequence is: A -> B -> idle -> A -> B -> idle -> A -> B.

After completing task A, you must wait two intervals before doing A again. The same applies to task B. In the 3rd interval, neither A nor B can be done, so you idle. By the 4th interval, you can do A again as 2 intervals have passed.

**Example 2:**

**Input:** tasks = ["A","C","A","B","D","B"], n = 1

**Output:** 6

**Explanation:** A possible sequence is: A -> B -> C -> D -> A -> B.

With a cooling interval of 1, you can repeat a task after just one other task.

**Example 3:**

**Input:** tasks = ["A","A","A", "B","B","B"], n = 3

**Output:** 10

**Explanation:** A possible sequence is: A -> B -> idle -> idle -> A -> B -> idle -> idle -> A -> B.

There are only two types of tasks, A and B, which need to be separated by 3 intervals. This leads to idling twice between repetitions of these tasks.

**Constraints:**

- `1 <= tasks.length <= 104`
- `tasks[i]` is an uppercase English letter.
- `0 <= n <= 100`

# Using Heaps

```java
class Solution {
    class Process{
        int freq;
        int waitingTime;
        Process(int freq,int waitingTime){
            this.freq = freq;
            this.waitingTime = waitingTime;
        }
    }
    public int leastInterval(char[] tasks, int n) {
        int hash[] = new int[26];
        for(char task:tasks){
            hash[task-'A']++;
        }
        PriorityQueue<Process> readyQueue = new PriorityQueue<>((a,b)->b.freq - a.freq);
        Queue<Process> jobQueue = new LinkedList<>();
        for(int i=0;i<26;i++){
            if(hash[i]>0)readyQueue.offer(new Process(hash[i],0));
        }
        int time = 0;
        while(!jobQueue.isEmpty() || !readyQueue.isEmpty()){
            time++;
            if(!readyQueue.isEmpty()){
                Process activeProcess = readyQueue.poll();
                if(activeProcess.freq>1 && activeProcess.waitingTime <= time){
                    jobQueue.offer(new Process(activeProcess.freq-1,time+n));
                }
            }
            if(!jobQueue.isEmpty() && jobQueue.peek().waitingTime <= time){
                readyQueue.offer(jobQueue.poll());
            }
        }
        return time;
    }
}
```

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a,b)->b[0]-a[0]);
        int hash[] = new int[26];
        for(char ch:tasks){
            hash[ch-'A']++;
        }
        for(int i=0;i<26;i++){
            if(hash[i]>0)
            maxHeap.add(new int[]{hash[i],0});
        }
        Queue<int[]> queue = new LinkedList<>();
        int time = 0;
        while(!queue.isEmpty() || !maxHeap.isEmpty()){
            time++;
            if(!maxHeap.isEmpty()){
                int root[] = maxHeap.remove();
                if(root[0]!=1 && root[1]<=time){
                    queue.offer(new int[]{root[0]-1,time+n});
                }
            }
            if(!queue.isEmpty() && queue.peek()[1]<=time){
                maxHeap.add(queue.poll());
            }
        }
        return time;
    }
}
```


# Better

```java
class Solution {
    class Process{
        int freq;
        int waitingTime;
        Process(int freq,int waitingTime){
            this.freq = freq;
            this.waitingTime = waitingTime;
        }
    }
    public int leastInterval(char[] tasks, int n) {
        int hash[] = new int[26];
        for(char task:tasks){
            hash[task-'A']++;
        }
        PriorityQueue<Process> readyQueue = new PriorityQueue<>((a,b)->b.freq - a.freq);
        Process[] jobQueue = new Process[tasks.length];
        int size=0,front=0;
        for(int i=0;i<26;i++){
            if(hash[i]>0)readyQueue.offer(new Process(hash[i],0));
        }
        int time = 0;
        while(size-front > 0 || !readyQueue.isEmpty()){
            time++;
            if(!readyQueue.isEmpty()){
                Process activeProcess = readyQueue.poll();
                if(activeProcess.freq>1 && activeProcess.waitingTime <= time){
                    jobQueue[size] = new Process(activeProcess.freq-1,time+n);
                    size++;
                }
            }
            if(size-front > 0 && jobQueue[front].waitingTime <= time){
                readyQueue.offer(jobQueue[front]);
                front++;
            }
        }
        return time;
    }
}
```

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a,b)->b[0]-a[0]);
        int hash[] = new int[26];
        for(char ch:tasks){
            hash[ch-'A']++;
        }
        for(int i=0;i<26;i++){
            if(hash[i]>0)
            maxHeap.add(new int[]{hash[i],0});
        }
        int queue[][] = new int[tasks.length][2];
        int front=-1,back=-1;
        int time = 0;
        while((front<=back && front!=-1) || !maxHeap.isEmpty()){
            time++;
            if(!maxHeap.isEmpty()){
                int root[] = maxHeap.remove();
                if(root[0]!=1 && root[1]<=time){
                    queue[++back] = new int[]{root[0]-1,time+n};
                    if(front==-1)front=0;
                }
            }
            if(front!=-1 && front<=back && queue[front][1]<=time){
                maxHeap.add(queue[front++]);
            }
        }
        return time;
    }
}
```

# Optimal

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int totalProcess = tasks.length;
        int hash[] = new int[26];
        for(int task:tasks){
            hash[task-'A']++;
        }
        int maxFreq=0;
        for(int freq:hash){
            maxFreq = Math.max(maxFreq,freq);
        }
        int maxFreqCnt=0;
        for(int freq:hash){
            if(maxFreq == freq)maxFreqCnt++;
        }
        int gapSize = n - (maxFreqCnt-1);
        int gapFreq = maxFreq - 1;
        int totalGap = gapSize*gapFreq;
        int remainingProcess = totalProcess - maxFreq * maxFreqCnt;
        int idleTime = Math.max(0,totalGap- remainingProcess);
        return totalProcess+idleTime;
    }
}
```

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int[] hash = new int[26];
        int maxFreq = 0;
        int maxFreqCnt = 0;
        for(char ch:tasks){
            hash[ch-'A']++;
            int freq = hash[ch-'A'];
            if(maxFreq<freq){
                maxFreq=freq;
                maxFreqCnt=0;
            }
            if(maxFreq==freq)maxFreqCnt++;
        }
        int totalTasks = tasks.length;
        int partition = maxFreq-1;
        int partitionSize = n - (maxFreqCnt-1);
        int emptySlots = partition*partitionSize;
        int leftTasks = totalTasks-maxFreq*maxFreqCnt;
        int idle = Math.max(0,emptySlots-leftTasks);
        return idle+totalTasks;
    }
}
```

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int hash[] = new int[26];
        int len = tasks.length;
        for(int i=0;i<len;i++){
            hash[tasks[i]-'A']++;
        }
        int maxi=0,maxCnt=0;
        for(int i=0;i<26;i++){
            maxi = Math.max(maxi,hash[i]);
        }
        for(int i=0;i<26;i++){
            if(maxi==hash[i])maxCnt++;
        }
        int gapSize = n - (maxCnt-1);
        int gapCnt = maxi-1;
        int totalGap = gapCnt*gapSize;
        int waitingTasks = len-(maxi*maxCnt);
        int idleTime = Math.max(0,totalGap-waitingTasks);
        return idleTime+len;
    }
}
```


```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int hash[] = new int[26];
        int len = tasks.length;
        for(int i=0;i<len;i++)hash[tasks[i]-'A']++;
        int maxi=0,maxCnt=0;
        for(int i=0;i<26;i++)maxi = Math.max(maxi,hash[i]);
        for(int i=0;i<26;i++)if(maxi==hash[i])maxCnt++;
        return Math.max(len,(maxi-1)*(n+1)+maxCnt);
    }
}
```