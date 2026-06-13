## 🔹 What is NAT Gateway?

A **NAT Gateway** (Network Address Translation Gateway) is a **cloud-managed service** that allows **resources in a private subnet** (which don't have public IPs) to **access the internet** securely **without being exposed to inbound internet traffic**.

> Think of it as a **middleman** between private resources and the internet, **masking internal IPs** with a public one for [[outgoing traffic]] only.

---

## 🔹 Why Do You Need a NAT Gateway?

In cloud environments (like AWS, Azure, GCP):

- Private subnets are used for security (e.g., databases, backend services).
    
- But sometimes these resources need to:
    
    - Download security patches.
        
    - Access external APIs.
        
    - Send logs to monitoring services.
        
- NAT Gateway makes this possible **without assigning a public IP** to each instance.
    

---

## 🔹 How NAT Gateway Works (Simple Example)

1. A server in a private subnet (say 10.0.1.5) sends a request to the internet.
    
2. The NAT Gateway **replaces the private IP** with its own public IP.
    
3. The response returns to the NAT Gateway, which **translates the IP back** and forwards it to the original instance.
    
4. No direct incoming traffic from the internet is allowed.
    

---

## 🔹 Types of NAT in General

|Type|Description|
|---|---|
|**NAT Gateway**|Managed service provided by cloud providers (e.g., AWS, Azure)|
|**NAT Instance**|A self-managed EC2/VM used to perform NAT manually|
|**Static NAT (SNAT)**|Maps one private IP to a public IP for consistent translation|
|**Dynamic NAT (DNAT)**|Maps multiple private IPs to a pool of public IPs|
|**PAT (Port Address Translation)**|Many-to-one mapping using different ports|

---

## 🔹 NAT Gateway in Different Cloud Providers

### 🔸 AWS NAT Gateway

- Fully managed.
    
- Automatically scales.
    
- Requires placement in a **public subnet**.
    
- Associated with an **Elastic IP**.
    
- High availability within an AZ.
    
- Charged per GB of data and per hour.
    

### 🔸 Azure NAT Gateway

- Provides outbound internet for subnets.
    
- Integrates with public IP prefix.
    
- Can be used with both standard load balancer and VM scalesets.
    

### 🔸 Google Cloud NAT

- Also a managed service.
    
- Provides NAT for Compute Engine VMs in private subnets.
    
- Can be **regional** and supports **manual or auto IP allocation**.
    

---

## 🔹 Benefits of NAT Gateway

✅ **Security** – Keeps private resources hidden from the internet.  
✅ **Scalability** – Handles thousands of concurrent connections.  
✅ **Reliability** – Highly available and resilient.  
✅ **Ease of Use** – Minimal configuration compared to NAT instances.  
✅ **No Maintenance** – Fully managed by the cloud provider.

---

## 🔹 NAT Gateway vs Internet Gateway vs NAT Instance

|Feature|NAT Gateway|NAT Instance|Internet Gateway|
|---|---|---|---|
|Managed Service|✅ Yes|❌ No (Self-managed)|✅ Yes|
|Supports Inbound|❌ No|✅ Yes (configurable)|✅ Yes|
|For Private Subnet|✅ Yes|✅ Yes|❌ No|
|For Public Subnet|❌ No|✅ Yes|✅ Yes|
|Auto Scaling|✅ Yes|❌ Manual|✅ Yes|
|Cost Efficiency|✅ High|❌ Lower (EC2 costs)|✅ High|

---

## 🔹 Common Use Cases

- Allowing private EC2 instances (or VMs) to:
    
    - Download OS updates.
        
    - Communicate with internet APIs.
        
    - Send metrics/logs to cloud monitoring tools.
        
- Protecting internal services from direct internet exposure.
    
- Accessing SaaS services from secure internal infrastructure.
    

---

## 🔹 Example Setup in AWS

1. Create a **public subnet** (for NAT Gateway).
    
2. Launch the **NAT Gateway** in this subnet with an Elastic IP.
    
3. Create a **private subnet**.
    
4. Set a **route** in the private subnet's route table:
    
    - Destination: `0.0.0.0/0`
        
    - Target: NAT Gateway
        
5. Launch EC2 in the private subnet with **no public IP**.
    
6. Now it can **access the internet outbound**, but **can’t be accessed directly from the internet**.
    

---

## 🔹 Limitations

- **No inbound traffic allowed** (by design).
    
- In AWS:
    
    - One NAT Gateway is specific to an **Availability Zone** (for high availability, deploy one in each AZ).
        
    - Costs can grow with data transfer volume.
        
- Not suitable if you need to **receive** data from the internet (use Load Balancer or Internet Gateway instead).