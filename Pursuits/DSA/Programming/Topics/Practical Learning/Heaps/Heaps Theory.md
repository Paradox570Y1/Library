> [Resources](https://github.com/kunal-kushwaha/DSA-Bootcamp-Java/blob/main/lectures/24-heaps/notes/Heaps%20-%201.pdf)
# Why we need Heap?
-> To get the item in constant time while ensuring that inserting the element takes only O(log n).
- If we do it without heaps then we will be sorting the array each time while inserting new element , although we can get element in O(1) but putting that in array will take at minimum O(n logn) in case of merge sort or quick sort.
![[Pasted image 20250301200843.png]]


# Understanding Structure of Heap

- Heap is stored in the form of array internally but it will be represented as a tree.
- To be specific it will be represented as complete binary tree.
- Types
	- `Max Heap :`Gives maximum item in constant time.
	- `Min Heap :`Gives minimum item in constant time.
- In case of `Max heap`
	- Every node value is >=  All of its children
- For simplicity we are taking smallest index as 1 which is also the root of the tree.
- Index of parent of a node is half of its own index.
- Index of left children of a node is 2\*i.  (where i=index of node)
- Index of right children of a node is 2\*i+1.  (where i=index of node)
-  Height of tree is `log n`.

- For 0 based indexing
	- index of parent node will be (i-1)/2.
	- index of left child of parent is 2\*i+1.
	- index of right child of parent is  2\*i+2.
![[Pasted image 20250301200915.png]]


# Inserting element in Heap

To insert an element we only need to swap it with its parent so at max we have to swap log n times to  climb to the root of the tree.
![[Pasted image 20250301224223.png]]

# Removing an element

- To remove the element take the last element in the array or we can say largest element in case of min heap and place it at the root .
- Now compare left and right child of root , and if smaller child is smaller than the root then swap and then continue to check it down in the tree until the both child are bigger than the swapped node.
- It also takes O(log n)


# Convert minheap to maxheap

- Although it looks like iterating N/2 times and calling `downheap`  function which takes log n times will make the time complexity `N log N `times but that is not true.
- Actual time complexity turn out to be `O(N)`.

![[Pasted image 20250301232127.png]]

![[Pasted image 20250301232935.png]]

![[Pasted image 20250301233014.png]]
![[Pasted image 20250301233026.png|400]]
So it becomes constant and hence time complexity is
![[Pasted image 20250301233054.png|300]]



Implementation
```java
import java.util.ArrayList;
class Main{
    public static void main(String[] args) throws Exception{
        Heap<Integer> heap = new Heap<>();
        heap.insert(5);
        heap.insert(12);
        heap.insert(1);
        heap.insert(6);
        heap.remove();
        System.out.println(heap.heapSort());
    }
}
class Heap<T extends Comparable<T>>{
    private ArrayList<T> list;
    Heap(){
        list = new ArrayList<>();
    }
    private void swap(int first,int second){
        T temp  = list.get(first);
        list.set(first,list.get(second));
        list.set(second,temp);
    }
    private int parent(int i){
        return (i-1)/2;
    }
    private int left(int i){
        return 2*i+1;
    }
    private int right(int i){
        return 2*i+2;
    }
    public void insert(T data){
        list.add(data);
        upheap(list.size()-1);
    }
    private void upheap(int i){
        if(i==0)return;
        int parent = parent(i);
        if(list.get(i).compareTo(list.get(parent))<0){
            swap(i,parent);
            upheap(parent);
        }
    }
    public T remove() throws Exception{
        if(list.isEmpty()){
            throw new Exception("Trying to remove element from empty list!");
        }
        T temp = list.get(0);
        //to balance the tree
        T last = list.remove(list.size()-1);
        if(!list.isEmpty()){
            list.set(0,last);
            downheap(0);
        }
        return temp;
    }
    private void downheap(int index){
        int min = index;
        int left = left(min);
        int right = right(min);
        if(left<list.size() && list.get(left).compareTo(list.get(min))<0)min = left;
        if(right<list.size() && list.get(right).compareTo(list.get(min))<0)min = right;
        if(min!=index){
            swap(min,index);
            downheap(min);
        }
    }
    public ArrayList<T> heapSort() throws Exception{
        ArrayList<T> temp = new ArrayList<>();
        while(!list.isEmpty()){
            temp.add(this.remove());
        }
        return temp;
    }
}

```



```java
import java.util.List;
import java.util.ArrayList;
class Main {
    public static void main(String[] args) throws Exception {
        Heap<Integer> heap = new Heap<>();
        heap.insert(4);
        heap.insert(1);
        heap.insert(18);
        heap.insert(12);
        heap.insert(5);
        System.out.println(heap.heapSort());
    }
}
class Heap<T extends Comparable<T>>{
    private T[] arr;
    private int s;
    @SuppressWarnings("unchecked")
    Heap(){
        arr = (T[]) new Comparable[1001];
        s=0;
    }
    private int parent(int index){
        return (index-1)/2;
    }
    private int left(int index){
        return index*2+1;
    }
    private int right(int index){
        return index*2+2;
    }
    public void insert(T val){
        arr[s++] = val;
        upheap(s-1);
    }
    private void swap(int first,int second){
        T temp = arr[first];
        arr[first] = arr[second];
        arr[second] = temp;
    }
    private void upheap(int index){
        if(index==0)return;
        int parent = parent(index);
        if(arr[index].compareTo(arr[parent])>0){
            swap(index,parent);
            upheap(parent);
        }
    }
    public T remove() throws Exception{
        if(s==0){
            throw new Exception("You are trying to remove element from empty heap!");
        }
        T root = arr[0];
        arr[0] = arr[s-1];
        s--;
        downheap(0);
        return root;
    }
    private void downheap(int index) throws Exception{
        int left = left(index);
        int right = right(index);
        int min = index;
        if(left<s && arr[left].compareTo(arr[min])>0)min = left;
        if(right<s && arr[right].compareTo(arr[min])>0)min = right;
        if(min!=index){
            swap(min,index);
            downheap(min);
        }
    }
    public int size(){
        return s;
    }
    public List<T> heapSort() throws Exception{
        List<T> sortedList = new ArrayList<>();
        int size = s;
        for(int i=0;i<size;i++){
            sortedList.add(this.remove());
        }
        return sortedList;
    }
}

```

```java
class Main {
    public static void main(String[] args) throws Exception {
        Heap<String> heap = new Heap<>();
        heap.insert("apurav");
        heap.insert("aman");
        heap.insert("cat");
        heap.insert("boxer");
        heap.insert("bad");
        System.out.println(heap.heapSort());
    }
}
```
![[Pasted image 20250302105824.png|300]]
