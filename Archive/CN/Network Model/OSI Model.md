[[CORE Books]]
### OSI Model Overview

The Open Systems Interconnection (OSI) model is a conceptual framework used to understand and design a network system that allows communication between all types of computer systems. It is structured into seven distinct layers, each with specific functions. Here is an overview of each layer and how they interact:

1. **Physical Layer**
2. **Data Link Layer**
3. **Network Layer**
4. **Transport Layer**
5. **Session Layer**
6. **Presentation Layer**
7. **Application Layer**

### Detailed Explanation of Each Layer

#### 1. Physical Layer

- **Function**: Deals with the physical connection between devices, including cables, switches, and other hardware.
- **Example**: Transmission of raw bitstreams over a physical medium like a coaxial cable.
- **Impact**: Issues at this layer can include broken cables, faulty network interface cards (NICs), and problems with signal transmission.

#### 2. Data Link Layer

- **Function**: Responsible for node-to-node data transfer and error detection and correction.
- **Example**: MAC addresses and Ethernet.
- **Impact**: Problems can involve frame errors, collisions, and MAC address conflicts.

#### 3. Network Layer

- **Function**: Manages device addressing, tracks the location of devices on the network, and determines the best way to move data.
- **Example**: IP addresses and routing.
- **Impact**: Issues here include routing errors, IP address conflicts, and problems with routers and Layer 3 switches.

#### 4. Transport Layer

- **Function**: Ensures complete data transfer and error recovery. It provides end-to-end communication services for applications.
- **Example**: TCP and UDP.
- **Impact**: Common issues are packet loss, retransmission errors, and port number conflicts.

#### 5. Session Layer

- **Function**: Manages sessions between applications. It establishes, manages, and terminates connections between local and remote applications.
- **Example**: Session management in web conferencing.
- **Impact**: Problems can involve session timeout, session establishment failures, and synchronization issues.

#### 6. Presentation Layer

- **Function**: Translates data between the application layer and the network format. It handles data encryption, decryption, compression, and decompression.
- **Example**: SSL/TLS encryption.
- **Impact**: Issues can include data format mismatch and problems with encryption/decryption.

#### 7. Application Layer

- **Function**: Provides network services directly to user applications. It interfaces directly with the software application to provide communication functions.
- **Example**: HTTP, FTP, and email protocols.
- **Impact**: Issues here include software bugs, application misconfigurations, and protocol errors.

### Example of Data Transmission

Consider sending an email:

1. **Application Layer**: The user composes an email in an email client.
2. **Presentation Layer**: The email client encrypts the email.
3. **Session Layer**: A session is established between the sender's and recipient's email servers.
4. **Transport Layer**: The email data is divided into segments, and TCP ensures they are transmitted reliably.
5. **Network Layer**: Each segment is encapsulated into packets with appropriate IP addresses for routing.
6. **Data Link Layer**: Packets are encapsulated into frames for node-to-node delivery.
7. **Physical Layer**: The frames are transmitted as bits over the physical medium.

### Impacts on Each Layer

- **Physical Layer**: A damaged cable can cause the entire transmission to fail.
- **Data Link Layer**: A MAC address conflict can prevent devices from communicating.
- **Network Layer**: An incorrect IP address can lead to data being sent to the wrong destination.
- **Transport Layer**: High packet loss can disrupt the communication session.
- **Session Layer**: If a session times out, the connection will be lost.
- **Presentation Layer**: Incorrect decryption can result in unreadable data.
- **Application Layer**: A bug in the email client can prevent the email from being sent or received.