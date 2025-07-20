
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

### 1. **PAN (Personal Area Network)**
- **Range**: ~1 to 10 meters
- **Scope**: **Personal** use, around a single person
- **Devices Involved**: Smartphones, laptops, headphones, smartwatches
- **Connection Types**: Bluetooth, USB, infrared
- **Example**:
    - Connecting your **phone to wireless earbuds** via Bluetooth
    - Syncing your smartwatch with your phone
---
### 🏠 2. **LAN (Local Area Network)**
- **Range**: Covers a **building** or small area (up to a few kilometers)
- **Scope**: Office, school, home
- **Speed**: High-speed (typically 100 Mbps – 10 Gbps)
- **Devices**: Computers, printers, servers, switches, routers
- **Ownership**: Usually owned, controlled, and managed by a **single organization or individual**
- **Example**:
    - A **home Wi-Fi network**
    - Office network connecting employees' PCs to a shared printer
---
### 🌆 3. **MAN (Metropolitan Area Network)**
- **Range**: Covers a **city or metropolitan area** (tens of kilometers)
- **Scope**: Multiple LANs across a city
- **Managed by**: ISPs, governments, universities, or large companies
- **Technology**: Often uses fiber optics
- **Example**:
    - A university campus network connecting all buildings
    - City-wide internet or cable TV network
---
### 🌍 4. **WAN (Wide Area Network)**
- **Range**: Covers a **large geographical area** (country or world)
- **Scope**: Multiple LANs and MANs connected over long distances
- **Speed**: Generally lower than LAN due to long-distance transmission
- **Ownership**: Multiple organizations (public + private networks)
- **Technology**: Uses satellites, leased lines, fiber optics
- **Example**:
    - The **Internet** (largest WAN)
    - A multinational company’s network connecting offices globally



# Difference between network and internet
### 🌐 **1. Network**
A **network** is a group of **interconnected devices** (like computers, printers, routers) that can **communicate and share resources** with each other.
#### 🔧 Key Points:
- Can be **small or large** (e.g., PAN, LAN, MAN, WAN).
- Can be **private or public**.
- Devices are connected using **wired or wireless** technologies.
- Examples:
    - Your **home Wi-Fi** (LAN)
    - A company's internal office network
    - A campus network
---
### 🌍 **2. Internet**
The **Internet** is the **worldwide system** of **interconnected networks** — it is essentially a **network of networks**.
#### 🔧 Key Points:
- Connects **millions of private, public, academic, business, and government networks**.
- Uses **standardized protocols** like **TCP/IP**.
- Managed by multiple entities worldwide (not owned by one organization).
- Enables services like **web browsing, email, cloud computing, etc.**
---
### 📊 Comparison Table:

| Feature       | **Network**                      | **Internet**                                   |
| ------------- | -------------------------------- | ---------------------------------------------- |
| Definition    | Group of connected devices       | Global system of interconnected networks       |
| Scope         | Local or organizational          | Worldwide                                      |
| Ownership     | One entity (e.g., home, company) | No single owner (multiple ISPs, organizations) |
| Accessibility | Private or limited access        | Public and globally accessible                 |
| Example       | Office LAN, Home Wi-Fi           | Google, YouTube, Email, Web                    |

