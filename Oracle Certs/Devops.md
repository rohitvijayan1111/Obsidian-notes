# Devops

![[Pasted image 20250807180425.png]]

![[Pasted image 20250807180520.png]]


### **Application Layer**

- **OKE (Oracle Kubernetes Engine):** Run containerized microservices at scale.
    
- **OCI Functions:** Event-driven, serverless functions for lightweight tasks.
    
- **OCI Container Registry & Artifact Registry:** Store container images & artifacts securely.
    

### **Integration Layer**

- **OCI API Gateway:**
    
    - Entry point for external consumers (customers, third-party aggregators).
        
    - Handles authentication, authorization, rate limiting, and routing.
        

### **Data Layer**

- **Autonomous Database (serverless):**
    
    - Stores bookings, availability, and customer data.
        
    - Fully managed, self-patching, and auto-scaling.
        

### **Security Layer**

- **Web Application Firewall (WAF):** Protects the site against OWASP Top 10 attacks.
    
- **OCI Vault:** Manages sensitive data (API keys, credentials, encryption keys).
## 5. **Step 4: Development & Deployment Automation**

- **OCI DevOps Projects:** Automates CI/CD pipelines for faster release cycles.
    
- **OCI Resource Manager:** Infrastructure as Code (IaC) using Terraform templates.
    

---

## 6. **Step 5: Communication & Observability**

- **OCI Service Mesh:** Simplifies secure service-to-service communication.
    
- **OCI Logging & Monitoring:** Tracks app health, performance, and errors.
    
- **OCI Notifications:** Sends alerts to the DevOps team when issues occur.




![[Pasted image 20250828101239.png]]

## **CI/CD & Automation**

- **OCI DevOps Project** + **DevOps Code Repository**:
    
    - Automates build, test, and deployment pipelines.
        
- **Artifact & Container Registry**:
    
    - Stores container images and deployment artifacts securely.
        
- Deployment strategies supported:
    
    - **Blue-Green** (switch between old/new versions seamlessly).
        
    - **Canary** (release updates gradually to a subset of users).
        

👉 This ensures **faster, safer deployments** with minimal downtime.

---

## 6. **Messaging & Notifications**

- **OCI Streaming**:
    
    - Captures booking-related events/messages.
        
    - Supports analytics and downstream integrations.
        
- **OCI Notifications**:
    
    - Sends email/SMS alerts to hotel admin teams for new bookings.
        

---

## 7. **Observability & Event Handling**

- **OCI Events Service**:
    
    - Reacts to changes (e.g., trigger a function when a booking is made).
        
- **OCI Monitoring**:
    
    - Tracks system metrics like CPU, memory, network, and app performance.
        
- **OCI Logging**:
    
    - Captures application logs, user interactions, and system events for troubleshooting.
        

👉 Together, these ensure **real-time visibility**, proactive issue detection, and automated responses.


# Microservice

![[Pasted image 20250828102543.png]]
## 🔹 Communication in Microservices
Because microservices are separate processes, they need **network communication**:
1. **By Protocol (sync vs async)**
    - **Synchronous (Request-Response)** → HTTP, HTTPS, gRPC(gRPC - used mostly for microservices to interact with each other)
        - Client waits for response.
    - **Asynchronous (Message Queue)** → AMQP (RabbitMQ, Kafka)
        - Client sends message and continues, service responds later.
2. **By Receivers (single vs many)**
    - **Single Receiver** → One service gets the request (command pattern).
    - **Many Receivers** → Event-driven architecture, message sent to multiple services
👉 Most real systems use a **mix** (example: async queues for heavy work, HTTP for quick requests).


## 🔹 Design Methodology for Microservices

### **12-Factor App Methodology**

The **12-factor app** is a set of best practices for building cloud-friendly, scalable applications that fit well with microservices. It was created by **Heroku** in 2011. Here’s a summary of the factors:

1. **Codebase**
    
    - Each microservice should have its **own code repository**.
        
    - Helps with **CI/CD** and independent deployment.
        
2. **Dependencies**
    
    - Manage all packages via **package managers** (Maven, Gradle, npm).
        
    - In containers, use **Dockerfiles**; in non-containerized, use configuration tools like Chef/Ansible.
        
3. **Configuration**
    
    - Keep **configs separate from code** (environment variables or external config files).
        
    - This allows updating configs **without redeploying the app**.
        
4. **Backing Services**
    
    - Services (databases, caches, message brokers) should be **replaceable without code changes**.
        
    - Example: Switch MySQL → cloud DB without touching code.
        
5. **Build, Release, Run**
    
    - Separate **build, release, and run stages**.
        
    - Docker + CI/CD pipelines make this easier.
        
6. **Processes**
    
    - Apps should be **stateless** (use Redis, Memcached for state).
        
    - Stateless apps can scale horizontally easily.
        
7. **Port Binding**
    
    - Apps should be **self-contained** and expose APIs via their own ports instead of relying on external servers.
        
8. **Concurrency**
    
    - Prefer **horizontal scaling** (more instances) over vertical scaling (bigger machines).
        
    - Containers make this easy.
        
9. **Disposability**
    
    - Services should start/stop **quickly and safely**.
        
    - Docker containers handle this naturally.
        
10. **Dev/Prod Parity**
    
    - Keep **development, staging, and production environments similar** to reduce bugs.
        
    - Containers help maintain this parity.
        
11. **Logs**
    
    - Apps should **stream logs** to monitoring tools instead of writing to files.
        
    - Important for troubleshooting in microservices.
        
12. **Admin Processes**
    
    - Separate **maintenance tasks** (analytics, DB cleanup, feature toggles) from the main app.


## 🔹 What is Containerization?

- **Containerization** is a form of virtualization that runs applications in **isolated spaces called containers**.
    
