[Link](https://www.geeksforgeeks.org/problems/page-faults-in-lru5603/1)

Difficulty: **Easy**Accuracy: **25.51%**Submissions: **59K+**Points: **2**

In operating systems that use paging for memory management, page replacement algorithm is needed to decide which page needs to be replaced when the new page comes in. Whenever a new page is referred and is not present in memory, the page fault occurs and Operating System replaces one of the existing pages with a newly needed page.

Given a sequence of pages in an array **pages[]** of length **N** and memory capacity **C**, find the number of page faults using Least Recently Used (LRU) Algorithm. 

_**Note:-** Before solving this example revising the OS LRU cache mechanism is recommended._

**Example 1:**

**Input:** N = 9, C = 4
pages = {5, 0, 1, 3, 2, 4, 1, 0, 5}
**Output:** 8
**Explaination:** memory allocated with 4 pages 5, 0, 1, 
3: page fault = 4
page number 2 is required, replaces LRU 5: 
page fault = 4+1 = 5
page number 4 is required, replaces LRU 0: 
page fault = 5 + 1 = 6
page number 1 is required which is already present: 
page fault = 6 + 0 = 6
page number 0 is required which replaces LRU 3: 
page fault = 6 + 1 = 7
page number 5 is required which replaces LRU 2: 
page fault = 7 + 1  = 8.

**Your Task:**  
You do not need to read input or print anything. Your task is to complete the function **pageFaults()** which takes N, C and pages[] as input parameters and returns the number of page faults.

**Expected Time Complexity:** O(N*C)  
**Expected Auxiliary Space:** O(N)

**Constraints:**  
1 ≤ N ≤ 1000  
1 ≤ C ≤ 100  
1 ≤ pages[i] ≤ 1000


# Brute

```java
class Solution{
    static int pageFaults(int N, int C, int pages[]){
        // code here
        int memory[] = new int[C];
        int stackPointer = 0;
        int cnt=0;
        for(int i=0;i<N;i++){
            int exist=-1;
            for(int j=0;j<stackPointer;j++){
                if(memory[j] == pages[i]){
                    exist = j;
                    break;
                }
            }
            if(exist==-1){
                if(stackPointer == C){
                    for(int j=0;j<C-1;j++){
                        memory[j] = memory[j+1];
                    }
                    memory[C-1] = pages[i];
                }
                else{
                    memory[stackPointer] = pages[i];
                    stackPointer++;
                }
                cnt++;
            }
            else{
                int temp = memory[exist];
                for(int j=exist;j<stackPointer-1;j++){
                    memory[j] = memory[j+1];
                }
                memory[stackPointer-1] = temp;
            }
        }
        return cnt;
    }
}
```


# Using Deque

```java
class Solution{
    static int pageFaults(int N, int C, int pages[]){
        // code here
        Deque<Integer> cache = new ArrayDeque<>();
        HashSet<Integer> hs = new HashSet<>();
        int pageFaults=0;
        for(int page:pages){
            if(!hs.contains(page)){
                pageFaults++;
                if(cache.size()==C){
                    int last = cache.removeLast();
                    hs.remove(last);
                }
                hs.add(page);
            }
            else{
                cache.remove(page);
            }
            cache.addFirst(page);
        }
        return pageFaults;
    }
}
```
# Using LinkedHashSet

```java
class Solution{
    static int pageFaults(int N, int C, int pages[]){
        // code here
        Set<Integer> cache = new LinkedHashSet<>(C);
        int cnt=0;
        for(int i=0;i<N;i++){
            int page = pages[i];
            if(!cache.contains(page)){
                cnt++;
                if(cache.size()<C){
                    cache.add(page);
                }
                else{
                    Iterator<Integer> LRU = cache.iterator();
                    LRU.next();//moves to first element
                    LRU.remove();removes that element
                    cache.add(page);
                }
            }
            else{
                cache.remove(page);
                cache.add(page);
            }
        }
        return cnt;
    }
}
```