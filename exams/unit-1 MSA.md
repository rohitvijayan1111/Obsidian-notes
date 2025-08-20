
- aggregate pattern
- chained
- decomposition
- branch

Types:
- api gateway
- database per services
- service discovery
- SAGA
- circuit breaker
- event sourcing



# SAGA

Got it 👍 Let’s break down the **SAGA Pattern** in a simple, step-by-step way so it’s easy to understand.

---

## 🔹 What is the SAGA Pattern?

The **SAGA Pattern** is a design pattern for managing **distributed transactions** (when a business process spans multiple microservices or databases).

Since distributed systems can’t use traditional **ACID transactions** across services (too slow, complex, or impossible), SAGA provides a way to maintain **data consistency** using a series of **local transactions** and **compensating actions** if something fails.

👉 Think of it as:

- Break one big transaction into smaller steps (local transactions).
    
- If one step fails, undo the previous steps with compensating actions (like an "undo" function).
    

---

## 🔹 Example to Keep in Mind

Imagine you’re booking a trip:

1. Book flight ✈️
    
2. Book hotel 🏨
    
3. Reserve taxi 🚕
    

If hotel booking fails, the system needs to **cancel the flight reservation** to keep things consistent. That’s SAGA.

---

## 🔹 [Types of SAGA Pattern ](https://medium.com/cloud-native-daily/microservices-patterns-part-04-saga-pattern-a7f85d8d4aa3)

There are **two main types**:

### 1. **Choreography-based Saga (Event-driven)**

- Each service **listens** for events and **publishes events** when it completes a local transaction.
    
- No central controller. Services "dance" together like choreography.
    

✅ **Flow Example (Trip Booking):**

1. **Flight Service** books flight → emits event _"FlightBooked"_.
    
2. **Hotel Service** listens for _"FlightBooked"_, books hotel → emits event _"HotelBooked"_.
    
3. **Taxi Service** listens for _"HotelBooked"_, reserves taxi → emits event _"TaxiBooked"_.
    

❌ If hotel booking fails:

- Hotel Service emits _"HotelBookingFailed"_.
    
- Flight Service listens and cancels flight.
    

🔹 **Pros:**

- Simple for small systems.
    
- No central point of failure.
    
- Natural event-driven flow.
    

🔹 **Cons:**

- Hard to monitor/debug.
    
- Workflow logic is scattered across services.
    
- Risk of "event storming" (too many events flying around).
    

---

### 2. **Orchestration-based Saga (Centralized control)**

- A **central orchestrator** (like a conductor in an orchestra 🎼) tells each service what to do.
    
- Services don’t listen for events, they just perform tasks when told.
    

✅ **Flow Example (Trip Booking):**

1. **Orchestrator** sends command: _"BookFlight"_ → Flight Service does it → replies back.
    
2. **Orchestrator** sends command: _"BookHotel"_ → Hotel Service tries.
    
3. If Hotel fails → Orchestrator sends command to Flight Service: _"CancelFlight"_.
    

🔹 **Pros:**

- Centralized control → easier to monitor and debug.
    
- Business logic in one place.
    
- Easier error handling.
    

🔹 **Cons:**

- Orchestrator can become a bottleneck.
    
- Single point of failure.
    
- Less loosely coupled than choreography.
    

---

## 🔹 Quick Comparison

| Feature         | Choreography Saga            | Orchestration Saga             |
| --------------- | ---------------------------- | ------------------------------ |
| **Control**     | Decentralized (event-driven) | Centralized (orchestrator)     |
| **Complexity**  | Harder to monitor            | Easier to monitor              |
| **Scalability** | High (no central brain)      | Can bottleneck at orchestrator |
| **Use Case**    | Simple workflows             | Complex workflows              |

---

## 🔹 When to Use Which?

- **Choreography**:
    
    - Simple processes with few services.
        
    - High scalability needed.
        
    - Event-driven systems.
        
- **Orchestration**:
    
    - Complex workflows with many steps.
        
    - Easier error handling and monitoring required.
        
    - Clear central authority makes sense.
        

---

✅ In short:

- **Choreography Saga** = Event-driven, services react to each other.
    
- **Orchestration Saga** = A boss (orchestrator) tells services what to do.
    

---

Would you like me to also **draw a simple diagram (flow chart)** of both types so it’s more visual and easier to remember?




# [Deployment models](https://dennylesmana.medium.com/microservices-deployment-patterns-ca1343c89e13)
- single service per host
- multiple service per host
- service instance per VM
- service instance per Container
- Serverless
- A/B Testing
- Canary deployment
- Blue Green deployment

