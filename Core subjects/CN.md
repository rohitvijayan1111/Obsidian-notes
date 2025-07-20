
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

# terms in a browser
---
### 🌐 **1. Web Client**
- A **Web Client** is the user-side of internet communication.
- It refers to the **browser** or any software you use to access websites.
- **Example**: When you use Chrome or Firefox to open a website, your browser is acting as the **Web Client**.
- Sometimes, helper software (like PDF readers or media players) also supports the client.
---
###  **2. Web Browser**
- A **Web Browser** is the program (software) that helps you **search, retrieve, and display web content** like web pages, images, videos, etc.
- It **sends requests** to websites (web servers) and shows you the results.
- Common browsers:
    - Google Chrome
    - Mozilla Firefox
    - Safari
    - Microsoft Edge
---
### 📄 **3. Webpage**
- A **Webpage** is a **single document** on the internet.
- It is written using **HTML (structure)** and **CSS (style)**.
- You view it using a browser.
- A webpage contains:
    - Text
    - Images
    - Videos
    - Links
- The **Home Page** is the **main or starting page** of a website.
- Each webpage has its **own unique address** (called a **URL**) you see in the address bar of your browser.
---
### 🌐 **4. Website**
- A **Website** is a **collection of related webpages** grouped under one **domain name**.
- Example:
    - `https://www.wikipedia.org` is a **website**.
    - The pages like `/main`, `/about`, `/contact` are its **webpages**.
- Websites are built for:
    - Sharing information
    - Selling products
    - Providing services
    - Entertainment, and more
---
### 🔍 **5. Search Engine**
- A **Search Engine** is a **tool or website** that helps you find information on the internet.
- You enter a query (keywords), and it shows you a list of matching results (webpages, images, videos, etc.).
- Examples of search engines:
    - **Google**
    - **Bing**
    - **Yahoo**
    - **DuckDuckGo**
- Instead of typing the exact website address, you can just **search for what you need**, and the engine will help you find the most relevant results.


## Types of Network Topology
## Point to Point Topology

Point-to-point topology is a type of topology that works on the functionality of the sender and receiver. It is the simplest communication between two nodes, in which one is the sender and the other one is the receiver.
## Mesh Topology

