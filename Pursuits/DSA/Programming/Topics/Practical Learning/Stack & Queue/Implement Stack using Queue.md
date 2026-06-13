[Link](https://leetcode.com/problems/implement-stack-using-queues/description/)

```java
class MyStack {
    Queue<Integer> qi;
    public MyStack() {
        qi =new LinkedList<>();
    }
    
    public void push(int x) {
        qi.add(x);
    }
    private void reverse(Queue<Integer> qi){
        if(qi.size() ==0)return;
        int ele = qi.poll();
        reverse(qi);
        qi.add(ele);
        return;
    }
    public int pop() {
        reverse(qi);
        int ele = qi.poll();// or qi.remove()
        reverse(qi);
        return ele;
    }
    
    public int top() {
        reverse(qi);
        int ele = qi.peek();
        reverse(qi);
        return ele;
    }
    
    public boolean empty() {
        if(qi.size() == 0) return true;
        return false;
    }
}
```


Only push takes O(N)
```java
class MyStack {
    Queue<Integer> qi;
    public MyStack() {
        qi =new LinkedList<>();
    }
    
    public void push(int x) {
        qi.add(x);
        reverse(qi);
    }
    private void reverse(Queue<Integer> qi){
        for(int i=0;i<qi.size()-1;i++){
            qi.add(qi.poll());
        }
    }
    public int pop() {
        return qi.poll();
    }
    
    public int top() {
        return qi.peek();
    }
    
    public boolean empty() {
        if(qi.size() == 0) return true;
        return false;
    }
}
```