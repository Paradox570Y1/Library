[146. LRU Cache](https://leetcode.com/problems/lru-cache/)

Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**

**Input**
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
**Output**
[null, null, null, 1, null, -1, null, -1, 3, 4]

**Explanation**
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4

**Constraints:**

- `1 <= capacity <= 3000`
- `0 <= key <= 104`
- `0 <= value <= 105`
- At most `2 * 105` calls will be made to `get` and `put`.


# Brute

```java
class LRUCache {
    Deque<Integer> dq;
    HashMap<Integer,Integer> hm;
    int limit;
    public LRUCache(int capacity) {
        dq = new ArrayDeque<>();
        limit = capacity;
        hm = new HashMap<>();
    }
    private int fetchKey(int key){
        dq.remove(key);
        dq.offer(key);
        return hm.get(key);
    }
    public int get(int key) {
        if(hm.containsKey(key))return fetchKey(key);
        return -1;
    }
    
    public void put(int key, int value) {
        if(hm.containsKey(key)){
            dq.remove(key);
        }
        if(dq.size() == limit){
            hm.remove(dq.pollFirst());
        }
        
        dq.offer(key);
        hm.put(key,value);
    }
}

```

# Better

```java
class Node{
    int key;
    int val;
    Node next,prev;
    Node(int key,int val){
        this.key = key;
        this.val = val;
        next = prev = null;
    }
}
class LRUCache {
    int size;
    HashMap<Integer,Node> hm;
    Node head,tail;
    public void attachFirst(Node newNode){
        Node temp = head.next;
        head.next = newNode;
        newNode.next = temp;
        temp.prev = newNode;
        newNode.prev = head;
    }
    public void skipNext(Node temp){
        Node destiny = temp.next.next;
        temp.next = destiny;
        destiny.prev = temp;
    }
    public void removeLRU(Node temp){
        Node newBack = temp.prev;
        if(head != newBack){
            newBack.next = tail;
            tail.prev = newBack;
        }
    }
    public LRUCache(int capacity) {
        size = capacity;
        hm = new HashMap<>();
        head = new Node(-1,-1);
        tail = new Node(-1,-1);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        if(hm.containsKey(key)){
            Node ans = hm.get(key);
            skipNext(ans.prev);
            attachFirst(ans);
            return ans.val;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        Node newNode = new Node(key,value);
        if(hm.size()<size || hm.containsKey(key)){
            if(hm.containsKey(key)){
                newNode = hm.get(key);
                skipNext(newNode.prev);
                newNode.val = value;
            }
            else hm.put(key,newNode);
        }
        else{
            hm.remove(tail.prev.key);
            removeLRU(tail.prev);
            hm.put(key,newNode);
        }
        attachFirst(newNode);
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

Little better execution

```java
class Node{
    int key;
    int val;
    Node next,prev;
    Node(int key,int val){
        this.key = key;
        this.val = val;
        next = prev = null;
    }
}
class LRUCache {
    int size;
    HashMap<Integer,Node> hm;
    Node head,tail;
    public void attachFirst(Node newNode){
        Node temp = head.next;
        head.next = newNode;
        newNode.next = temp;
        temp.prev = newNode;
        newNode.prev = head;
    }
    public void removeNode(Node temp){
        Node destiny = temp.next;
        temp=temp.prev;
        temp.next = destiny;
        destiny.prev = temp;
    }
    public LRUCache(int capacity) {
        size = capacity;
        hm = new HashMap<>();
        head = new Node(-1,-1);
        tail = new Node(-1,-1);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        if(hm.containsKey(key)){
            Node ans = hm.get(key);
            removeNode(ans);
            attachFirst(ans);
            return ans.val;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if(hm.containsKey(key)){
            Node newNode = hm.get(key);
            removeNode(newNode);
            newNode.val = value;
            attachFirst(newNode);
        }
        else{
            if(hm.size() == size){
                hm.remove(tail.prev.key);
                removeNode(tail.prev);
            }
            Node newNode = new Node(key,value);
            hm.put(key,newNode);
            attachFirst(newNode);
        }
    }
}
```


OR

```java
class LRUCache {
    class Node{
        Node next;
        Node prev;
        int val,key;
        Node(int key,int val){
            this.val = val;
            this.key = key;
            next = prev = null;
        }
    }
    int capacity;
    int size;
    Node head,tail;
    HashMap<Integer,Node> hm;
    public LRUCache(int capacity) {
        this.capacity = capacity;
        head = new Node(-1,-1);
        tail = new Node(-1,-1);
        head.next = tail;
        tail.prev =head;
        hm = new HashMap<>();
        size=0;
    }
    private void insertAtRecent(Node cur){
        Node front = head.next;
        head.next = cur;
        cur.next = front;
        cur.prev = head;
        front.prev = cur;
    }
    private void removeNode(Node cur){
        Node back = cur.prev;
        Node front = cur.next;
        back.next = front;
        front.prev = back;
    }
    private void shiftToRecent(Node cur){
        removeNode(cur);
        insertAtRecent(cur);
    }
    public int get(int key) {
        if(hm.containsKey(key)){
            Node found = hm.get(key);
            shiftToRecent(found);
            return found.val;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if(hm.containsKey(key)){
            Node cur = hm.get(key);
            shiftToRecent(cur);
            cur.val = value;
            return;
        }
        if(size == capacity){
            Node rear = tail.prev;
            hm.remove(rear.key);
            removeNode(rear);
            size--;
        }
        Node newNode = new Node(key,value);
        hm.put(key,newNode);
        insertAtRecent(newNode);
        size++;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```