## 🧱 What is EBS?

**Amazon Elastic Block Store (EBS)** is a <mark style="background: #FFF3A3A6;">block-level storage </mark>service designed for use with **Amazon EC2 instances**. Think of it like a **virtual hard drive** that you attach to your EC2 instance.

---

## 📌 Key Features of EBS:

| Feature           | Description                                                                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Durable**       | Data is automatically replicated within its Availability Zone.                                                                              |
| **Persistent**    | Data <mark style="background: #FFF3A3A6;">persists</mark> even after the EC2 instance is stopped or terminated (unless deleted explicitly). |
| **Elastic**       | You can increase volume size, change type, or adjust IOPS without downtime.                                                                 |
| **Encrypted**     | Supports encryption at rest and in transit using AWS KMS.                                                                                   |
| **Snapshots**     | You can back up EBS volumes to S3 using snapshots.                                                                                          |
| **Attach/Detach** | Volumes can be attached or detached from EC2 instances dynamically (except root volumes).                                                   |

---

## 📂 EBS Volume Types:

|Type|Best For|Characteristics|
|---|---|---|
|**gp3**|General-purpose workloads|Default, balanced performance, scalable IOPS.|
|**gp2**|Legacy general-purpose|Performance scales with size.|
|**io2/io1**|High-performance workloads|Provisioned IOPS for databases, latency-sensitive apps.|
|**st1**|Big data, log processing|Throughput-optimized HDD.|
|**sc1**|Cold storage, infrequent access|Lowest-cost HDD, sequential access.|

---

## 🛠️ EBS vs Instance Store

|Feature|EBS|Instance Store|
|---|---|---|
|Persistent|✅ Yes|❌ No (data lost on stop/terminate)|
|Backup via snapshot|✅ Yes|❌ No|
|Can attach/detach|✅ Yes|❌ No (only during launch)|
|Use Case|General purpose|Temporary storage like cache, buffer|

---

## 🔗 Attaching EBS to EC2

1. **During EC2 Launch**:
    
    - Add volume via "Add Storage" tab.
        
2. **Post Launch**:
    
    - Go to **EC2 → Volumes** → Create volume.
        
    - Attach to running instance (must be in same AZ).
        
    - SSH into EC2 and mount it (format if new).
        

---

## 🧮 Common CLI Commands (AWS CLI)

bash

CopyEdit

`# Create EBS volume aws ec2 create-volume --availability-zone us-east-1a --size 10 --volume-type gp3  # Attach volume to EC2 aws ec2 attach-volume --volume-id vol-xxxxxxxx --instance-id i-xxxxxxxx --device /dev/xvdf  # Detach volume aws ec2 detach-volume --volume-id vol-xxxxxxxx  # Create snapshot aws ec2 create-snapshot --volume-id vol-xxxxxxxx --description "Backup"`

---

## 📊 Performance Metrics (for `gp3` as example):

- **Max IOPS**: 16,000
    
- **Max Throughput**: 1,000 MB/s
    
- **Baseline**: 3,000 IOPS (customizable)
    

---

## 🔐 EBS Encryption

- Uses **AWS KMS keys** (default or custom).
    
- Enables:
    
    - Encrypted data at rest
        
    - Encrypted snapshots
        
    - Encrypted volume copies
        

---

## 🔄 Snapshots and AMIs

- EBS snapshots stored in **S3** (managed, not directly accessible).
    
- Can **restore a snapshot** to create a new volume.
    
- Can create **AMIs from snapshots** for launching EC2 with pre-baked volumes.
    

---

## 📚 Real-World Use Cases

|Scenario|EBS Role|
|---|---|
|Hosting a database|Use `io2` for low-latency access|
|Web server storage|Use `gp3` for boot + web assets|
|Data warehouse / Big data|Use `st1` or `sc1` volumes|
|Backup/Recovery|Use snapshots regularly|

---

## ✅ Best Practices

- Use **gp3** unless you have specific performance needs.
    
- Regularly **create snapshots** for disaster recovery.
    
- Monitor using **CloudWatch metrics** (e.g., IOPS, queue depth).
    
- **Tag volumes** for cost tracking and management.
    
- **Detach and delete** unused volumes to avoid unnecessary charges.

---

### 1. What is EBS? (The High-Level Concept)

**EBS (Elastic Block Store)** is a high-performance, persistent **block storage service** designed for use with Amazon EC2 (Elastic Compute Cloud) instances.

Think of it as a **virtual, network-attached Hard Disk Drive (HDD) or Solid-State Drive (SSD)** that you can attach to your virtual server (EC2 instance). Just like you can plug a new hard drive into a physical computer, you can attach an EBS volume to an EC2 instance.

- **Persistent:** Unlike the local "instance store" disks that come with some EC2 instances, EBS storage persists independently of the life of an instance. If you terminate the EC2 instance, you can keep the EBS volume and attach it to another one.
    
- **Block Storage:** This is the key characteristic. It provides raw, unformatted block-level storage. This means the EC2 instance's operating system (e.g., Linux, Windows) sees it as a blank block device (e.g., `/dev/xvdf` on Linux). You must then create a filesystem (e.g., ext4, NTFS) on it, format it, and mount it to a directory before you can use it. This is in contrast to object storage (like S3) or file storage (like EFS).
    

---

### 2. Why Was EBS Needed?

Before EBS, the primary storage for EC2 instances was **ephemeral instance store**. This storage was physically attached to the host machine hosting the EC2 instance.

**The problems with instance store were:**

1. **Lack of Persistence:** If the instance failed, was stopped, or terminated, all data on the instance store was lost forever.
    