In a mesh topology, every device is connected to another device via a particular channel. Every device is connected to another via dedicated channels. These channels are known as links. In Mesh Topology, the protocols used are AHCP (Ad Hoc Configuration Protocols), [DHCP](https://www.geeksforgeeks.org/dynamic-host-configuration-protocol-dhcp/) (Dynamic Host Configuration Protocol), etc.
## Star Topology

In Star Topology, all the devices are connected to a single hub through a cable. This hub is the central node and all other nodes are connected to the central node.

In Star Topology, many popular [Ethernet](https://www.geeksforgeeks.org/what-is-ethernet/) LAN protocols are used as CD(Collision Detection), [CSMA](https://www.geeksforgeeks.org/carrier-sense-multiple-access-csma/) (Carrier Sense Multiple Access), etc.

## Bus Topology

Bus Topology is a network type in which every computer and network device is connected to a single cable. It is bi-directional. It is a multi-point connection and a non-robust topology because if the backbone fails the topology crashes. In Bus Topology, various [MAC](https://www.geeksforgeeks.org/mac-address-in-computer-network/) (Media Access Control) protocols are followed by LAN ethernet connections like [TDMA](https://www.geeksforgeeks.org/difference-between-fdma-tdma-and-cdma/), [Pure Aloha](https://www.geeksforgeeks.org/what-is-pure-aloha/), CDMA, [Slotted Aloha](https://www.geeksforgeeks.org/what-is-slotted-aloha/), etc.


## Ring Topology

In a Ring Topology, it forms a ring connecting devices with exactly two neighboring devices. A number of repeaters are used for Ring topology with a large number of nodes, because if someone wants to send some data to the last node in the ring topology with 100 nodes, then the data will have to pass through 99 nodes to reach the 100th node. Hence to prevent data loss repeaters are used in the network.

 In-Ring Topology, the Token Ring Passing protocol is used by the workstations to transmit the data

## ****Tree Topology****

Tree topology is the variation of the Star topology. This topology has a hierarchical flow of data. In Tree Topology, protocols like [DHCP](https://www.geeksforgeeks.org/dynamic-host-configuration-protocol-dhcp/)

In tree topology, the various secondary hubs are connected to the central hub which contains the repeater. This data flow from top to bottom i.e. from the central hub to the secondary and then to the devices or from bottom to top i.e. devices to the secondary hub and then to the central hub.


### Hybrid  Technology

Here’s a detailed yet simplified **insight into key network communication protocols**:  
**DHCP, CSMA/CD, CSMA/CA, Token Ring, Pure ALOHA, and Slotted ALOHA.**

---

### 🔄 **1. DHCP (Dynamic Host Configuration Protocol)**

- **Purpose**: Automatically assigns **IP addresses** to devices on a network.
    
- **Why?**: Manual IP assignment is slow and error-prone. DHCP makes it dynamic and automatic.
    
- **How it works**:
    
    - A new device joins the network.
        
    - It sends a **DHCP Discover** message (broadcast).
        
    - The **DHCP Server** replies with an **Offer**.
        
    - The device **requests** the offered IP.
        
    - The server **acknowledges** and leases the IP address.
        
- **Key Terms**:
    
    - IP Address
        
    - Subnet Mask
        
    - Gateway
        
    - DNS Server
        

---

### 📡 **2. CSMA/CD (Carrier Sense Multiple Access / Collision Detection)**

- **Used in**: **Wired Ethernet** networks (older tech)
    
- **Purpose**: Avoid data collisions on a **shared medium** (like a cable).
    
- **How it works**:
    
    1. Device listens to the channel (Carrier Sense).
        
    2. If channel is **idle**, it transmits.
        
    3. If two devices transmit at the same time → **Collision happens**.
        
    4. They **detect** the collision and stop.
        
    5. Then they **wait a random time** and try again.
        
- **Limitations**:
    
    - Inefficient under high traffic.
        
    - Mostly replaced by **switch-based Ethernet** now.
        

---

### 📶 **3. CSMA/CA (Carrier Sense Multiple Access / Collision Avoidance)**

- **Used in**: **Wireless networks** (like Wi-Fi)
    
- **Purpose**: Avoid collisions in a shared wireless medium.
    
- **Why needed?** In wireless, **collision detection** like CSMA/CD is hard because devices can’t hear each other well.
    
- **How it works**:
    
    1. Device **checks** if the channel is free.
        
    2. If free, it waits a small **random backoff** time before transmitting.
        
    3. Optionally uses **RTS/CTS** (Request to Send / Clear to Send) to reserve the channel.
        
    4. Then it sends the data.
        
- **Goal**: Prevent collisions **before** they happen.
    

---

### 🔁 **4. Token Ring (Token Passing Protocol)**

- **Type**: **Deterministic** access method.
    
- **How it works**:
    
    - Devices are connected in a **ring topology**.
        
    - A special **token** circulates around the ring.
        
    - A device can **only transmit** when it holds the token.
        
    - After sending, it **passes the token** to the next device.
        
- **Advantages**:
    
    - No collisions (controlled access).
        
    - Fair access to the medium.
        
- **Disadvantages**:
    
    - Slower than Ethernet.
        
    - If the token or one device fails, the whole network may go down.
        

---

### 🌐 **5. Pure ALOHA**

- **Used in**: Very early wireless systems (like satellite communication).
    
- **How it works**:
    
    - Devices **transmit whenever they want**, without checking the channel.
        
    - If a **collision** occurs, the sender waits for a **random time** and retransmits.
        
- **Efficiency**: Very low (~18%) because collisions are frequent.
    

---

### 📦 **6. Slotted ALOHA**

- **Improvement over Pure ALOHA**.
    
- **How it works**:
    
    - Time is divided into **slots**.
        
    - Devices can **only transmit** at the beginning of a time slot.
        
    - This reduces the chance of collisions.
        
- **Efficiency**: Better than Pure ALOHA (~36%).
    

---

### 📊 Summary Table

|Protocol|Type|Used In|Collision Handling|Efficiency|
|---|---|---|---|---|
|**DHCP**|IP Assignment|All networks|N/A (Not for collisions)|Automatic IP setup|
|**CSMA/CD**|Random Access|Wired Ethernet|Detects and retransmits|Moderate|
|**CSMA/CA**|Random Access|Wireless (Wi-Fi)|Avoids before sending|Better for wireless|
|**Token Ring**|Deterministic|Ring networks|Token prevents collisions|High, but slower|
|**Pure ALOHA**|Random Access|Wireless/satellite|Sends anytime, high collisions|~18%|
|**Slotted ALOHA**|Random Access|Wireless/satellite|Sends only at slot start|~36%|

---

Let me know if you'd like animations or diagrams to see how these protocols behave in action!



https://www.geeksforgeeks.org/computer-networks/network-devices-hub-repeater-bridge-switch-router-gateways/



# What is OSI Model? - Layers of OSI Model

- The ****OSI (Open Systems Interconnection)**** Model is a set of rules that explains how different computer systems communicate over a network.
- The OSI Model consists of 7 layers and each layer has specific functions and responsibilities
- This layered approach makes it easier for different devices and technologies to work together.
- 