- Amazon SQS and Kafka , Online Cloud Solution uses this message queue in their original code.

https://docs.google.com/document/d/1wI-h2CwsAn1F-GPqzREiDUj1zib7HBUnonTVrg8-SJI/edit?tab=t.0
```java
import java.util.*;
import java.lang.*;
import java.io.*;


class Message {
    public String msg;
    public int timeStamp;
    public boolean shouldPrintMessage;
    public Message(String msg, int timeStamp) {
        this.msg = msg;
        this.timeStamp = timeStamp;
        this.shouldPrintMessage = true;
    }
}

interface MessageTracker {
    Message getMessage();    
}

class RobotTracker
{
    MessageTracker messageTracker;
    Map<String,Message> messageTimeStamp;
    Queue<Message> q;
    public RobotTracker(MessageTracker messageTracker) {
        this.messageTracker = messageTracker;
        this.messageTimeStamp = new HashMap<>();
        q = new LinkedList<>();
    }
    
    public void pollMessage() {
        while (true) {
            Message message = messageTracker.getMessage();
            shouldPrintMessage(message);
        }
    }
    /*
    
        [1, "Hello"] , [2, "Hello"], [8, "Bye"], [12, "Hello"], [13, "Bye"]
        Answer is : [1, "Hello"], [8, "Bye"], [12, "Hello"]
    */
    private printTillTimeStamp(int threshold){
        while(!q.isEmpty() && q.peek().timeStamp <= threshold){
            Message printMessage = q.poll();
            System.out.println
        }
    }
    public void shouldPrintMessage(Message message) {
        // Add your implementation here
        if(messageTimeStamp.containsKey(message.msg)){
            Message olderMessage = messageTimeStamp.get(message.msg);
            if(message.timeStamp -olderMessage.timeStamp < 10){
                olderMessage.shouldPrintMessage = false;
                message.shouldPrintMessage = false;
            }
        }
        q.offer(message);
        messageTimeStamp.put(message.msg,message);
        printTillTimeStamp(message.timeStamp-10);
    }
    
    public static void main(String args[]) {
        RobotTracker robotTracker = new RobotTracker(null);
        robotTracker.shouldPrintMessage(new Message("hello" , 1)); // print this
        robotTracker.shouldPrintMessage(new Message("hello" , 2));
        robotTracker.shouldPrintMessage(new Message("bye" , 8)); //print this
        robotTracker.shouldPrintMessage(new Message("yoo" , 10)); //print this
        robotTracker.shouldPrintMessage(new Message("hello" , 12)); //print this
        robotTracker.shouldPrintMessage(new Message("bye" , 13));
        robotTracker.shouldPrintMessage(new Message("bye" , 24)); //print this
    }
}


```