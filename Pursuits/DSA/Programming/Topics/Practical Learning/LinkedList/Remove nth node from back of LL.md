[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = [1,2,3,4,5], n = 2
**Output:** [1,2,3,5]

**Example 2:**

**Input:** head = [1], n = 1
**Output:** []

**Example 3:**

**Input:** head = [1,2], n = 1
**Output:** [1]

**Constraints:**

- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

# Brute
TC -> O(2\*N)
SC -> O(1)
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode temp = head;
        int maxLen = 0;
        while(temp!=null){
            temp = temp.next;
            maxLen++;
        }
        if(n==maxLen){
            head = head.next;
            return head;
        }
        n = maxLen-n;
        temp = head;
        while(n-->1){
            temp = temp.next;
        }
        temp.next = temp.next.next;
        return head;
    }
}
```


# Optimal
TC-> O(N)
SC-> O(N)
```java
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* fast = head;
        while(n-->0)fast = fast->next;
        ListNode* slow = head;
        if(fast == NULL) return head->next;
        while(fast->next!=NULL){
            slow = slow->next;
            fast = fast->next;
        }
        ListNode* deleteNode = slow->next;
        slow->next = slow->next->next;
        delete deleteNode;
        return head;
    }
};
```