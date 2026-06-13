- In a star topology, each device has a dedicated point-to-point link only to a central controller, usually called a hub. 
- The devices are not directly linked to one another. Unlike a mesh topology, a star topology does not allow direct traffic between devices. 
- The controller acts as an exchange: If one device wants to send data to another, it sends the data to the controller, which then relays the data to the other connected device.
  ![[Pasted image 20240630131727.png|350]]
- Advantages
     - A star topology is less expensive than a mesh topology. In a star, each device needs only one link and one I/O port to connect it to any number of others. This factor also makes it easy to install and reconfigure. 
     - Far less cabling needs to be housed, and additions, moves, and deletions involve only one connection: between that device and the hub.
     - Other advantages include robustness. If one link fails, only that link is affected. All other links remain active. This factor also lends itself to easy fault identification and fault isolation. As long as the hub is working, it can be used to monitor link problems and bypass defective links.
- Disadvantages
     - One big disadvantage of a star topology is the dependency of the whole topology on one single point, the hub. If the hub goes down, the whole system is dead. 
     - Although a star requires far less cable than a mesh, each node must be linked to a central hub. For this reason, often more cabling is required in a star than in some other topologies (such as ring or bus).
     - The star topology is used in local-area networks (LANs), as we will see in Chapter 13. High-speed LANs often use a star topology with a central hub.

