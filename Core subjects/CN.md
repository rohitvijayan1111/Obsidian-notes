
What is CN?
A computer network is a collection of interconnected devices that share resources and information.

### Types of CN Architectures :

i) Client Server:
- is a type of Computer Network Architecture in which Nodes can be Servers or Clients. Here, the server node can manage the Client Node Behaviour.


ii) Peer-to-Peer:
- there is not any concept of a Central Server. Each device is free for working as either client or server.

### Network Devices

#### HUB:
  - **Layer**: Physical Layer (Layer 1)
- **Function**: Basic device that connects multiple devices in a network.
- **How it works**:
    - Broadcasts data to **all** connected devices regardless of destination.
    - Does **not** filter or manage traffic.
- **Downside**:
    - Causes **network congestion**.
    - No security or traffic control.

#### **Switch** 
- **Layer**: Data Link Layer (Layer 2)
- **Function**: Connects devices within the same network and forwards data only to the **intended recipient**.
- **How it works**:
    - Maintains a MAC address table.        
    - Learns which device is on which port.
    - Sends data only to the port where the destination device is connected.
- **Advantages**:
    - Efficient, reduces collisions.
    - More secure and faster than hubs.

### . **Bridge**
- **Layer**: Data Link Layer (Layer 2)
- **Function**: Connects and filters traffic between **two network segments**.
- **How it works**:
    - Like a basic switch, but only between **two LANs**.
    - Filters traffic based on MAC address.
- **Use Case**: Used to reduce network traffic or divide networks.
- A **network segment** is a **portion of a computer network** where all devices can communicate directly with each other **without needing a router**.
- If the two rooms are **not connected**, each room is its own **network segment**.
-  Bridges connect network segments within a single network.


#### **Router**
- **Layer**: Network Layer (Layer 3)
- **Function**: Connects **different networks** and routes data between them
- **How it works**:
    - Uses IP addresses to forward data packets.
    - Can connect to the internet.
    - Supports NAT, DHCP, firewall capabilities.
- **Advantages**:
    - Routes traffic efficiently.
    - Connects LANs to WANs.
- **Use Case**: Home/enterprise gateways, Internet connections.
- **Analogy**: Like a postal service that finds the best route to deliver a package between cities.





# Types of Computer Networks

## Classification Based on ****Geographical Area****

### ****1. Personal Area Network (PAN)****

PAN is the most basic type of computer network. It is a type of network designed to connect devices within a short range, typically around one person. It allows your personal devices, like smartphones, tablets, laptops, and wearables, to communicate and share data with each other.

