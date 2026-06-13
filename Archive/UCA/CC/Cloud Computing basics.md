# Limitations
- Security
- Internet Connectivity'
- Vendor lock-in

# Advantages
- Cost effective
- Scalability
# History
##### Transition
client-server -> distributed computing -> cloud computing

During the initial phase of cloud computing adaptation was quite slow which was accelerated by `Salesforce` and later `Amazon` started selling storage online which later transitioned to sell other services as well.


# Cloud Computing Requirement Model

- `public cloud`
	- Types: gdrive, uber, google maps
	- Can be used by anyone publicly
- `private cloud`
	- It's owned by an organization.
	- People registered with organization can use it.
- `Hybrid cloud`
	- It has features of both public and private cloud.
	- Like you can use Spotify without registering with email which is functionality of public cloud and can pay to use premium tier which is private cloud.
- `Community Cloud`
	- Group of organizations which are using a common cloud.


---
# DAY 2 

# Few terms
- `Runtime:`  program in execution
- `PaaS:` It's like Renting a platform
- `IaaS:` It's Renting just hardware (storage, servers)and virtualization, networking while having full control over the application.

`What are the disadvantages of using Paas,IaaS and similar services?`
- Security , although security mechanisms are provided.
- Less Customization
- Internet Connectivity

##### Cloud architecture
- `Backend` -> cloud itself
- `Frontend` -> Client Infra / GUI / User Interface

Application -> ensures communication b/w frontend and backend.
Service -> It stores all services provided and handled by cloud service provider.

###### Important components which handles application
- Management
- Infrastructure
- Security


---

AWS Global Infrastructure
- Region
	- US-east-1 (North Virginia)
- Availability zone
	- Minimum no. of zones are 3.
	- Maximum no. of zones are 6.
- Data Centers
- All availability zones are connected by low latency network.
- When you have to opt for zone , then instead of giving preference , just opt for all as it provides high availability.

# Tools
- **EC2**
	- Using it we can create instance of virtual machines.
	- It is computation services provided by AWS.



# Instance type
- General Purpose
	- Used in small  and medium sized database.
	- Instance family - M5 , M6g , M7g
- Compute Optimized
- Memory Optimized
	- Real time processing like live streaming
	- It's not about storing  , but memory required for processing.
	- Instance family - R5, R6, X1
		- When there is R, it means it is for memory intensive applications
- Storage Optimized
	- Instance - B3, B4
- Accelerated 
	- P series, G2 , G5
- High Performance Computing


# Auto Scaling instances

- Desired capacity, Max capacity , Min capacity
- Threshold more than 80% then scale up
- Threshold less than 30% then scale down
- Cloud Watch sends the alert that you  have reached a particular threshold
- Set Target group
- Set Desired capacity

Download cookie software


# NginX server

- Use Ubuntu allow all trafic and select t2.micro without keypair
- use `sudo -i` so that we don't need to write sudo again and again
`apt-get update` updates ubuntu package
`apt-get install nginx`
`curl localhost` it send's a request to server and receives the response
`cd /var/www/html`
`echo "Welcome to Chitkara University" >index.html` - to write a custom page 

Now copy the ip address of instance at paste on browser and same page can be seen.


# Putty

- Create amazom linux machine with .ppk key pair with only ssh traffic needed.
- Go to SSH client on clicking connect

![[Pasted image 20250725122855.png]]

![[Pasted image 20250725122947.png]]
then browse private key  and select the downloaded key pair

![[Pasted image 20250725123120.png]]
Accept it

![[Pasted image 20250725123207.png]]

![[Pasted image 20250725123234.png]]


---
![[Pasted image 20250731112128.png]]

![[Pasted image 20250731112601.png]]

![[Pasted image 20250731112550.png]]

![[Pasted image 20250731112701.png]]

![[Pasted image 20250731112750.png]]

![[Pasted image 20250731113048.png]]

![[Pasted image 20250731113100.png]]

![[Pasted image 20250731113155.png]]

![[Pasted image 20250731113212.png]]

![[Pasted image 20250731113348.png]]

![[Pasted image 20250731113558.png]]

![[Pasted image 20250731113629.png]]

![[Pasted image 20250731114208.png]]
![[Pasted image 20250731114230.png]]
![[Pasted image 20250731114241.png]]

![[Pasted image 20250731114324.png]]

![[Pasted image 20250731114312.png]]

![[Pasted image 20250731114350.png]]

![[Pasted image 20250731114433.png]]

![[Pasted image 20250731114839.png]]

![[Pasted image 20250731115012.png]]

![[Pasted image 20250731115034.png]]

![[Pasted image 20250731115403.png]]

![[Pasted image 20250731115552.png]]

![[Pasted image 20250731115618.png]]

![[Pasted image 20250731115630.png]]

![[Pasted image 20250731115945.png]]

