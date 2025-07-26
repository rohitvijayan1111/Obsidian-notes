
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


**TCP PROTOCOL** - Transmission control protocol

- tcp protocol is an protocol used to create a dedicated connection to transfer data between two devices
- it is used when the data must be sent correctly and shouldnt suffer any data losses


WORKING OF TCP PROTOCOL:

CONNECTION ESTABLISHMENT:
- SYN - sent from the sender  to the recevier
- ACK- sent from the receiver to acknowledge the sender
- 