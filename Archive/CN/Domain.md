# What is Domain?
• A domain is a type of computer network in which all user computers, printer accounts, and other devices are registered. 
• It is a central database located on single or multiple clusters of central computers, that is known as domain controllers.

### Collision Domain
• `Collisions` will happen in an Ethernet Network when two devices simultaneously try to send data on the Shared Media, since Shared Media is half-duplex and sending and receiving are not supported at the same time. 
• Collisions are a normal part of life in an Ethernet network when Ethernet operates in a Half duplex and under most circumstances should not be considered a problem. 
• A Collision Domain is any network segment in which collisions can happen (usually in Ethernet networks). In other words, a Collision Domain consists of all the devices connected using a Shared Media (Bus Topology or using Ethernet Hubs) where a Collision can happen between any device at any time.

### Broadcast Domain
• Broadcast is a type of communication, where the sending device send a single copy of data and that copy of data will be delivered to every device in the network segment. Broadcast is a required type of communication and we cannot avoid Broadcasts, because many protocols (Example: ARP and DHCP) and applications are dependent on Broadcast to function. 
• A Broadcast Domain consists of all the devices that will receive any broadcast packet originating from any device within the network segment. 
• In Mention picture, "Computer A" is sending a broadcast and switch will forward it to every ports and all the switches will get a copy of broadcast packet. Every switch will flood the broadcast packet to all the ports. Router also will get a copy of broadcast packet, but the Router will not forward the packet to the next network segment. 
• As the number of devices in the Broadcast Domain increases, number of Broadcasts also increases and the quality of the network will come down.