- **Containers share the same OS kernel**, unlike virtual machines which each have their own OS.
    
- The **container engine** (like Docker) manages creating, running, and deploying containers.
    

---

## 🔹 How Containers Work

- Think of a container as a **“digital suitcase”** containing:
    
    - Application code
        
    - Libraries
        
    - Dependencies
        
    - Configuration files
        
- Containers are **portable**: they run the same way on **any device, OS, or cloud platform**.
    

---

## 🔹 Containers vs Virtual Machines

|Feature|Virtual Machines|Containers|
|---|---|---|
|OS|Each VM has its **own full OS**|Share the **host OS kernel**|
|Resource Overhead|High (full OS per VM)|Low (lightweight)|
|Startup Time|Slow|Fast|
|Portability|Limited|High (run anywhere)|
|Isolation|Strong|Strong, but lighter|

- Analogy:
    
    - VM = Multiple houses, each with its own walls and utilities.
        
    - Container = Floors in a building sharing the same foundation but isolated individually.
        

---

## 🔹 Why Containerization is Useful

1. **Portability** → Runs uniformly across platforms.
    
2. **Efficiency** → Lightweight, shares OS kernel, fewer resources.
    
3. **Speed** → Fast startup times; ideal for microservices.
    
4. **Fault Isolation** → Problems in one container don’t affect others.
    
5. **Scalability** → Easy to scale individual services.
    
6. **Manageability** → Orchestration tools like **Kubernetes** automate deployments and scaling.
    
7. **Security** → Isolation and defined permissions help protect applications.
    

---

## 🔹 Key Takeaways

- Containers are **lightweight, portable, and efficient virtual environments**.
    
- Perfect for **microservices**, as each service can run in its own container.
    
- Unlike VMs, containers **share the host OS**, reducing overhead and startup time.
    
- Orchestration platforms like Kubernetes make **large-scale container management** easier.



# Docker commands
Absolutely! Let’s break down this Docker demo into **clear, organized points** so it’s easier to understand and remember.

---

## 🔹 Setting Up Docker

- **Docker installation**: Must have Docker installed locally, or you can use **OCI Cloud Shell** (pre-configured with Docker).
    
- **Check Docker version**:
    
    ```bash
    docker -v
    ```
    

---

## 🔹 Basic Docker Commands

### **1. Running a Container**

- Command:
    
    ```bash
    docker run <image_name>
    ```
    
- Example:
    
    ```bash
    docker run hello-world
    ```
    
    - Pulls image from Docker Hub if not present locally.
        
    - Prints a message (“Hello from Docker”).
        
- Check downloaded images:
    
    ```bash
    docker images
    ```
    

---

### **2. Managing Containers**

- **List running containers:**
    
    ```bash
    docker ps
    ```
    
- **List all containers (running + stopped):**
    
    ```bash
    docker ps -a
    ```
    
- **Remove a container:**
    
    ```bash
    docker rm <container_id_or_name>
    ```
    

---

### **3. Interactive Shell Access**

- Command:
    
    ```bash
    docker run -it busybox sh
    ```
    
- `-it` → interactive mode + pseudo-TTY
    
- Access shell inside the container:
    
    ```bash
    pwd       # check current directory
    ls        # list files
    exit      # exit the container
    ```
    
- Exiting with `exit` stops the container.
    
- Use **Ctrl + D** to exit the shell **without stopping the container**.
    

---

### **4. Running Containers in Detached Mode**

- Command:
    
    ```bash
    docker run -d -p <host_port>:<container_port> <image_name>
    ```
    
- `-d` → detached mode (runs in background)
    
- `-p` → maps host port to container port
    
- Example:
    
    ```bash
    docker run -d -p 80:80 nginx
    ```
    
    - Container runs NGINX server, port 80 accessible on host.
        
- Test connection using `curl` on mapped port.
    

---

### **5. Start, Stop, Restart**

- Start stopped container:
    
    ```bash
    docker start <container_id>
    ```
    
- Stop running container:
    
    ```bash
    docker stop <container_id>
    ```
    
- Restart container:
    
    ```bash
    docker restart <container_id>
    ```
    

---

### **6. Inspecting Containers**

- **Check container port mapping:**
    
    ```bash
    docker port <container_id>
    ```
    
- **View logs:**
    
    ```bash
    docker logs <container_id>
    ```
    
- **Detailed container info:**
    
    ```bash
    docker inspect <container_id>
    ```
    
    - Shows image, state, CPU, memory, network, and storage info.
        
- **View top processes in a container:**
    
    ```bash
    docker top <container_id>
    ```
    
- **Execute commands inside running container:**
    
    ```bash
    docker exec -it <container_id> sh
    ```
    
    - Gives interactive shell inside a running container.
        

---

## 🔹 Key Takeaways

1. **Images vs Containers**
    
    - Image → template
        
    - Container → running instance
        
2. **Interactive vs Detached Mode**
    
    - Interactive → `-it`, for shell access
        
    - Detached → `-d`, runs in background
        
3. **Container Management**
    
    - `docker ps`, `docker ps -a`, `docker rm`
        
    - `docker start`, `docker stop`, `docker restart`
        
4. **Inspect & Logs**
    
    - Monitor container performance, network, storage, and logs.
        
5. **Port Mapping**
    
    - Map container ports to host ports to expose services.
        

✅ **In short:** Docker lets you **run, manage, and monitor containers efficiently** using simple commands, making it easier to develop and deploy applications in isolated, portable environments.

---

If you want, I can make a **diagram showing all these commands and their effect on container lifecycle**—from pulling an image to starting, stopping, and inspecting a container.

Do you want me to make that diagram?

![[Pasted image 20250828110712.png]]