2. **Inflexibility:** You couldn't detach the storage from one instance and attach it to another. The storage was tied to the specific physical host.
    
3. **Limited Data Durability:** A hardware failure on the host could mean complete data loss.
    

**EBS was created to solve these critical issues:**

- **Data Persistence:** Decouple storage from compute. The life of the storage is independent of the life of the virtual server.
    
- **Flexibility:** Volumes can be dynamically attached, detached, and reattached to different EC2 instances in the same Availability Zone (AZ).
    
- **High Durability:** EBS volumes are automatically replicated within its Availability Zone, protecting against component failure.
    
- **Operational Benefits:** Enables use cases like:
    
    - **Boot Volumes:** You can stop an EC2 instance and later restart it, and your OS and all your installed software are still there.
        
    - **Database Storage:** Running databases like MySQL or PostgreSQL requires persistent, reliable block storage.
        
    - **Data Portability:** Moving data between instances for maintenance or scaling.
        

---

### 3. Low-Level Implementation (How It Works Under the Hood)

While AWS doesn't reveal its exact proprietary architecture, the general principles are based on well-known distributed systems concepts. Here's a simplified view of the low-level implementation:

**1. Architecture & Redundancy:**

- When you create an EBS volume in an Availability Zone (AZ), it is not a single physical disk.
    
- It is a **logical volume** striped across multiple physical disks in a storage backend cluster within that AZ.
    
- Each write operation to the volume is **synchronously replicated** across multiple servers (and thus multiple disks) in that cluster. This is typically done using a distributed replication protocol (like Paxos or Raft) to ensure consistency and durability.
    
- This replication protects against the failure of any single component (disk, server, rack).
    

**2. Network-Attached Storage (NAS):**

- The physical disks hosting your EBS volume are **not** in the same physical host as your EC2 instance.
    
- They reside in a separate, massive-scale storage cluster dedicated to EBS within the AZ.
    
- Your EC2 instance communicates with this storage cluster over a **high-speed, low-latency network** (AWS's internal network). This is why it's called "network-attached" block storage.
    
- The communication protocol is likely a optimized, proprietary version of a standard block protocol like iSCSI or NVMe over Fabrics (NVMe-oF).
    

**3. The I/O Path (Read/Write Operation):**  
1. Your EC2 instance sends a read or write request (e.g., "write block number 12345 with this data") to the OS.  
2. The OS's device driver sends this request over the network to the EBS backend cluster.  
3. The request is received by a **controller node** in the EBS cluster responsible for your volume.  
4. The controller writes the data to multiple storage nodes (replicas) and waits for acknowledgements to ensure durability.  
5. Once the write is confirmed on enough replicas, an acknowledgement is sent back to the EC2 instance.  
6. For a read, the controller fetches the requested block from one of the replicas and sends it back to the instance.

**4. Snapshots:**

- A snapshot is an **incremental, point-in-time copy** of your EBS volume, stored in the highly durable Amazon S3.
    
- The first snapshot is a full copy. Subsequent snapshots only save the blocks that have _changed_ since the last snapshot.
    
- This is highly efficient in terms of storage and time. When you delete a snapshot, only the data blocks unique to that snapshot are freed.
    

---

### 4. Pros and Cons of EBS

#### Pros:

- **High Durability:** Designed for 99.999% availability (for io2 Block Express) and 99.999% durability. Data is replicated within an AZ.
    
- **Persistence:** Data persists independently of instance state.
    
- **High Performance:** Offers a range of volume types (SSD, HDD) with tunable IOPS (I/O Operations Per Second) and throughput for different workloads.
    
- **Flexibility:** Volumes can be easily resized, have their performance tuned, and be attached/detached from running instances.
    
- **Snapshotting:** Easy and efficient backup mechanism (incremental snapshots to S3).
    
- **Encryption:** Native integration with AWS Key Management Service (KMS) for encryption at rest and in transit.
    

#### Cons:

- **Cost:** Adds an ongoing cost on top of the EC2 instance cost. Provisioned IOPS can become expensive.
    
- **Latency:** Being network-attached, it has higher latency than physically attached **instance store** volumes (though it's very low and sufficient for most use cases).
    
- **AZ-Bound:** A significant limitation. An EBS volume is locked to a specific Availability Zone. You cannot directly attach it to an instance in a different AZ. You must first create a snapshot, then create a new volume from that snapshot in the target AZ.
    
- **Performance Overhead:** The network stack and replication protocol introduce some overhead compared to a direct-attached disk.
    
- **Capacity Limits:** You are limited by AWS quotas on the number and total size of volumes per account and region.
    

### Summary Table: EBS vs. Instance Store

|Feature|EBS Volume|Instance Store (Ephemeral)|
|---|---|---|
|**Persistence**|**Persistent** (survives instance stop/terminate)|**Ephemeral** (lost on instance stop/terminate/failure)|
|**Attachment**|Network-attached (over AWS network)|Physically attached to the host server|
|**Durability**|Highly durable (replicated within AZ)|Not durable (tied to host health)|
|**Performance**|Very good, consistent, tunable|**Extremely high, very low latency** (best for temp data)|
|**Flexibility**|Can be detached and reattached|Cannot be detached; tied to instance life|
|**Use Case**|Boot volumes, databases, apps|Cache, buffers, temporary processing, read-only data|

In conclusion, EBS is the foundational persistent storage layer for stateful applications on AWS. Its network-attached, replicated architecture provides the perfect blend of persistence, performance, and flexibility that modern cloud workloads require, despite its minor trade-offs in absolute latency and cost compared to ephemeral storage.