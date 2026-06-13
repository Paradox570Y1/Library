[23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**

**Input:** lists = [[1,4,5],[1,3,4],[2,6]]
**Output:** [1,1,2,3,4,4,5,6]
**Explanation:** The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6

**Example 2:**

**Input:** lists = []
**Output:** []

**Example 3:**

**Input:** lists = [[]]
**Output:** []

**Constraints:**

- `k == lists.length`
- `0 <= k <= 104`
- `0 <= lists[i].length <= 500`
- `-104 <= lists[i][j] <= 104`
- `lists[i]` is sorted in **ascending order**.
- The sum of `lists[i].length` will not exceed `104`.

# Using Merge with recursion

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null || lists.length==0)return null;
        return helper(lists,0);
    }
    private ListNode helper(ListNode[] lists,int i){
        if(lists.length-1==i)return lists[i];
        ListNode newList = helper(lists,i+1);
        return merge(lists[i],newList);
    }
    private ListNode merge(ListNode l1,ListNode l2){
        ListNode p1 = l1;
        ListNode p2 = l2;
        ListNode dummy = new ListNode(-1);
        ListNode temp = dummy;
        while(p1!=null && p2!=null){
            if(p1.val>p2.val){
                temp.next = p2;
                p2=p2.next;
            }
            else {
                temp.next = p1;
                p1=p1.next;
            }
            temp = temp.next;
        }
        if(p1==null)temp.next = p2;
        else temp.next = p1;
        return dummy.next;
    }
}
```

Using recursion to merge which makes the TC even terrible
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null || lists.length==0)return null;
        return helper(lists,0);
    }
    private ListNode helper(ListNode[] lists,int i){
        if(lists.length-1==i)return lists[i];
        ListNode newList = helper(lists,i+1);
        return merge(lists[i],newList);
    }
    private ListNode merge(ListNode l1,ListNode l2){
        if (l1 == null) return l2;
        if (l2 == null) return l1;

        if (l1.val < l2.val) {
            l1.next = merge(l1.next, l2);
            return l1;
        } else {
            l2.next = merge(l1, l2.next);
            return l2;
        }
    }
}
```
# Using Heap
TC-> O(N log k)
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        PriorityQueue<ListNode> minHeap = new PriorityQueue<>((a,b)->a.val-b.val);
        for(int i=0;i<lists.length;i++){
            if(lists[i]!=null)minHeap.add(lists[i]);
        }
        ListNode dummy = new ListNode(-1);
        ListNode temp = dummy;
        while(!minHeap.isEmpty()){
            ListNode root = minHeap.remove();
            temp.next = new ListNode(root.val);
            temp = temp.next;
            if(root.next!=null){
                root = root.next;
                minHeap.add(root);
            }
        }
        return dummy.next;
    }
}
```