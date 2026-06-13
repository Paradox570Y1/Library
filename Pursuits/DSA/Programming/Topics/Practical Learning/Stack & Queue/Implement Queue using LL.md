
[Link](https://www.geeksforgeeks.org/problems/implement-queue-using-linked-list/1)

```java
class MyQueue
{
    QueueNode front, rear;
    
    //Function to push an element into the queue.
	void push(int a)
	{
        // Your code here
        if(front == null){
            front = new QueueNode(a);
            rear = front;
            return;
        }
        rear.next = new QueueNode(a);
        rear = rear.next;
	}
	
    //Function to pop front element from the queue.
	int pop()
	{
        // Your code here
        if(front == null)return -1; 
        QueueNode temp = front;
        front = front.next;
        temp.next = null;
        return temp.data;
	}
}

```