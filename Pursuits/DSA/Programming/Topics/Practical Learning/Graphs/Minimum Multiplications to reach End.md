[Link](https://www.geeksforgeeks.org/problems/minimum-multiplications-to-reach-end/1)
Given **start**, **end** and an array **arr** of **n** numbers. At each step, **start** is multiplied with any number in the array and then mod operation with **100000** is done to get the new start.

Your task is to find the minimum steps in which **end** can be achieved starting from **start**. If it is not possible to reach **end**, then return **-1**.

**Example 1:**

**Input:**
arr[] = {2, 5, 7}
start = 3, end = 30
**Output:**
2
**Explanation:**
Step 1: 3*2 = 6 % 100000 = 6 
Step 2: 6*5 = 30 % 100000 = 30

**Example 2:**

**Input:**
arr[] = {3, 4, 65}
start = 7, end = 66175
**Output:**
4
**Explanation:**
Step 1: 7*3 = 21 % 100000 = 21 
Step 2: 21*3 = 63 % 100000 = 63 
Step 3: 63*65 = 4095 % 100000 = 4095 
Step 4: 4095*65 = 266175 % 100000 = 66175

**Your Task:  
**You don't need to print or input anything. Complete the function **minimumMultiplications()** which takes an integer array **arr**, an integer **start** and an integer **end** as the input parameters and returns an integer, denoting the minumum steps to reach in which **end** can be achieved starting from **start**.

**Expected Time Complexity:** O(105)  
**Expected Space Complexity:** O(105)

**Constraints:**

- 1 <= n <= 104
- 1 <= arr[i] <= 104
- 1 <= start, end < 105


- The thing about this problem is that modulo forces us to move forward only as using MOD we actually create a new number when it's about to pass 1e5 size and that might be the number which later makes up the result so normally diving the end by a number will not lead us to the correct start.


# Using BFS
- It's extra overhead to sort as this overhead will be greater than its benefit which may occur in lucky cases where it prevents unnecessary computation
```java
// User function Template for Java

class Solution {
    int minimumMultiplications(int[] arr, int start, int end) {

        // Your code here
        if (start == end) return 0;
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        int MOD = (int) 1e5;
        Arrays.sort(arr);
        boolean vis[] = new boolean[MOD];
        vis[start] = true;
        int count = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                int num = q.poll();
                if (num == end) return count;
                for (int i = arr.length -1; i >= 0; i--) {
                    int next = (num * arr[i]) % MOD;
                    if (!vis[next]) {
                        vis[next] = true;
                        q.offer(next);
                    }
                    else if (next == end) {
                        return count + 1;
                    }
                }
            }
            count++;
        }
        return -1;
    }
}

```
# Optimal

```java
// User function Template for Java

class Solution {
    int minimumMultiplications(int[] arr, int start, int end) {

        // Your code here
        if (start == end) return 0;
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        int MOD = (int)1e5;
        boolean[] vis = new boolean[MOD];
        vis[start] = true;
        int steps = 1;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-->0) {
                int u = q.poll();
                for (int v : arr) {
                    int w = (int)((long)u * v) % MOD;
                    if (w == end) return steps;
                    if (!vis[w]) {
                        vis[w] = true;
                        q.offer(w);
                    }
                }
            }
            steps++;
        }
        return -1;
    }
}
```

# Using Dijkstra

- Since we have unit weights therefore BFS is sufficient for our cause
```java
// User function Template for Java

class Solution {
    class Node{
        int opCount;
        int num;
        Node(int opCount, int num) {
            this.opCount = opCount;
            this.num = num;
        }
    }
    int minimumMultiplications(int[] arr, int start, int end) {

        // Your code here
        int MOD = (int) 1e5;
        int dist[] = new int[MOD];
        Arrays.fill(dist, (int) 1e9);
        
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> a.opCount - b.opCount);
        pq.offer(new Node(0, start));
        dist[start] = 0;
        while (!pq.isEmpty()) {
            Node parent = pq.poll();
            if (parent.num == end) return parent.opCount;
            for (int op : arr) {
                int child = (parent.num * op) % MOD;
                
                if (parent.opCount + 1 < dist[child]) {
                    dist[child] = parent.opCount + 1;
                    if (child == end) return dist[child];
                    pq.offer(new Node(dist[child], child));
                }
            }
        }
        return -1;
    }
}

```



OR

Dijkstra using visited array instead of dist array
```java
// User function Template for Java

class Solution {
    class Node{
        int opCount;
        int num;
        Node(int opCount, int num) {
            this.opCount = opCount;
            this.num = num;
        }
    }
    int minimumMultiplications(int[] arr, int start, int end) {

        // Your code here
        int n = arr.length;
        int MOD = (int) 1e5;
        
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> a.opCount - b.opCount);
        boolean[] vis = new boolean[MOD];
        pq.offer(new Node(0, start));
        vis[start] = true;
        while (!pq.isEmpty()) {
            Node parent = pq.poll();
            if (parent.num == end) return parent.opCount;
            
            for (int op : arr) {
                int child = (parent.num * op) % MOD;
                if (!vis[child]) {
                    vis[child] = true;
                    pq.offer(new Node(parent.opCount + 1, child));
                }
            }
        }
        return -1;
    }
}

```