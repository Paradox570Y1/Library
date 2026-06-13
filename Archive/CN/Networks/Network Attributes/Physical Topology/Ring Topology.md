- In a ring topology, each device has a dedicated point-to-point connection with only the two devices on either side of it. A signal is passed along the ring in one direction, from device to device, until it reaches its destination. Each device in the ring incorporates a `repeater`. When a device receives a signal intended for another device, its repeater regenerates the bits and passes them along.
  ![[Pasted image 20240630134902.png|450]]
-  Advantages
	- A ring is relatively easy to install and reconfigure. 
	- Each device is linked to only its immediate neighbors (either physically or logically). To add or delete a device requires changing only two connections. 
- Disadvantages
	- The only constraints are media and traffic considerations (maximum ring length and number of devices). More the number of devices signal will become weaker.
	- In addition, fault isolation is simplified. Generally, in a ring a signal is circulating at all times. If one device does not receive a signal within a specified period, it can issue an alarm. The alarm alerts the network operator to the problem and its location. 
	- However, unidirectional traffic can be a disadvantage. In a simple ring, a break in the ring (such as a disabled station) can disable the entire network. 
		- This weakness can be solved by using a `dual ring` or a switch capable of closing off the break. 
- Ring topology was prevalent when IBM introduced its local-area network, Token Ring. Today, the need for higher-speed LANs has made this topology less popular.
- There are two types of token release techniques:
  - Early Token Release
  - Delay Token Release
- The following operations take place in ring topology are : 
 1.One station is known as a monitor station which takes all the responsibility to perform the operations. 
 2.To transmit the data, the station has to hold the token. After the transmission is done, the token is to be released for other stations to use. 
	 3.When no station is transmitting the data, then the token will circulate ixn the ring. 
 4.There are two types of token release techniques: Early token release releases the token just after transmitting the data and Delay token release releases the token after the acknowledgment is received from the receiver.