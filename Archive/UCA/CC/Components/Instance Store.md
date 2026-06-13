## ⚡ What is Instance Store?

**Instance Store**, also known as **ephemeral storage**, is **temporary block-level storage** physically attached to the **host machine** of an EC2 instance. Unlike EBS, it is **not persistent**—data is **lost** if the instance is stopped, hibernated, or terminated.

---

## 📌 Key Characteristics:

|Feature|Details|
|---|---|
|**Location**|Storage is **physically attached** to the underlying hardware.|
|**Persistence**|❌ **Temporary** – data is lost on instance stop, termination, or failure.|
|**Performance**|✅ Very **high IOPS & low latency**, because it bypasses the network.|
|**Cost**|Included **free** with specific EC2 instance types (e.g., `c3`, `i3`, `d2`).|
|**Durability**|❌ Not durable – meant for **scratch space, cache, buffer** only.|
|**Encryption**|No built-in encryption. Must encrypt manually if needed.|
|**Snapshots**|❌ Cannot create snapshots (unlike EBS).|

---

## 📂 Typical Use Cases

|Use Case|Description|
|---|---|
|**Buffer/cache**|Temporary data that can be recomputed or re-downloaded.|
|**Scratch disk**|During processing like sorting, temporary computation.|
|**Swap space**|For virtual memory or OS-level temporary storage.|
|**High-speed logs**|Data that needs fast I/O but not long-term storage.|

---

## 🧪 When Instance Store is Provisioned?

- You get it **only when launching certain EC2 instance types** that support it.
    
- It's **automatically attached**, and often appears as `/dev/xvdb`, `/dev/nvme1n1`, etc.
    
- You must **format and mount** it manually after instance boot.
    

---

## 🛠️ Instance Store vs EBS

|Feature|Instance Store|EBS|
|---|---|---|
|**Data Persistence**|❌ Lost on stop/terminate|✅ Persistent|
|**Attach/Detach**|❌ Only during launch|✅ Any time|
|**Backups**|❌ No snapshots|✅ Snapshots supported|
|**Performance**|✅ Extremely fast|✅ Fast, but network-bound|
|**Availability**|❌ Only certain instance types|✅ Almost all EC2 types|
|**Encryption**|❌ Manual|✅ Built-in|
|**Cost**|✅ Free (bundled)|💲 Charged separately|

---

## 🧮 How to Check for Instance Store (AWS Console):

1. When launching an instance, in the **“Instance type”** selection, check for:
    
    - “Instance storage” column (e.g., `i3.large` shows `1 x 475 NVMe SSD`)
        
2. In **“Add Storage”**, you’ll see `ephemeral0`, `ephemeral1`, etc.
    

---

## 🔧 Linux Commands to Use Instance Store

bash

CopyEdit

`# View all attached storage devices lsblk  # Format instance store (e.g., /dev/nvme1n1) sudo mkfs -t ext4 /dev/nvme1n1  # Create mount point sudo mkdir /mnt/instance-store  # Mount it sudo mount /dev/nvme1n1 /mnt/instance-store  # Optional: Add to /etc/fstab for auto-mount on reboot (won't help if instance is stopped!)`

---

## 🧊 Cold Start Warning

If the EC2 instance is stopped or terminated:

- **All data in instance store is lost.**
    
- **Reboots do NOT wipe data**, but you still shouldn't rely on that for critical storage.
    

---

## ✅ Best Practices

- **Never store important data** in instance store.
    
- Use it only for **temporary files**, logs, cache, etc.
    
- **Copy critical results** to EBS, S3, or a database as soon as possible.
    
- Don’t forget to **mount it manually** after instance launch.
    

---

## 🧠 Good to Know

- **Some EC2 types** (like `i3`, `d3`, `h1`, `z1d`, `m5d`) offer **NVMe-based instance store** with extremely fast throughput.
    
- Instance store volumes are not **resizable**, **encrypted**, or **available separately** from the EC2 instance.
    
- You can combine **EBS for persistent storage** and **instance store for temporary high-speed needs** in the same EC2.