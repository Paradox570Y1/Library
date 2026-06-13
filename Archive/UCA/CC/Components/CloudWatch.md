Great! Let’s now explore **Amazon CloudWatch**, another key AWS service. It plays a vital role in **monitoring** and **observability** in cloud computing.

---

## 🔷 **Amazon CloudWatch**

### 🔹 What is Amazon CloudWatch?

Amazon CloudWatch is a **monitoring and observability service** that helps you collect, visualize, and act on metrics, logs, and events from AWS resources, applications, and services in real-time.

> ✅ **Think of it as the "eyes and ears" of your AWS infrastructure.**

---

### 🔹 Why Use CloudWatch?

- Monitor **EC2 instance CPU, memory, network, etc.**
    
- Track **API calls and resource usage**
    
- Automatically **trigger alerts** (e.g., send an email or restart an instance)
    
- View **dashboards** with real-time and historical metrics
    
- Detect and respond to system-wide **performance changes**
    

---

### 🔹 Core Components of CloudWatch

|Component|Description|Example|
|---|---|---|
|**Metrics**|Time-ordered numerical data (e.g., CPUUtilization, NetworkIn)|`CPUUtilization: 85%`|
|**Logs**|Aggregated logs from applications and AWS services|EC2 syslogs, Lambda output|
|**Alarms**|Conditions that trigger actions based on thresholds|Alert if disk usage > 90%|
|**Events**|Event-based triggers for system changes|Auto-restart EC2 if it fails|
|**Dashboards**|Visual interface to view metrics and logs|Custom view of all services|

---

### 📊 **How CloudWatch Works (Simplified)**

lua

CopyEdit

`[AWS Resources: EC2, Lambda, RDS, S3, etc.]           |       +---v---+       | Logs  |       | Metrics|       +---+---+           |    +------v------+    | CloudWatch  |    +-------------+    | Alarms      |    | Dashboards  |    | Events      |    +-------------+           | [Auto Actions / Email Alerts / Visualizations]`

---

### 🔹 Real-World Use Cases

1. **EC2 Monitoring:**  
    Track CPU usage, memory, and disk space.  
    🔔 Trigger alarm if CPU > 80% for 5 minutes.
    
2. **Lambda Debugging:**  
    Store logs from each function execution for debugging.
    
3. **S3 File Events:**  
    Notify via SNS when new files are uploaded to a bucket.
    
4. **Custom Applications:**  
    Publish your own metrics using AWS SDKs (e.g., requests/sec, app errors).
    

---

### 🔹 Common Metrics

|AWS Service|Metric Example|
|---|---|
|EC2|CPUUtilization, DiskReadOps|
|RDS|DatabaseConnections, FreeStorageSpace|
|Lambda|Invocations, Duration, Errors|
|ELB|RequestCount, Latency|
|S3|BucketSizeBytes, NumberOfObjects|

---

### 🔹 Setting Up an Alarm (Example)

1. Go to **CloudWatch Console**
    
2. Choose **Alarms > Create Alarm**
    
3. Select a metric (e.g., `EC2 > CPUUtilization`)
    
4. Set condition (e.g., `Greater than 80% for 5 mins`)
    
5. Add action (e.g., **SNS Email Notification** or **Auto-scaling**)
    

---

### 🔐 Integration with IAM

Use **IAM roles** and policies to restrict who can:

- View dashboards
    
- Edit alarms
    
- Access specific logs
    

---

## 📘 Suggested Resources

- AWS Docs: [https://docs.aws.amazon.com/cloudwatch/](https://docs.aws.amazon.com/cloudwatch/)
    
- Lab: [Free Hands-On with CloudWatch (Qwiklabs)](https://www.qwiklabs.com/)
    
- YouTube: ["Amazon CloudWatch Explained" by AWS](https://www.youtube.com/watch?v=jXSHU_uA2wU)