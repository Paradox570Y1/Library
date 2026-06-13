[460. LFU Cache](https://leetcode.com/problems/lfu-cache/)

Design and implement a data structure for a [Least Frequently Used (LFU)](https://en.wikipedia.org/wiki/Least_frequently_used) cache.

Implement the `LFUCache` class:

- `LFUCache(int capacity)` Initializes the object with the `capacity` of the data structure.
- `int get(int key)` Gets the value of the `key` if the `key` exists in the cache. Otherwise, returns `-1`.
- `void put(int key, int value)` Update the value of the `key` if present, or inserts the `key` if not already present. When the cache reaches its `capacity`, it should invalidate and remove the **least frequently used** key before inserting a new item. For this problem, when there is a **tie** (i.e., two or more keys with the same frequency), the **least recently used** `key` would be invalidated.

To determine the least frequently used key, a **use counter** is maintained for each key in the cache. The key with the smallest **use counter** is the least frequently used key.

When a key is first inserted into the cache, its **use counter** is set to `1` (due to the `put` operation). The **use counter** for a key in the cache is incremented either a `get` or `put` operation is called on it.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**

**Input**
["LFUCache", "put", "put", "get", "put", "get", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [3], [4, 4], [1], [3], [4]]
**Output**
[null, null, null, 1, null, -1, 3, null, -1, 3, 4]

**Explanation**
// cnt(x) = the use counter for key x
// cache=[] will show the last used order for tiebreakers (leftmost element is  most recent)
LFUCache lfu = new LFUCache(2);
lfu.put(1, 1);   // cache=[1,_], cnt(1)=1
lfu.put(2, 2);   // cache=[2,1], cnt(2)=1, cnt(1)=1
lfu.get(1);      // return 1
                 // cache=[1,2], cnt(2)=1, cnt(1)=2
lfu.put(3, 3);   // 2 is the LFU key because cnt(2)=1 is the smallest, invalidate 2.
                 // cache=[3,1], cnt(3)=1, cnt(1)=2
lfu.get(2);      // return -1 (not found)
lfu.get(3);      // return 3
                 // cache=[3,1], cnt(3)=2, cnt(1)=2
lfu.put(4, 4);   // Both 1 and 3 have the same cnt, but 1 is LRU, invalidate 1.
                 // cache=[4,3], cnt(4)=1, cnt(3)=2
lfu.get(1);      // return -1 (not found)
lfu.get(3);      // return 3
                 // cache=[3,4], cnt(4)=1, cnt(3)=3
lfu.get(4);      // return 4
                 // cache=[4,3], cnt(4)=2, cnt(3)=3

**Constraints:**

- `1 <= capacity <= 104`
- `0 <= key <= 105`
- `0 <= value <= 109`
- At most `2 * 105` calls will be made to `get` and `put`.

# Using custom doubly linked list with deque logic but more flexible for the question

```java
class LFUCache {
    HashMap<Integer,DLLNode> cache;
    HashMap<Integer,DoubleLinkedList> listOfDLL;
    int curSize,cacheSize,minFreq;
    public LFUCache(int capacity) {
        cache = new HashMap<>();
        listOfDLL = new HashMap<>();
        curSize=0;
        cacheSize = capacity;
        minFreq=0;
    }
    
    public int get(int key) {
        if(!cache.containsKey(key)){
            return -1;
        }
        DLLNode temp = cache.get(key);
        updateNode(temp);
        return temp.val;
    }
    
    public void put(int key, int value) {
        if(cacheSize==0)return;
        if(cache.containsKey(key)){
            DLLNode temp = cache.get(key);
            temp.val = value;
            updateNode(temp);
        }
        else{
            if(curSize == cacheSize){
                DoubleLinkedList base = listOfDLL.get(minFreq);
                cache.remove(base.tail.prev.key);
                base.removeNode(base.tail.prev);
                curSize--;
            }
            curSize++;
            minFreq = 1;
            DoubleLinkedList newList = new DoubleLinkedList();
            if(listOfDLL.containsKey(1)){
                newList = listOfDLL.get(1);
            }
            DLLNode newNode = new DLLNode(key,value);
            newList.addFront(newNode);
            cache.put(key,newNode);
            listOfDLL.put(1,newList);
        }
    }
    void updateNode(DLLNode temp){
        DoubleLinkedList currFreqList = listOfDLL.get(temp.freq);
        currFreqList.removeNode(temp);
        if(currFreqList.size==0 && temp.freq == minFreq)minFreq++;
        DoubleLinkedList upperFreqList = new DoubleLinkedList();
        temp.freq++;
        if(listOfDLL.containsKey(temp.freq)){
            upperFreqList = listOfDLL.get(temp.freq);
        }
        upperFreqList.addFront(temp);
        listOfDLL.put(temp.freq,upperFreqList);
    }
}
class DLLNode{
    int val,key,freq;
    DLLNode next,prev;
    DLLNode(int key,int val){
        this.key = key;
        this.val = val;
        freq=1;
        next = prev = null;
    }
}

class DoubleLinkedList{
    DLLNode head,tail;
    int size;
    DoubleLinkedList(){
        head = new DLLNode(0,0);
        tail = new DLLNode(0,0);
        head.next = tail;
        tail.prev = head;
        size=0;
    }
    void addFront(DLLNode temp){
        DLLNode afterHead = head.next;
        head.next = temp;
        temp.next = afterHead;
        afterHead.prev = temp;
        temp.prev = head;
        size++;
    }
    void removeNode(DLLNode temp){
        DLLNode before = temp.prev;
        DLLNode after = temp.next;
        before.next = after;
        after.prev = before;
        size--;
    }
}
/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache obj = new LFUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

Unimplementable code
```java
class Node{
    Node next,prev;
    int key,value;
    Node(key,value){
        this.key = key;
        this.value = value;
        next = prev = null;
    }
}
class LFUCache {
    HashMap<Node,Node> findTail;
    HashMap<Integer,Node> freqHead;
    HashMap<Integer,Integer> Freq;
    HashMap<Integer,HashMap<Integer,Node>> hml;
    int maxFreq,capacity,curSize;
    public LFUCache(int capacity) {
        findTail = new HashMap<>();
        freqHead = new HashMap<>();
        Freq = new HashMap<>();
        hml = new HashMap<>();
        maxFreq=0;
        this.capacity = capacity;
        curSize=0;
    }
    
    public int get(int key) {
        
    }
    public void addNode(Node temp,Node head){
        Node afterHead = head.next;
        head.next = temp;
        temp.next = afterHead;
        afterHead.prev = temp;
        temp.prev = head;
    }
    public void removeNode(Node temp){
        Node before = temp.prev;
        Node after = temp.next;
        before.next = after;
        after.prev = before;
    }
    public void put(int key, int value) {
        int freq = Freq.getOrDefault(key,0)+1;
        maxFreq = Math.max(freq,maxFreq);
        if(freq==1){
            Node head = new Node(0,0);
            Node tail = new Node(0,0);
            head.next = tail;
            tail.prev = head;
            Node newNode = new Node(key,value);
            addNode(newNode,head);
            freqHead.put(freq,head);
            findTail.put(head,tail);
            HashMap<Integer,Node> hm = new HashMap<>();
            hm.put(key,newNode);
            hml.put(freq,hm);
            curSize++;
        }
        else{
            Node head = freqHead.get(freq);
            Node tail = findTail.get(head);
            HashMap<Integer,Node> hm = hml.get(freq);
            if(!hm.containsKey(key)){
                if(curSize==capacity){

                    curSize--;
                }
                Node newNode = new Node(key,value);
                addNode(newNode,head);
                hm.put(key,newNode);
                curSize++;
            }
            else{
                Node newNode = hm.get(key);
                removeNode(newNode);
                newNode.value = value;
                addNode(newNode);
            }
        }
        Freq.put(key,freq);
    }
}

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache obj = new LFUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

OR

```java

class LFUCache {
    class Node{
        Node prev;
        Node next;
        int key;
        int val;
        int freq;
        Node(int key,int val){
            this.key = key;
            this.val = val;
            this.freq=1;
            prev = next = null;
        }
    }
    class DLL{
        Node head;
        Node tail;
        DLL(){
            head = new Node(-1,-1);
            tail = new Node(-1,-1);
            head.next = tail;
            tail.prev = head;
        }
        public boolean isEmpty(){
            return (head.next == tail);
        }
        public void addFront(Node cur){
            Node front = head.next;
            head.next = cur;
            cur.next = front;
            front.prev = cur;
            cur.prev = head;
        }
        public void addLast(Node cur){
            Node back = tail.prev;
            back.next = cur;
            cur.next = tail;
            tail.prev = cur;
            cur.prev = back;
        }
        public void remove(Node cur){
            Node back = cur.prev;
            Node front = cur.next;
            back.next = front;
            front.prev = back;
        }
    }
    HashMap<Integer,Node> keyNode;
    HashMap<Integer,DLL> freqList;
    int lfu;
    int capacity;
    public LFUCache(int capacity) {
        keyNode = new HashMap<>();
        freqList = new HashMap<>();
        lfu = 0;
        this.capacity = capacity;
    }
    private void LFUShift(Node cur){
        int oldFreq = cur.freq;
        DLL temp = freqList.get(oldFreq);
        temp.remove(cur);
        if(oldFreq == lfu && temp.isEmpty()){
            freqList.remove(lfu);
            lfu++;
        }   
        cur.freq++; 
        temp = freqList.getOrDefault(cur.freq,new DLL());
        temp.addFront(cur);
        freqList.put(cur.freq,temp);
    }
    public int get(int key) {
        if(keyNode.containsKey(key)){
            Node cur = keyNode.get(key);
            LFUShift(cur);
            return cur.val; 
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if(keyNode.containsKey(key)){
            Node cur = keyNode.get(key);
            LFUShift(cur);
            cur.val =value;
        }
        else{
            if(keyNode.size()==capacity){
                DLL temp = freqList.get(lfu);
                int keyToRemove = temp.tail.prev.key;
                temp.remove(temp.tail.prev);
                keyNode.remove(keyToRemove);
            }
            Node newNode = new Node(key,value);
            DLL temp = freqList.getOrDefault(1,new DLL());
            temp.addFront(newNode);
            keyNode.put(key,newNode);
            freqList.put(1,temp);
            lfu=1;
        }
    }
}

```