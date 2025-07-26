
- osi - open system interconnection
- seven layer model:
	- physical
	- data link
	- network
	- transport
	- session
	- presentation 
	- application


- physical layer-> physical mode of data transfer 
	- could it be wirless?
- data link layer
	- adds the mac address to the packet , and it is called as frame
	- Inside every network-enabled computer is a **N**etwork **I**nterface Card (**NIC**) which comes with a unique MAC address to identify it.

- Network layer
- Transport layer
- session layer
	- The **Session Layer** is responsible for **establishing, maintaining, and terminating communication sessions** between two devices (e.g., computers, applications) on a network
	- This includes authentication and authorization (e.g., logging into a remote server).
	- **Checkpoints (Synchronization):**
		- Implements **checkpoints** in data streams.
		- If data is lost or corrupted, the transfer resumes from the last checkpoint, not from the beginning — this **saves bandwidth and time**.
- presentation layer
	- This layer acts as a translator for data to and from the application layer (layer 7)
	- Security features such as data encryption (like HTTPS when visiting a secure site) occur at this layer.
- Application layer
	- - - Initiates requests to lower layers to perform tasks like file transfers, email delivery, or web browsing.
	- allows networked services (e.g., web servers, FTP servers) to announce their presence.




TCP/ IP model


LAYERS:
- data link/ network interface
- internet 
- transport 
- application


# **TCP PROTOCOL** - Transmission control protocol

- tcp protocol is an protocol used to create a dedicated connection to transfer data between two devices
- it is used when the data must be sent correctly and shouldnt suffer any data losses


## 🧠 **Working of the TCP Protocol**

### 1. ✅ **Connection Establishment** (Three-Way Handshake)

Before sending data, a **reliable connection** must be established between the **Sender (Client)** and **Receiver (Server)**.

Both devices select a random **Initial Sequence Number (ISN)** to track sent and received data.

|Step|Sender (Client)|Receiver (Server)|Sequence Numbers|
|---|---|---|---|
|1. **SYN**|Sends SYN packet to initiate connection|—|ISN = 0|
|2. **SYN/ACK**|—|Sends SYN to initiate return connection and ACK to confirm receipt|ISN = 5000|
|3. **ACK**|Sends ACK to confirm server's ISN|—|ACK = 5001|

✅ Connection is established! Now both sides know each other's ISNs and are ready to transfer data in order.

---

### 2. 📦 **Data Transfer**

- Data is sent **reliably and in order**.
    
- Each byte is tracked using **sequence numbers**.
    
- Acknowledgments (ACKs) are sent by the receiver to confirm receipt of data.
    

Example:  
If client sends 100 bytes starting at sequence number 1,  
the receiver sends back `ACK = 101` to confirm all 100 bytes were received.

---

### 3. 🔚 **Connection Termination** (Four-Step FIN Process)

When the communication is complete, the connection must be closed **gracefully** to release system resources.

|Step|Who Sends|Packet|Purpose|
|---|---|---|---|
|1.|**Sender**|`FIN`|Requests to close its side of the connection|
|2.|**Receiver**|`ACK`|Acknowledges the FIN|
|3.|**Receiver**|`FIN`|Now requests to close its own side|
|4.|**Sender**|`ACK`|Acknowledges the receiver's FIN|

✅ Connection is fully closed on both sides.

## 🔻 **TCP RST (Reset) Flag**

### 🧠 **What is it?**

- The `RST` (Reset) flag in TCP is used to **immediately terminate** a connection.
    
- It **forcibly closes** the connection without the standard **FIN/ACK** four-step termination.
    
- It is usually sent when there’s an **error**, **unexpected packet**, or **unavailable service**.

That's totally normal — **TCP sequence and acknowledgment numbers** can be confusing at first, especially when you're seeing them jump or repeat. But once you understand **how they work byte-by-byte**, it all clicks into place.

Let’s break it down **very simply** using a step-by-step analogy and **color-coded values**.

---

## 🎯 Think of it like this:

- **Sequence Number (SEQ)** = "I’m sending data starting from this byte."
    
- **Acknowledgment Number (ACK)** = "I’m expecting the next byte to be this."
    

✅ TCP tracks **bytes**, not messages.

---

## 🧪 Simple TCP Example (Sending "Hello")

We’ll assume:

- **Client** starts with SEQ = `1000`
    
- **Server** starts with SEQ = `3000`
    

