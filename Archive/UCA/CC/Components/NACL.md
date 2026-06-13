
Here’s a **complete and clear guide to NACLs (Network Access Control Lists)** — a crucial security layer in cloud networking, especially in **AWS**.

---

## 🔹 What is a NACL?

**NACL (Network Access Control List)** is a **stateless**, **subnet-level firewall** that controls **inbound and outbound traffic** to and from subnets in a **Virtual Private Cloud (VPC)**.

> Think of a NACL as a security guard at the **subnet gate**, deciding which traffic can come in or go out — based on **rules you define**.

---

## 🔹 Key Characteristics

|Feature|Description|
|---|---|
|**Level**|Works at the **subnet** level|
|**Stateless**|Responses to allowed traffic **must be explicitly allowed** (both directions need rules)|
|**Rules**|You define **allow or deny** rules based on IP, protocol, and port|
|**Order**|Rules are evaluated in order, based on **rule number (lowest first)**|
|**Default NACL**|Automatically comes with a VPC and allows **all traffic in/out**|
|**Custom NACL**|Starts with **deny all** traffic until you add rules|

---

## 🔹 Inbound vs Outbound Rules

Each NACL has two sets of rules:

- **Inbound Rules** – Control traffic **entering** the subnet
    
- **Outbound Rules** – Control traffic **leaving** the subnet
    

> Because NACLs are stateless, if you allow inbound traffic, you also need to allow outbound response traffic.

---

## 🔹 NACL Rule Components

Each rule includes:

- **Rule number** (priority, lower numbers checked first)
    
- **Type** (e.g., HTTP, SSH, Custom TCP)
    
- **Protocol** (TCP, UDP, ICMP, etc.)
    
- **Port range** (e.g., 80 for HTTP)
    
- **Source/Destination IP** (CIDR block)
    
- **Allow or Deny**
    

---

## 🔸 Example: Allow SSH and HTTP, Deny Everything Else

|Rule #|Type|Protocol|Port|Source|Action|
|---|---|---|---|---|---|
|100|SSH|TCP|22|0.0.0.0/0|ALLOW|
|110|HTTP|TCP|80|0.0.0.0/0|ALLOW|
|*|All|All|All|0.0.0.0/0|DENY|

---

## 🔹 NACL vs Security Group (Quick Comparison)

|Feature|NACL|Security Group|
|---|---|---|
|Level|Subnet-level|Instance-level|
|Stateful|❌ No (stateless)|✅ Yes (stateful)|
|Rules|Allow or Deny|Only Allow|
|Rule Order|Evaluated in order|Evaluated all at once|
|Default behavior|Denies unless allowed|Denies unless allowed|
|Use Case|Broad subnet-level filtering|Fine-grained instance control|

---

## 🔹 Use Cases of NACLs

✅ Block specific IPs or countries at subnet level  
✅ Add an extra security layer in public-facing applications  
✅ Quickly allow/deny traffic during incidents  
✅ Segregate front-end and back-end subnets

---

## 🔹 AWS Default NACL

- Allows all traffic by default (both inbound and outbound)
    
- Associated automatically with every new subnet unless changed
    
- You can modify or replace it
    

---

## 🔹 Important Best Practices

- Always create **custom NACLs** for production and limit access.
    
- Use **least privilege** — only allow necessary ports/protocols.
    
- Remember to allow **return traffic** (stateless behavior).
    
- Apply **logging** using **VPC Flow Logs** to monitor traffic behavior.
    
- Use NACLs with **Security Groups** — don’t rely on one alone.
    

---

## 🔹 Common Interview Question

> **Q:** If NACL allows traffic but Security Group denies it, what happens?

🅰️ **Traffic is denied.** Both must allow it. **Security Group rules override NACL permissions at the instance level**.

---

## 🔹 Diagram (Text Representation)

csharp

CopyEdit

`Internet    | [Internet Gateway]    | [VPC]    | [Subnet] <-- NACL rules apply here    | [EC2 Instance] <-- Security Group applies here`