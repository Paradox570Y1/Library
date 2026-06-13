[239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3
**Output:** [3,3,5,5,6,7]
**Explanation:** 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       **3**
 1 [3  -1  -3] 5  3  6  7       **3**
 1  3 [-1  -3  5] 3  6  7      ** 5**
 1  3  -1 [-3  5  3] 6  7       **5**
 1  3  -1  -3 [5  3  6] 7       **6**
 1  3  -1  -3  5 [3  6  7]      **7**

**Example 2:**

**Input:** nums = [1], k = 1
**Output:** [1]

**Constraints:**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`
- `1 <= k <= nums.length`

# Brute

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int j=0;
        int n=nums.length;
        int ans[] =  new int[n-k+1];
        for(int i=k-1;i<n;i++){
            int maxi = -10001;
            for(int t=j;t<=i;t++){
                 maxi = Math.max(maxi,nums[t]);
            }
            ans[i-(k-1)] = maxi;
            j++;
        }
        return ans;
    }
}
```

# Using Priority Queue

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> nums[b] - nums[a]);
        int n = nums.length;
        int res[] = new int[n-k+1];
        int p = 0;
        for (int i = 0; i < n; i++) {
            pq.offer(i);
            if (i < k-1) continue;
            while (i >= k && pq.peek() <= i-k) {
                pq.poll();
            }
            res[p++] = nums[pq.peek()];
        }
        return res;
    }
}
```

OR

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[0] - a[0]);
        int n = nums.length;
        int res[] = new int[n-k+1];
        int p = 0;
        for (int i = 0; i < n; i++) {
            pq.offer(new int[]{nums[i], i});
            if (i < k-1) continue;
            while (i >= k && pq.peek()[1] <= i-k) {
                pq.poll();
            }
            res[p++] = pq.peek()[0];
        }
        return res;
    }
}
```
# Using Tree Set

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        TreeSet<Integer> ts = new TreeSet<>((a, b)-> {
            if (nums[a] != nums[b]) return nums[a] - nums[b];
            return  a-b;
        });
        for (int i = 0; i < k; i++) {
            ts.add(i);
        }
        int[] res = new int[nums.length-k+1];
        int p = 0;
        res[p++] = nums[ts.last()];
        for (int i = k; i < nums.length; i++) {
            ts.add(i);
            ts.remove(i-k);
            res[p++] = nums[ts.last()];
        }
        return res;
    }
}
```
# Using Dequeue
- This approach is similar to monotonic stack , here you always try to maintain biggest element withing the window in the head of the dequeue, by removing all elements from tail which seems to be smaller then the current element, this ensures next bigger element is right next to the cur windows biggest element by removing all small elements in between.
TC-> O(2N)
SC - > O(k) + O(N-K)
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        Deque<Integer> dq = new ArrayDeque<>();
        int n = nums.length;
        int ans[] = new int[n-k+1];
        for(int i=0;i<n;i++){
            int ele = nums[i];
            while(!dq.isEmpty() && nums[dq.peekFirst()]<ele)dq.pollFirst();
            dq.addFirst(i);
            if(i>=k-1)ans[i-(k-1)] = nums[dq.peekLast()];
            if(dq.peekLast()==i-k+1)dq.pollLast();
        }
        return  ans; 
    }
}
```

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        Deque<Integer> dq = new ArrayDeque<>();
        int n = nums.length;
        int ans[] = new int[n-k+1];
        for(int i=0;i<n;i++){
            int ele = nums[i];
            while(!dq.isEmpty() && nums[dq.peekLast()]<=ele)dq.pollLast();
            dq.add(i);
            if(i>=k-1)ans[i-(k-1)] = nums[dq.peek()];
            if(dq.peek()==i-k+1)dq.poll();
        }
        return  ans; 
    }
}
```

```java
 public static int[] maxSlidingWindow(int[] a, int k) {
        int n = a.length;
        int[] r = new int[n - k + 1];
        int ri = 0;
        // store index
        Deque < Integer > q = new ArrayDeque < > ();
        for (int i = 0; i < a.length; i++) {
            // remove numbers out of range k
            if (!q.isEmpty() && q.peek() == i - k) {
                q.poll();
            }
            // remove smaller numbers in k range as they are useless
            while (!q.isEmpty() && a[q.peekLast()] < a[i]) {
                q.pollLast();
            }

            q.offer(i);
            if (i >= k - 1) {
                r[ri++] = a[q.peek()];
            }
        }
        return r;
    }
```

OR

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        int dq[] = new int[n];
        int front =-1;
        int rear=-1;
        int j=0;
        int[] ans = new int[n-k+1];
        int a=0;
        for(int i=0;i<n;i++){
            while(rear!=front && nums[dq[front]]<nums[i])front--;
            dq[++front] = i;
            
            if(i-j+1 == k){
                ans[a++] = nums[dq[rear+1]];
                j++;
            }
            if(dq[rear+1]<j)rear++;
        }
        return ans;
    }
}
```