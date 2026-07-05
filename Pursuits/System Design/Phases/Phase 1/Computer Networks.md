Book:
[Computer Networking a top down approach](Assets/Books/computer-networking-a-top-down-approach-9.pdf)
Companion website and Author website [Link](https://media.pearsoncmg.com/bc/abp/cs-resources/products/product.html#student,isbn=0135415608)

# Internet

### Nuts and bolts of internet
- By some estimates, there were about 19 billion devices connected to the Internet in 2025.
- End systems are connected together by a network of communication links and packet switches
- Soul purpose of internet is to connect one end device to another.
- Routers: used in core network to connect networks and devices.
- Packet Switches: used in access control deciding who or what is allowed to access a network, resource, or service.

>**NOTE**
>Packet-switched networks (which transport packets) are in many ways similar to transportation networks transporting vehicles over highways, roads and, intersections. Consider, for example, a factory that needs to move a large amount of cargo to some destination warehouse located thousands of kilometers away. At the factory, the cargo is segmented and loaded into a fleet of trucks. Each of the trucks then independently travels through the network of highways, roads, and intersections to the destination warehouse. At the destination warehouse, the cargo is unloaded and grouped with the rest of the cargo arriving from the same shipment. Thus, in many ways, packets are analogous to trucks, communication links are analogous to highways and roads, packet switches are analogous to intersections, and end systems are analogous to buildings. Just as a truck takes a path through the transportation network, a packet takes a path through a computer network.


- End systems access the Internet through Internet Service Providers (ISPs)
- ISP is in itself a network of packet switches and communication links.
- ISP provides variety of types of network access to the end systems:
	- residential broadband access such as [[cable modem]] or [[DSL]] (Digital Subscriber Line)
	- high-speed local area network access
	- mobile wireless access

>**NOTE**
 **DSL:** Uses **Copper Telephone Lines** (originally built for voice).
 **Cable Modem:** Uses **Coaxial Cable Lines** (originally built for television).
  **Fiber (Netplus):** Uses **Fiber Optic Lines** (built explicitly for high-speed modern data).

- The sequence of communication links and packet switches traversed by a packet from the sending end system to the receiving end system is known as a route or path through the network.
- Since Internet is all about connecting end systems to each other, so the ISPs that provide access to end systems must also be interconnected.
- Thus Lower-tier ISPs are thus interconnected through national and international upper-tier ISPs and these upper-tier ISPs are connected directly to each other
- An upper-tier ISP consists of high-speed routers interconnected with high-speed fiber-optic links.
- Each ISP network, whether upper-tier or lower-tier, is managed independently, runs the IP protocol and conforms to certain naming and address conventions.

- End systems, packet switches, and other pieces of the Internet run protocols that control the sending and receiving of information within the Internet. The Transmission Control Protocol (TCP) and the Internet Protocol (IP) are two of the most important protocols in the Internet.

- The IP protocol specifies the format of the packets that are sent and received among routers and end systems
- The Internet’s principal protocols are collectively known as TCP/IP.
- Internet standards are developed by the Internet Engineering Task Force. The IETF standards documents are called requests for comments (RFCs).
- **RFCs (Request for Comments)** are technical documents that define Internet protocols and standards, such as TCP, IP, HTTP, and SMTP. Originally created to solve early networking challenges, there are now nearly 9,000 RFCs. Other organizations, such as the IEEE 802 LAN Standards Committee, develop standards for network technologies like Ethernet and Wi-Fi.


### Internet as a service
![[computer-networking-a-top-down-approach-9.pdf#page=29&rect=55,269,400,309|computer-networking-a-top-down-approach-9, p.5]]
- Distributed applications are those application which involves multiple end systems. Example: WhatsApp, Netflix, Free Fire etc.
	- These application run on end systems and not in packet switches or network core(routers).
	- Network core facilitates the data exchange but are not concerned with the application which is source or sink of data
- How does one program running on one end system instruct the Internet to deliver data to another program running on another end system?
	- When an end system is attached to Internet it provides a socket interface. Using this interface a program asks the Internet infrastructure to deliver data to a specific destination program running on another end system.
	- This Internet socket interface is a set of rules that the sending program must follow so that the Internet can deliver the data to the destination program.
	![[computer-networking-a-top-down-approach-9.pdf#page=30&rect=150,353,483,489|computer-networking-a-top-down-approach-9, p.6]]
	- The postal service, of course, provides more than one service to its customers. It provides express delivery, reception confirmation, ordinary use, and many more services. In a similar manner, the Internet provides multiple ser vices to its applications. When you develop an Internet application, you too must choose one of the Internet’s services for your application.


# Protocol
- Protocols can be understand by human analogy.
- Lets see how human protocol is analogous to network protocol
![[Pasted image 20260705123831.png|400]]

![[computer-networking-a-top-down-approach-9.pdf#page=32&rect=176,343,500,491|computer-networking-a-top-down-approach-9, p.8]]

- the exchange of messages and the actions taken when these messages are sent and received are the key defining elements of a protocol
- A protocol defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event.
![[computer-networking-a-top-down-approach-9.pdf#page=32&rect=203,116,485,175|computer-networking-a-top-down-approach-9, p.8]]


# The Network Edge

- Computers and other devices connected to the Internet are often referred to as end systems.
- End systems are also referred to as hosts because they host (that is, run) application programs such as a Web browser program, a Web server program, an e-mail client program, or an e-mail server program.
- host and end system can be used interchangeably.
- Hosts are sometimes further divided into two categories: clients and servers.

![[computer-networking-a-top-down-approach-9.pdf#page=34&rect=150,408,482,524|computer-networking-a-top-down-approach-9, p.10]]
![[computer-networking-a-top-down-approach-9.pdf#page=34&rect=159,38,468,365|computer-networking-a-top-down-approach-9, p.10]]

| Term      | Meaning                                                                                                |
| --------- | ------------------------------------------------------------------------------------------------------ |
| **Host**  | A computer (physical or virtual) that runs applications, virtual machines, or services.                |
| **Blade** | A thin, modular physical server that slides into a **blade chassis**. It is a type of server hardware. |
|           |                                                                                                        |
- Each blade is a physical server with its own CPU, RAM, and storage (or access to shared storage). If it runs workloads or virtual machines, it is functioning as a **host**.

```bash
Host
├── Client
│   ├── Laptop
│   ├── Desktop
│   └── Smartphone
└── Server
    ├── Tower Server
    ├── Rack Server
    └── Blade Server
```


### Access Networks