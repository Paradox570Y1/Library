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
>Packet-switched networks (which transport packets) are in many ways similar to transportation networks transporting vehicles over highways, roads and, intersections. Consider, for example, a factory that needs to move a large amount of cargo to some destination warehouse located thousands of kilometers away. At the factory, the cargo is segmented and loaded into a fleet of trucks. Each of the trucks then independently travels through the network of highways, roads, and intersections to the destination warehouse. At the desti nation warehouse, the cargo is unloaded and grouped with the rest of the cargo arriving from the same shipment. Thus, in many ways, packets are anal ogous to trucks, communication links are analogous to highways and roads, packet switches are analogous to intersections, and end systems are analogous to buildings. Just as a truck takes a path through the transportation network, a packet takes a path through a computer network.


- End systems access the Internet through Internet Service Providers (ISPs)
- ISP is in itself a net work of packet switches and communication links.
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
continued (page 5)