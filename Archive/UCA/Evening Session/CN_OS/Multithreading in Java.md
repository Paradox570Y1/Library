
%% Email => rohit@kaksha.dev %%

[Resources](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html)
- Java has its own library for multi-threading. 
- In **Java**, to use **threads**, you do **not need to import any external package manually** — everything you need is already part of the **`java.lang`** package, which is **automatically imported** by default in every Java program. you can use `Thread`, `Runnable`, and related classes **directly** without writing any import statement.
![[Pasted image 20251110130340.png|200]]
```java
public class Thread
extends Object
implements Runnable
```
- In Multithreaded environment , you can't expect ordered execution , CPU is going to execute threads by it's own accord unless Priority of threads is specified by the programmer.
- A _thread_ is a thread of execution in a program. The Java Virtual Machine allows an application to have multiple threads of execution running concurrently.
-  Each thread may or may not also be marked as a [[Daemon]].
- The **Java Virtual Machine (JVM)** will **automatically stop running** once **all user threads** are done executing **even if some other threads (daemon threads) are still running**.
- [[Every thread has a name for identification purposes]]. More than one thread may have the same name. If a name is not specified when a thread is created, a new name is generated for it. Unless otherwise noted, passing a `null` argument to a constructor or method in this class will cause a [`NullPointerException`](https://docs.oracle.com/javase/8/docs/api/java/lang/NullPointerException.html "class in java.lang") to be thrown since JDK 1.0.
- To get Thread Name
	`Thread.currentThread().getName()` - to get the name of current thread within it's scope of execution
	`thread_obj.getName()` - to get the name of given thread obj
- To invoke the thread
	`thread_name.start()`
	- It creates a parallel environment for the thread to execute and then invoke `.run()` method to actually execute the thread code.
	- You can never start a single thread 2 times.
- Each thread may or may not also be marked as a daemon. When code running in some thread creates a new `Thread` object, the new thread has its priority initially set equal to the priority of the creating thread, and is a daemon thread if and only if the creating thread is a daemon.
- When a Java Virtual Machine starts up, there is usually a single non-daemon thread (which typically calls the method named `main` of some designated class). The Java Virtual Machine continues to execute threads until either of the following occurs:
	- The `exit` method of class `Runtime` has been called and the security manager has permitted the exit operation to take place.
	- All threads that are not daemon threads have died, either by returning from the call to the `run` method or by throwing an exception that propagates beyond the `run` method.

- To give a custom name to thread
	`thread_name.setName("new_name")`
	- We can also set name while creating a new thread in case we are passing runnable object
		![[Pasted image 20250810192229.png]]
		
- To Just implement the functionality of thread without parallel execution.
	`thread_name.run()`
	- It happens synchronously
	- Kind of like a function
	- It can be used to test the implementation of the thread , you could just see how will it work or how it will execute when invoked in multi threading environment.
	- It shows what the code execution will look like.
	- But you can run a single thread multiple times.

```java
public class Main {
    public static void main(String[] args){
        System.out.println();
        Thread t1 = new Thread(()->{
            System.out.println(Thread.currentThread().getName());
        });
        t1.setName("Apurav");
        t1.setPriority(10); //(1-> min priority ,, 10->highest priority)
        t1.start();
        System.out.println(Thread.currentThread().getName());
    }
}

```
![[Pasted image 20251110161642.png|350]]


# Why threading
![[Pasted image 20250810174339.png|400]]

# Observations

[Resources](https://docs.google.com/document/d/1xuyBrNHEZdLGk5KgOmhZdAUtHfq-bo5mo-pruaxFoLg/edit?tab=t.0)

```java
public class Main {
    public static void main(String[] args){
        Thread t1 = new Thread(()->{
            for(int i=0;i<26;i++){
                System.out.println(i);
            }

            System.out.println(Thread.currentThread().getName());
        });
        
        t1.start();
        for(char ch = 'a';ch<='z';ch++){
            System.out.println(ch);
        }
        System.out.println(Thread.currentThread().getName());
    }
}
```

Ways of execution
- Way 1: Using Thread class
[[Execution1]]

```java
public class Main {
    public static void main(String[] args){
        Thread t1 = new Thread(()->{
            for(int i=0;i<26;i++){
                System.out.println(i);
            }
            System.out.println(Thread.currentThread().getName());
        });
        
        t1.run();
        for(char ch = 'a';ch<='z';ch++){
            System.out.println(ch);
        }
        System.out.println(Thread.currentThread().getName());
    }
}
```

[[Execution2]]

- Way 2: Extending Thread Class in another class
![[Pasted image 20250721203022.png|400]]

- Way 3: Implementing Runnable interface and passing it's object to create Thread object.

# State of Thread Cycle

NEW -> Running -> BLOCKED -> TERMINATE
NEW -> Runnable -> Running/Blocked -> TERMINATE
- You can never start a single thread 2 times.
	![[Pasted image 20250721205452.png|400]]
- But you can run a single thread multiple times.
	![[Pasted image 20250721205543.png|400]]


# Interface
- It defines the rules of Randhawa family if you want to be it's member.
- So just define what functionality the child class must have if that class 



# Three ways to implement a thread

- Directly use lambda expression in thread.
- Extend thread class to override it's implementation or create new implementations
- Create your own runnable(script) and provide that runnable obj to thread(actor) to implement.
	- You want to execute this although you doesn't belong to the thread class.
	- We use runnable as it's easy to read then using an anonymous function.

[[Implementing Threads by extending Thread class]]
[[Implementing Threads by implementing Runnable Interface]]
[[Thread Naming, Priority and Sleep]]
[[Detailed explanation on sleep]]
[[Thread Pools in JAVA]]
[[UUID in JAVA]]
Sir's example
![[Pasted image 20250721210004.png|400]]

# States in Threads
If you're studying **Java**, threads actually have **6 official states**:

1. **NEW**
2. **RUNNABLE**
3. **BLOCKED**
4. **WAITING**
5. **TIMED_WAITING**
6. **TERMINATED**

Java splits "waiting" into 3 categories (BLOCKED, WAITING, TIMED_WAITING), so it becomes 6 instead of 4.
[[States of Threads in JAVA]]

---
**Problem Statement 1**
Implement MinMaxStack

```java
import java.lang.*;
import java.io.*;
import java.util.Stack;
class MinMaxStack {
    class Element{
        int max;
        int min;
        int cur;
        Element(int cur,int min,int max){
            this.cur = cur;
            this.min = min;
            this.max = max;
        }
    }
    Stack<Element> st;
    public MinMaxStack() {
        st = new Stack<>();
    }
    
    public void push(int val) {
        if(st.isEmpty()){
            st.push(new Element(val,val,val));
            return;
        }
        st.push(new Element(val,Math.min(st.peek().min,val),Math.max(st.peek().max,val)));
    }
    
    public void pop() {
        if(!st.isEmpty())st.pop();
    }
    
    public int top() {
        if(!st.isEmpty())return st.peek().cur;
        else return -1;
    }
    
    public int getMin() {
        if(!st.isEmpty())return st.peek().min;
        else return -1;
    }
    
    public int getMax() {
        if(!st.isEmpty())return st.peek().max;
        else return -1;
    }
    public static void main(String[] args) {
      MinMaxStack stack = new MinMaxStack();
      stack.push(3);
      stack.push(12);
      stack.push(2);
      stack.push(5);
      assert(stack.top() == 5);
      assert(stack.getMin() == 2);
      assert(stack.getMax() == 12);
    }
}
```


- `thread_name.join()`
	- It is used to make sure that after thread completes it's execution then it will get merged into the main branch
	- Since it interrupts the main thread therefore there is a chance that main thread might not execute hence it should throw some kind of exception
	- So use `throws InterruptedException`
	- join is important to ensure that thread completes it's execution before you use it's result.
	 ![[Pasted image 20251116121018.png|200]]
[[Locks in Detail]]

[[Reentrant lock]]
[[wait and notify]]
[[Semaphores]]
HW -> Implement Race condition problem using Semaphores by allotting only one thread to it.
Ans: Make use of Binary Semaphore by just permitting only one entry.
```java
import java.util.concurrent.Semaphore;

class Solution {
    static class CommonCounter {
        int count;
        Semaphore semaphore; // Controls access

        CommonCounter() {
            this.count = 0;
            this.semaphore = new Semaphore(1); // 1 permit → like a mutex
        }

        public void increment() {
            try {
                semaphore.acquire(); // Wait for permit
                this.count += 1;
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            } finally {
                semaphore.release(); // Release permit
            }
        }
    }

    static class MyRunnable implements Runnable {
        CommonCounter resource;
        int n;

        MyRunnable(CommonCounter resource, int n) {
            this.resource = resource;
            this.n = n;
        }

        @Override
        public void run() {
            for (int i = 0; i < n; i++) {
                resource.increment();
            }
        }
    }

    public static void main(String[] args) throws InterruptedException {
        CommonCounter resource = new CommonCounter();
        
        Thread thread1 = new Thread(new MyRunnable(resource, 1000000));
        Thread thread2 = new Thread(new MyRunnable(resource, 1000000));
        
        thread1.start();
        thread2.start();
        
        thread1.join();
        thread2.join();
        
        System.out.println("Final count: " + resource.count);
    }
}

```

---
**[[Problem Statement 2a]]**

Implement the `shouldPrintMessage(Message message)` method such that:
1. Each `Message` has a **timestamp** (integer, seconds) and **text** (string).
2. A message should be **printed** if either:
    - It has not been printed before, OR
    - The last time it was printed was **at least 10 seconds ago**.
3. If a message is received within 10 seconds of its last print, ignore it.
4. Return only the messages that should be printed in the same format as the example.

```java
Q: [1, "Hello"], [2, "Hello"], [8, "Bye"], [12, "Hello"], [13, "Bye"]
Ans: [1, "Hello"], [8, "Bye"], [12, "Hello"]
```

> NOTE 
> In above question message is printed based on last printed message  not based on last message arrived , both are different things as all arrived message is not necessarily printed thereby map should be implemented based on last printed message rather than last arrived


**[[Problem Statement 2b]]**  
You are given a stream of messages in the form:
Write a program to print only those messages that satisfy the following condition:

- The same message **did not occur within the last 10 seconds** (before this timestamp).
    
- The same message **will not occur within the next 10 seconds** (after this timestamp).


--- 
---
# Transport Layer

- Here in terms of Network Protocol , Protocol means in what format data is sent , what is the sequence and what kind of congestion control is implemented .
- Two main Protocols:
	- TCP (Transmission Control Protocol)
		- Here we are making sure nothing is lost.
		- Used on Transport Layer.
		- We need HTTP to send data in format of HTML which can be displayed on browser. HTTP use TCP bcz all packets of data is important otherwise this could result in error. Sometimes there is lag in loading some section of the page that is because it doesn't occur in one go.
		- It is connection oriented because we have a three way handshake for each packet, this packet is marked with this sequence and there are n numbers of packets.
	- UDP (User Datagram Protocol)
		- It keeps on sending data and keep on displaying the data.
		- Example : Video call , LIVE videos, DNS
		- It's like we are talking to a socket and that thread is alive it keeps sending data.
		- It doesn't worry about sequencing , duplicating therefore  it's a light weight protocol.

- There is nothing bad and good in algo or network protocol it just depends on use case.
- `ps aux` command to check which internal port number is used
- Port
	- port has a queue.
	- When we accept a request then it picks request and put it in queue
---
GPT

## **1. What is TCP in Java?**

- TCP (Transmission Control Protocol) is like **a telephone call** between two computers:
    - Before talking, both sides connect.
    - Messages are delivered in order and reliably.
- In Java, TCP communication is done using
    - **`ServerSocket`** → for the _server_ side (the listener/waiter).
    - **`Socket`** → for the _client_ side (the one that connects).

---

## **2. How it works**

Think of it like a shop:

1. **Server Socket** is like the shop door — always waiting for customers.
2. **Client Socket** is like a person walking into the shop to buy something.
3. Once connected:
    - They can talk back and forth using **InputStream** (read) and **OutputStream** (write).
4. When the conversation is done, both close their sockets.


---
- In linux make use of netstat
- use `nc` to create a client with creating EchoClient.java
![[Pasted image 20250811202450.png]]

- HW implement same with Datagram protocol.

```java
import java.util.*;
import java.lang.*;
import java.io.*;

class Codechef
{
	public static void main (String[] args) throws java.lang.Exception {
		
        ProductTracker pt = new ProductTracker();
		pt.wishlit("a");
		pt.wishlit("a");
		pt.wishlit("a");
		
		pt.wishlit("b");
		pt.wishlit("b");
		
		System.out.println("MAX : " + pt.getMaxProduct());
		System.out.println("MIN : " + pt.getMinProduct());
		
		pt.delist("a");
		pt.delist("a");
		System.out.println("MAX : " + pt.getMaxProduct());
		System.out.println("MIN : "  + pt.getMinProduct());
		
		pt.delist("a");
		pt.delist("a");
		
		System.out.println("MAX : " + pt.getMaxProduct());
		System.out.println("MIN : " + pt.getMinProduct());
		
	}
}

class ProductTracker {

    Map<String, Integer> productCounter;
    
    public ProductTracker() {
        productCounter = new HashMap<>();
    }
    
    public void wishlit(String productName) {
        productCounter.merge(productName, 1, Integer::sum);
    }
    
    public void delist(String productName) {
        
        if (productCounter.containsKey(productName)) {
            int currCount = productCounter.merge(productName, -1, Integer::sum);
            if (currCount == 0) {
                productCounter.remove(productName);
            }
        }
    }
    
    public String getMaxProduct() {
        String maxKey = "";
        int maxCount = -1;
        for (Map.Entry<String, Integer> entry : productCounter.entrySet()) {
            if (maxCount < entry.getValue()) {
                maxCount = entry.getValue();
                maxKey = entry.getKey();
            }
        }
        
        return maxKey;
    }
    
    public String getMinProduct() {
        String minKey = "";
        int minCount = Integer.MAX_VALUE;
        for (Map.Entry<String, Integer> entry : productCounter.entrySet()) {
            if (minCount > entry.getValue()) {
                minCount = entry.getValue();
                minKey = entry.getKey();
            }
        }
        
        return minKey;
    }
}
```

![[Pasted image 20250818203559.png]]


```java
import java.util.*;
import java.lang.*;
import java.io.*;

class Codechef
{
	public static void main (String[] args) throws java.lang.Exception
	{
		// your code goes here
		ProductTracker obj = new ProductTracker();
        obj.wishlist("a");
        obj.wishlist("a");
        obj.wishlist("a");
        obj.wishlist("b");
        obj.wishlist("b");
        System.out.println("Max Element " + obj.getMaxProduct());
        System.out.println("Min Element " + obj.getMinProduct());
        obj.delist("a");
        obj.delist("a");
        System.out.println("Max Element " + obj.getMaxProduct());
        System.out.println("Min Element " + obj.getMinProduct());
        obj.delist("a");
        obj.delist("a");
        System.out.println("Max Element " + obj.getMaxProduct());
        System.out.println("Min Element " + obj.getMinProduct());
	}
}

class ProductTracker {
    PriorityQueue<String> minHeap;
    PriorityQueue<String> maxHeap;
    HashMap<String,Integer> product_list;
    public ProductTracker() {
        product_list = new HashMap<>();
        minHeap = new PriorityQueue((a,b) -> product_list.get(a) - product_list.get(b));
        maxHeap = new PriorityQueue((a,b) -> product_list.get(b) - product_list.get(a));
    }
    
    public void wishlist(String productName) {
        if(!product_list.containsKey(productName)) {
            product_list.put(productName,1);
            minHeap.offer(productName);
            maxHeap.offer(productName);
        } else {
            product_list.put(productName,product_list.get(productName) + 1);
            minHeap.remove(productName);
            maxHeap.remove(productName);
            minHeap.offer(productName);
            maxHeap.offer(productName);
        }
    }
    
    public void delist(String productName) {
        if(product_list.containsKey(productName)){
            int val = product_list.get(productName);
            minHeap.remove(productName);
            maxHeap.remove(productName);
            if(val == 0) product_list.remove(productName);
            else{
                product_list.put(productName,val-1);
                minHeap.offer(productName);
                maxHeap.offer(productName);
            }
        }
    }
    
    public String getMaxProduct() {
        return maxHeap.peek();
    }
    
    public String getMinProduct() {
        return minHeap.peek();
    }
}
```


