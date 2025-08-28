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