### 📶 Step 1: 3-Way Handshake

|Step|Who|Action|SEQ|ACK|Meaning|
|---|---|---|---|---|---|
|1|Client → Server|SYN|`1000`|—|Start connection, my SEQ = 1000|
|2|Server → Client|SYN-ACK|`3000`|`1001`|My SEQ = 3000, I got your SYN (next expected = 1001)|
|3|Client → Server|ACK|`1001`|`3001`|ACK your SYN (next expected = 3001)|

> **Note**: `SYN` uses **1 sequence number**, even though it doesn’t send data. That’s why we go from `1000` → `1001`.

---

### ✉️ Step 2: Client Sends Data ("Hello" = 5 bytes)

|Step|Who|Action|SEQ|ACK|Meaning|
|---|---|---|---|---|---|
|4|Client → Server|Send "Hello"|`1001`|`3001`|Sending 5 bytes starting at 1001|
|5|Server → Client|ACK|`3001`|`1006`|Received up to byte 1005, expect next byte = 1006|

> **Why 1006?** Because:
> 
> - Client’s data started at **1001**
>     
> - Sent **5 bytes** ("Hello")  
>     → So the next byte should be **1006**
>     

---

### 💬 Step 3: Server Sends "Hi" (2 bytes)

|Step|Who|Action|SEQ|ACK|Meaning|
|---|---|---|---|---|---|
|6|Server → Client|Send "Hi"|`3001`|`1006`|Sending 2 bytes starting at 3001|
|7|Client → Server|ACK|`1006`|`3003`|Got your 2 bytes; next expected is 3003|

> **Why 3003?** Because:
> 
> - Server started at **3001**
>     
> - Sent **2 bytes**  
>     → So the next byte should be **3003**
>     

---

## 🔚 Step 4: Closing the Connection (FIN)

> Even **FIN** uses 1 sequence number, just like SYN.

|Step|Who|Action|SEQ|ACK|Meaning|
|---|---|---|---|---|---|
|8|Client → Server|FIN|`1006`|`3003`|Client wants to close connection|
|9|Server → Client|ACK|`3003`|`1007`|ACK the FIN (1006 + 1)|
|10|Server → Client|FIN|`3003`|`1007`|Server closes its side|
|11|Client → Server|ACK|`1007`|`3004`|ACK the FIN (3003 + 1)|

---

## ✅ Key Rules to Remember

|Rule|Meaning|
|---|---|
|SYN and FIN **consume 1 byte**|Even though no data is sent|
|ACK numbers = **next expected SEQ**|So it’s always SEQ + data length|
|SEQ numbers = **starting byte of data**|Not the total count sent|
|Data length affects how SEQ changes|E.g., "Hello" = 5 bytes → SEQ increases by 5|

---

## 🔁 Final Sequence Flow Recap

|Event|Client SEQ/ACK|Server SEQ/ACK|
|---|---|---|
|SYN|1000 / —|— / —|
|SYN-ACK|— / 1001|3000 / —|
|ACK|1001 / 3001|— / —|
|Send "Hello"|1001–1005|—|
|ACK "Hello"|— / 1006|3001|
|Send "Hi"|—|3001–3002|
|ACK "Hi"|1006 / 3003|—|
|FIN/ACK Close|1006–1007|3003–3004|

---

Would you like a **visual diagram** (sequence chart) to go along with this? It helps a lot — and I can generate it if you switch to a regular (non-temporary) chat.




#  UDP

- UDP is used in situations where applications can tolerate data being lost (such as video streaming or voice chat) or in scenarios where an unstable connection is not the end-all.
- 


|   |   |
|---|---|
|**Header**|**Description**|
|Time to Live (TTL)|This field sets an expiry timer for the packet, so it doesn't clog up your network if it never manages to reach a host or escape!|
|Source Address|The IP address of the device that the packet is being sent from, so that data knows where to return to.|
|Destination Address|The device's IP address the packet is being sent to so that data knows where to travel next.|
|Source Port|This value is the port that is opened by the sender to send the UDP packet from. This value is randomly chosen (out of the ports from 0-65535 that aren't already in use at the time).|
|Destination Port|This value is the port number that an application or service is running on the remote host (the one receiving the data); for example, a webserver running on port 80. Unlike the source port, this value is not chosen at random.|
|Data|This header is where data, i.e. bytes of a file that is being transmitted, is stored.|