![[Pasted image 20250731115957.png]]

![[Pasted image 20250731120009.png]]

![[Pasted image 20250731120049.png]]


# AMI
- It is a template used to configure the instance (in which  you choose OS based on compatibility of instance type) , just like replicating an instance using a predefined template.
- It's full form is `Amazon Machine Image`.
- There are two types of Root Device Type
	- Amazon [[EBS]]
	- [[Instance Store]]
- Types of AMI:
	- Amazon AMI
	- Amazon Market Place AMI
	- Community AMI
		- Any **public AMI** becomes part of the **Community AMI pool**, but not all public AMIs are necessarily shown unless searched.
	- Custom AMI
		- Created and owned by user.
		- I can keep my AMI public or i can keep it private.
[Resources](https://chatgpt.com/share/688c58c2-1720-8000-951f-d2ea797dfa8f)



---
#Activity
- Allocate
- Associate
- Disassociate
- Release

![[Pasted image 20250807112518.png]]

![[Pasted image 20250807112529.png]]

![[Pasted image 20250807112556.png]]

![[Pasted image 20250807112625.png]]

![[Pasted image 20250807112658.png]]

![[Pasted image 20250807112723.png]]

![[Pasted image 20250807112759.png]]

![[Pasted image 20250807112820.png]]

![[Pasted image 20250807112920.png]]

![[Pasted image 20250807115708.png]]

![[Pasted image 20250807115719.png]]

![[Pasted image 20250807115733.png]]

![[Pasted image 20250807120532.png]]

![[Pasted image 20250807120543.png]]

![[Pasted image 20250807120618.png]]

---

# Load Balancing
- With the help of internet gateway , outside traffic can enter to your network.
- You can't directly expose your public IP.
- Routing table contains multiple pathways involving different hops to reach the destination.
- Types:
	- Application Load balancer
	- Network Load balancer
	- Gateway Load balancer
- Steps to do this activity:
	- Create two security groups:
		- One for SG- ALB (Application Load Balancer)
		- One for EC2
			- Inbound rules for it will be SSH , HTTP for SG-ALB, don't allow all traffic.
	- Launch Instances
		- Take at least 2 instances so that load can be balanced among them.
	- Target Group
		- **Target Group** is basically the group of EC2 instances (or other endpoints) that the **Application Load Balancer (ALB)** will forward traffic to.
	- Create Load Balancing


![[Pasted image 20250808114427.png]]

![[Pasted image 20250808114452.png]]

![[Pasted image 20250808114528.png]]

![[Pasted image 20250808114622.png]]

![[Pasted image 20250808114821.png]]

![[Pasted image 20250808114957.png]]

![[Pasted image 20250808115038.png]]

![[Pasted image 20250808115153.png]]

![[Pasted image 20250808115334.png]]

![[Pasted image 20250808115340.png]]

![[Pasted image 20250808115727.png]]

![[Pasted image 20250808115745.png]]

![[Pasted image 20250808115603.png]]


![[Pasted image 20250808115612.png]]

![[Pasted image 20250808115928.png]]

![[Pasted image 20250808120019.png]]

![[Pasted image 20250808120228.png]]

![[Pasted image 20250808120414.png]]

![[Pasted image 20250808120426.png]]

![[Pasted image 20250808120502.png]]

![[Pasted image 20250808120542.png]]

![[Pasted image 20250808121245.png]]

![[Pasted image 20250808124153.png]]

![[Pasted image 20250808124202.png]]


# S3 Practical

Create Empty Bucket
upload an image


![[Pasted image 20250829111902.png]]

![[Pasted image 20250829112010.png]]

Uncheck `block all public access`
![[Pasted image 20250829112220.png]]

![[Pasted image 20250829112757.png]]

![[Pasted image 20250829113550.png]]

![[Pasted image 20250829113634.png]]

![[Pasted image 20250829113646.png]]

Upload two files
- index.html - primary file
- error.html - in case primary file doesn't work it redirects to error.html

![[Pasted image 20250829113923.png]]


![[Pasted image 20250829114004.png]]

![[Pasted image 20250829114015.png]]

![[Pasted image 20250829114036.png]]

![[Pasted image 20250829114719.png]]


![[Pasted image 20250829114732.png]]

![[Pasted image 20250829114836.png]]

![[Pasted image 20250829114947.png]]

![[Pasted image 20250829114955.png]]

![[Pasted image 20250829115007.png]]

![[Pasted image 20250829115051.png]]


![[Pasted image 20250829115143.png]]

![[Pasted image 20250829115304.png]]


![[Pasted image 20250829115443.png]]


![[Pasted image 20250829115929.png]]

---
# Database

#Types
- Relational
	- Used in smaller dataset compared to big data where data can be organized by ER Diagrams for solid foundation. 
- Non-Relational
	- Used in key value pair, Big data and often in unorganized data.
	- Example : DynamoDB

### Relational Database System (RDS)

Read About
- Database Instance
- Database Engine 
- Cluster 
	- Collection of available instances or computing nodes.
	- Read about head node and compute node
- Multi Database Instance Deployment
- Access Control and Security group
- DynamoDB 
	- Fully managed, no SQL, serverless database
- Database Instance Classes
- Amazon RedShift
	- Process analytical data which requires analysis.


---
To create VPC , you need to know following:
- VPC
- Internet Gateway
- Subnet
- Rules

- We will be making both public and private subnet.
- All traffic should be enabled through internet gateway in public subnet which will be absent in private subnet.


![[Pasted image 20251003113015.png]]

![[Pasted image 20251003113316.png]]

![[Pasted image 20251003113418.png]]

![[Pasted image 20251003113636.png]]



![[Pasted image 20251003113748.png]]

![[Pasted image 20251003113802.png]]

![[Pasted image 20251003114035.png]]

![[Pasted image 20251003114253.png]]

![[Pasted image 20251003114503.png]]

![[Pasted image 20251003114323.png]]

![[Pasted image 20251003114526.png]]

![[Pasted image 20251003114858.png]]


- In private network only destination route is added so we have to attach an IG to 0.0.0.0/0 which is internet to make it public.

![[Pasted image 20251003115013.png]]

![[Pasted image 20251003115041.png]]

![[Pasted image 20251003115056.png]]

![[Pasted image 20251003115208.png]]

![[Pasted image 20251003115221.png]]

Now we need to associate subnets to route table , public to public and private to private.

![[Pasted image 20251003115351.png]]

![[Pasted image 20251003115416.png]]

![[Pasted image 20251003115428.png]]

![[Pasted image 20251003115514.png]]

![[Pasted image 20251003115535.png]]

![[Pasted image 20251003115550.png]]

	
	Now change VPC to your created VPC while running EC2 instances.


![[Pasted image 20251003115803.png]]

![[Pasted image 20251003115845.png]]

![[Pasted image 20251003120053.png]]

![[Pasted image 20251003120123.png]]

![[Pasted image 20251003120306.png]]

![[Pasted image 20251003120316.png]]

![[Pasted image 20251003120411.png]]

![[Pasted image 20251003120433.png]]

![[Pasted image 20251003120458.png]]

---

![[Pasted image 20251030093948.png]]

![[Pasted image 20251030094050.png]]

![[Pasted image 20251030094204.png]]

![[Pasted image 20251030094306.png]]

![[Pasted image 20251030094338.png]]

Ud35WDTM2cLDW4znySzm
paradox570y1.cluster-cui2r5ryyl8i.us-east-1.rds.amazonaws.com


Add security group so that workbench accept the request
![[Pasted image 20251030100239.png]]
- select MySQL/Aurora type connection with custom connection to anywhere.

In case not using workbench create an EC2 instance using above security group.



---
---
![[Pasted image 20251103093815.png]]

![[Pasted image 20251103093833.png]]

![[Pasted image 20251103093847.png]]

![[Pasted image 20251103093916.png]]

![[Pasted image 20251103094355.png]]

![[Pasted image 20251103094418.png]]

![[Pasted image 20251103094704.png]]

![[Pasted image 20251103095020.png]]

![[Pasted image 20251103095030.png]]
![[Pasted image 20251103095046.png]]

![[Pasted image 20251103095157.png]]

![[Pasted image 20251103095206.png]]

![[Pasted image 20251103095255.png]]

![[Pasted image 20251103095333.png]]

![[Pasted image 20251103095350.png]]

![[Pasted image 20251103095938.png]]![[Pasted image 20251103095934.png]]

![[Pasted image 20251103100114.png]]

![[Pasted image 20251103100151.png]]


![[Pasted image 20251103100230.png]]

![[Pasted image 20251103100248.png]]

![[Pasted image 20251103100405.png]]

![[Pasted image 20251103103955.png]]


---
---

![[Pasted image 20251104114824.png]]

![[Pasted image 20251104115441.png]]

![[Pasted image 20251104115452.png]]

![[Pasted image 20251104115518.png]]

![[Pasted image 20251104115618.png]]

![[Pasted image 20251104115728.png]]


---

![[Pasted image 20251104120131.png]]

![[Pasted image 20251104120151.png]]

![[Pasted image 20251104120225.png]]

![[Pasted image 20251104120235.png]]

![[Pasted image 20251104120247.png]]

![[Pasted image 20251104120450.png]]

![[Pasted image 20251104120335.png]]

![[Pasted image 20251104120507.png]]

![[Pasted image 20251112234204.png]]

![[Pasted image 20251113101424.png]]

![[Pasted image 20251113101431.png]]
![[Pasted image 20251113102059.png]]
