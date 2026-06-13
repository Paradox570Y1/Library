[Link](https://www.geeksforgeeks.org/problems/n-meetings-in-one-room-1587115620/1)
You are given timings of **n** meetings in the form of **(start[i], end[i])** where start[i] is the start time of meeting **i** and end[i] is the finish time of meeting **i.** Return the **maximum** number of meetings that can be accommodated in a single meeting room, when only one meeting can be held in the meeting room at a particular time. 

**Note:** The start time of one chosen meeting can't be equal to the end time of the other chosen meeting.

**Examples :**

**Input:** start[] = [1, 3, 0, 5, 8, 5], end[] =  [2, 4, 6, 7, 9, 9]
**Output:** 4
**Explanation:** Maximum four meetings can be held with given start and end timings. The meetings are - (1, 2), (3, 4), (5,7) and (8,9)

**Input:** start[] = [10, 12, 20], end[] = [20, 25, 30]
**Output:** 1
**Explanation:** Only one meetings can be held with given start and end timings.

**Input:** start[] = [1, 2], end[] = [100, 99]
**Output:** 1

**Constraints:**  
1 ≤ n ≤ 105  
0 ≤ start[i] < end[i] ≤ 106


TC -> O(2N + NlogN)
SC -> O(3\*N)

On Sorting according to start time
```java
class Solution {
    // Function to find the maximum number of meetings that can
    // be performed in a meeting room.
    class meeting{
        int start;
        int end;
        meeting(int start,int end){
            this.start = start;
            this.end = end;
        }
    }
    public int maxMeetings(int start[], int end[]) {
        // add your code here
        int n = start.length;
        meeting[] meetings = new meeting[n];
        for(int i=0;i<n;i++){
            meetings[i] = new meeting(start[i],end[i]);
        }
        Arrays.sort(meetings,(a,b)->a.start-b.start);
        int cnt=0;
        int lastMeet=-1;
        for(int i=0;i<n;i++){
            meeting curMeet = meetings[i];
            if(curMeet.start>lastMeet){
                lastMeet = curMeet.end;
                cnt++;
            }
            else if(curMeet.end<lastMeet){
                lastMeet = curMeet.end;
            }
        }
        return cnt;
    }
}
```

OR
On sorting according to end time
```java
class Solution {
    // Function to find the maximum number of meetings that can
    // be performed in a meeting room.
    class meeting{
        int start;
        int end;
        meeting(int start,int end){
            this.start = start;
            this.end = end;
        }
    }
    public int maxMeetings(int start[], int end[]) {
        // add your code here
        int n = start.length;
        meeting[] meetings = new meeting[n];
        for(int i=0;i<n;i++){
            meetings[i] = new meeting(start[i],end[i]);
        }
        Arrays.sort(meetings,(a,b)->a.end-b.end);
        int cnt=0;
        int lastMeet=-1;
        for(int i=0;i<n;i++){
            meeting curMeet = meetings[i];
            if(curMeet.start>lastMeet){
                cnt++;
                lastMeet = curMeet.end;
            }
        }
        return cnt;
    }
}
```



# Now if question asks for order in which the meeting takes place


```java
class Solution {
    // Function to find the maximum number of meetings that can
    // be performed in a meeting room.
    class meeting{
        int start;
        int end;
        int id;
        meeting(int start,int end,int id){
            this.start = start;
            this.end = end;
            this.id = id;
        }
    }
    public ArrayList<Integer> maxMeetings(int start[], int end[]) {
        // add your code here
        int n = start.length;
        meeting[] meetings = new meeting[n];
        for(int i=0;i<n;i++){
            meetings[i] = new meeting(start[i],end[i],i+1);
        }
        Arrays.sort(meetings,(a,b)->a.end-b.end);
        int cnt=0;
        int lastMeet=-1;
        ArrayList<Integer> ans=new ArrayList<>();
        for(int i=0;i<n;i++){
            meeting curMeet = meetings[i];
            if(curMeet.start>lastMeet){
                cnt++;
                lastMeet = curMeet.end;
                ans.add(curMeet.id);
            }
        }
        return ans;
    }
}
```