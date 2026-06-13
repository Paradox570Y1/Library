[Link](https://leetcode.com/problems/implement-queue-using-stacks/description/)

```java
class MyQueue {
    Stack<Integer> st;
    public MyQueue() {
        st = new Stack();
    }
    
    public void push(int x) {
        if(st.size() == 0){
            st.push(x);
            return;
        }
        int temp = st.pop();
        push(x);
        st.push(temp);
    }
    
    public int pop() {
        return st.pop();
    }
    
    public int peek() {
        return st.peek();
    }
    
    public boolean empty() {
        return st.isEmpty();
    }
}
```