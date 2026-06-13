```java
import java.util.*;
import java.lang.*;
class Solution{
    static class CommonCounter{
        int count;
        CommonCounter(){
            this.count = 0;
        }
        public synchronized void increment(){ // to prevent race condition
                this.count+=1;
        }
    }
    static class MyRunnable implements Runnable{
        CommonCounter resource;
        int n;
        MyRunnable(CommonCounter resource,int n){
            this.resource = resource;
            this.n = n;
        }
        @Override
        public void run(){
            for(int i=0;i<n;i++){
                resource.increment();
            }
        }
    }
    public static void main(String[] args) throws InterruptedException{
        CommonCounter resource = new CommonCounter();
        Thread thread1 = new Thread(new MyRunnable(resource,1000000));
        Thread thread2 = new Thread(new MyRunnable(resource,1000000));
        thread1.start();
        thread2.start();
        thread1.join();
        thread2.join();
        System.out.println(resource.count);
    }
    
}
```

Following are the ways to prevent Race Condition:
- Using `synchronized` keyword in the method where race condition can occur.
- Using Atomic Integer.
- Using [[tryLock() Method]]
```java
import java.util.*;
import java.lang.*;
import java.util.concurrent.locks.ReentrantLock;
class Solution{
    static class CommonCounter{
        public int count;
        public ReentrantLock lock;
        CommonCounter(){
            this.count = 0;
            this.lock = new ReentrantLock();
        }
        public  void increment(int n){
                while (!lock.tryLock()){}
                this.count+=1;
                lock.unlock();
        }
    }
    static class MyRunnable implements Runnable{
        CommonCounter resource;
        int n;
        MyRunnable(CommonCounter resource,int n){
            this.resource = resource;
            this.n = n;
        }
        @Override
        public void run(){
            for(int i=0;i<n;i++){
                resource.increment(i);
            }
        }
    }
    public static void main(String[] args) throws InterruptedException{
        CommonCounter resource = new CommonCounter();
        Thread thread1 = new Thread(new MyRunnable(resource,1000000));
        Thread thread2 = new Thread(new MyRunnable(resource,1000000));
        thread1.start();
        thread2.start();
        thread1.join();
        thread2.join();
        System.out.println(resource.count);
    }
    
}
```

- Using `AtomicInteger` class

```java
import java.util.*;
import java.lang.*;
import java.util.concurrent.atomic.AtomicInteger;
class Solution{
    static class CommonCounter{
        public AtomicInteger count;
        CommonCounter(){
            this.count = new AtomicInteger(0);;
        }
        public  void increment(int n){
                this.count.incrementAndGet();
        }
    }
    static class MyRunnable implements Runnable{
        CommonCounter resource;
        int n;
        MyRunnable(CommonCounter resource,int n){
            this.resource = resource;
            this.n = n;
        }
        @Override
        public void run(){
            for(int i=0;i<n;i++){
                resource.increment(i);
            }
        }
    }
    public static void main(String[] args) throws InterruptedException{
        CommonCounter resource = new CommonCounter();
        Thread thread1 = new Thread(new MyRunnable(resource,1000000));
        Thread thread2 = new Thread(new MyRunnable(resource,1000000));
        thread1.start();
        thread2.start();
        thread1.join();
        thread2.join();
        System.out.println(resource.count);
    }
    
}
```