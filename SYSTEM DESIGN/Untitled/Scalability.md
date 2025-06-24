
- Horizontal scaling 
- vertical scaling


# DNS Server

- this could also help traffic equally

LOAD Balancing

- could split traffic based on cpu usage
- or dedicate some service to a instance and traffic all the request to it accordingly 




HOW WOULD TRAFFIC THE USER TO THE SAME INSTANCE VIA THE LOAD BALANCER:

ISSUE: the user might need to login again and again , as the session cookie might not be stored in the other instances. OR The user might have added the things to carts in one instance , some in the other, this becomes difficult 


SOLUTION:
- Storing it in the load balancer itself or somewhere else
- COULD ASSIGN RANDOM ID TO THE SERVER AND STORE IT IN THE COOKIE OF THE USER, THE LOADBALANCER WILL DIRECT THE TRAFFIC TO THE RIGHT USER , BASED ON THE ID
  

SUPPOSE THE ELB IS THE ONE STORING EVERTHING = HOW DO WE ENSURE THE DATA ISNT LOST
RAID
RAID1
RAID5
RAID6
RAID10




CACHING


- MY SQL QUERY CACHE ->
- MEMCACHE->


WHAT TO DO IF THE CACHE IS GETTING FULL
- TRY TO DISCARD THE ONE THAT IS OLD AND LESS RECENTLY USED



DATABASE REPLICATION:

- HAVE ONE MASTER AND CREATE REPLICA OF THE SLAVES
- so an write query hits the master, it is copied down to all others
- so thereby IT CAN BE USED AS A LOAD BALANCING FOR READ REQUEST



- USE TWO MASTER SERVERS


![[Pasted image 20250606211531.png]]


WHAT IF THE LOAD BALANCER DIES (SINGLE POINT OF FAILURE)


ADD EXTRA LOAD BALANCER AND PARTITION 

![[Pasted image 20250606212843.png]]




# Scalability of application servers
---

### 🔑 **Scalability Golden Rule**

- **Consistency across servers**: Every server must serve **exactly the same codebase** and must not store any **user-related state** (e.g., sessions, profile pictures) locally.
    
- This ensures **Steve** (or any user) gets the **same result** regardless of the server he "lands on."
    

---

### 🗂️ **Session Management**

- **Problem**: Local session storage leads to inconsistent user experience.
    
- **Solution**: Use a **centralized session store** accessible by all servers.
    
    - Options:
        
        - ✅ **External Database** – reliable but potentially slower
            
        - ✅ **External Persistent Cache (e.g., Redis)** – faster, designed for quick session access
            
- **External** = outside the application server, but **in or near** the data center.
    

---

### 🚀 **Deployment Consistency**

- **Problem**: Some servers may run **outdated code** during deployments.
    
- **Solution**: Use tools like **Capistrano** to deploy the same code to **all servers at once**.
    
    - Capistrano is popular in the Ruby on Rails ecosystem but can be used elsewhere too.
        
    - Ensures **zero-downtime deployment** and uniformity.
        

---

### 🖥️ **Server Provisioning**

- After centralizing sessions and ensuring codebase uniformity:
    
    - Create an **Amazon Machine Image (AMI)** from a properly configured server.
        
    - Use this AMI as a **base image** to launch new instances.
        
    - After launching, just pull the **latest code** and you’re ready to go.
        

---

### ✅ **End Result**

- Horizontally scalable infrastructure with:
    
    - Identical, stateless app servers
        
    - Centralized session handling
        
    - Automated, consistent deployments
        
    - Reproducible infrastructure using AMIs
        

---

Let me know if you'd like this in visual format (like a diagram or flashcards) or if you want to continue with the rest of the “Scalability for Dummies” series.



# Scalability of databases

Here's a clear and concise explanation of **Scalability for Dummies – Part 2: Database**, broken down into digestible sections:

---

## 🚨 The Problem: The Database Bottleneck

After solving server-side scalability (Part 1), your app can handle many concurrent users — **until the database becomes the bottleneck**.

- Most likely, you're using **MySQL** (or similar relational DB).
    
- As your user base and data volume grow, database queries slow down and **eventually crash your system**.
    

---

## 🛣️ Two Paths Forward

### 🛤️ **Path #1: Stick with MySQL (and make it scale)**

- This path involves keeping MySQL and scaling it with **more complexity** over time.
    

#### 🔧 Techniques:

1. **Master-slave replication**
    
    - **Writes** go to the **master**.
        
    - **Reads** go to one or more **slaves** to reduce load.
        
2. **Upgrade hardware**
    
    - Add more **RAM** and CPU to your master DB.
        
3. **Hire a DBA**
    
    - A Database Administrator will help with:
        
        - **Sharding** (splitting data across DBs)
            
        - **Denormalization**
            
        - **SQL performance tuning**
            

#### ⚠️ Drawbacks:

- Gets **expensive** (specialist staff, hardware upgrades)
    
- Gets **complex** (replication lag, schema design issues)
    
- Gets **slower** to evolve (every new optimization takes longer)
    

---

### 🌐 **Path #2: Embrace Denormalization and NoSQL**

- This path encourages you to **stop using JOINs** in your queries and restructure your data early.
    

#### 🔄 Steps:

1. **Denormalize your schema**
    
    - Duplicate some data to avoid JOINs
        
    - Optimize for **read performance**
        
2. **Do JOINs in application code**
    
    - Fetch related records manually in your backend logic
        
3. **Switch to NoSQL (optional but encouraged)**
    
    - Examples: **MongoDB**, **CouchDB**
        
    - Built to scale horizontally and avoid JOINs by design
        

#### ✅ Benefits:

- More scalable and performant
    
- Easier to shard and distribute
    
- Less DB overhead as load increases
    

#### ⚠️ Warning:

- **Eventually**, even NoSQL databases will slow down due to frequent reads.
    
- At that point, you'll need a **caching layer** (e.g., Redis or Memcached) to offload hot data.
    

---

## 🧠 Takeaways

|Feature|Path #1: Traditional RDBMS|Path #2: Denormalized / NoSQL|
|---|---|---|
|Schema Design|Normalized, many JOINs|Denormalized, no JOINs|
|Scaling Strategy|Vertical + Replication + Sharding|Horizontal + Caching|
|Who Handles JOINs|Database|Application code|
|Maintenance Cost|High (DBAs, tuning, upgrades)|Moderate (early rework, then smooth)|
|Long-term Performance|Diminishing returns|Scales well with proper caching|

---

## 💡 Final Tip

- The **earlier** you move toward denormalization and a scalable data structure, the **less effort** it will take later.
    
- Choose the **right path** based on your application's future needs, team expertise, and growth expectations.
    

---

Would you like diagrams, flashcards, or code examples (e.g., SQL JOIN vs NoSQL-style data retrieval)?

Sure! Here's a **detailed explanation of each technical topic** discussed in _Scalability for Dummies – Part 2: Database_, so you get a **clear understanding of both paths** — whether you're scaling traditional RDBMS like MySQL or adopting NoSQL and denormalization.

---

## 📌 1. **Master-Slave Replication**

### 🧠 What is it?

A replication setup where:

- **Master** server handles all **write** operations (INSERT, UPDATE, DELETE).
    
- **Slave(s)** replicate the master's data and handle **read** operations (SELECT).
    
- The master  Writes the changes in a script file and the slaves continously looks for this changes and 
### ✅ Why it’s useful:

- Reduces **read load** on the master server.
    
- Increases **availability** and **fault tolerance**.
    

### ⚠️ Drawbacks:

- **Replication lag**: Slaves may lag slightly behind the master.
    
- Writes are still **centralized** — master becomes a bottleneck at high scale.
    

---

## 📌 2. **Denormalization**

### 🧠 What is it?

The process of **restructuring a relational database** to reduce the number of **JOINs** by **duplicating data** across tables or documents.

### 📝 Example:

Normalized:

```sql
SELECT orders.id, customers.name
FROM orders
JOIN customers ON orders.customer_id = customers.id;
```

Denormalized:

```json
{
  "order_id": 123,
  "customer_name": "Steve Rogers"
}
```

### ✅ Benefits:

- Faster **read queries** (no JOINs).
    
- Simplifies data access patterns.
    

### ⚠️ Trade-offs:

- More **storage used** (duplicated data).
    
- More complex **update logic** (need to update in multiple places).
    

---

## 📌 3. **SQL Tuning**

### 🧠 What is it?

Improving SQL query performance by optimizing:

- **Indexes**
    
- **Query structure**
    
- **Execution plans**
    

### ⚒️ Techniques:

- Add **indexes** on columns frequently used in `WHERE`, `JOIN`, `ORDER BY`.
    
- Avoid `SELECT *`, use only needed columns.
    
- Use **EXPLAIN** to analyze query execution.
    

### ⚠️ Challenge:

Tuning can get extremely complex for large schemas with heavy traffic and many JOINs.

---

## 📌 4. **Sharding**

### 🧠 What is it?

**Partitioning** your database horizontally by splitting your data across multiple databases or servers, called **shards**.

Each shard contains a **subset of the data**.

### 📝 Example:

- Shard 1 stores users with IDs 1–1000
    
- Shard 2 stores users with IDs 1001–2000
    

### ✅ Benefits:

- Increases performance and scalability.
    
- Helps avoid single-server bottlenecks.
    

### ⚠️ Drawbacks:

- Complex to implement and maintain.
    
- Requires application-level logic to route queries to the right shard.
    

---

## 📌 5. **Joins in Application Code**

### 🧠 What is it?

Instead of letting the database engine combine data across tables (`JOIN`), you:

- Query data from multiple sources
    
- Manually **combine them in your backend**
    

### 📝 Example (Node.js + MongoDB):

```js
const orders = await db.orders.find({ user_id: "123" });
const user = await db.users.findOne({ id: "123" });
return { ...user, orders };
```

### ✅ Benefits:

- Works well with NoSQL.
    
- Avoids costly JOIN operations.
    

### ⚠️ Trade-offs:

- More logic in your application code.
    
- Slightly more data fetching overhead.
    

---

## 📌 6. **NoSQL Databases (e.g., MongoDB, CouchDB)**

### 🧠 What is NoSQL?

Databases that **don’t rely on a strict relational schema** or JOINs. They support:

- Document stores (MongoDB)
    
- Key-value stores (Redis)
    
- Wide-column stores (Cassandra)
    

### ✅ Benefits:

- Highly **scalable** and **schema-less**.
    
- Easy to horizontally scale (sharding, replication).
    
- Fast for **read-heavy workloads**.
    

### ⚠️ Considerations:

- No JOINs — must denormalize.
    
- Consistency trade-offs (e.g., eventual consistency).
    
- Indexing and querying can still become a performance bottleneck.
    

that's the **NoSQL approach** using **denormalization** and **document embedding**. Instead of creating separate tables (or collections) for related data like `orders`, you embed them **within the parent document** — in this case, the `user` document.

---

## 📌 7. **Caching**

### 🧠 What is it?

A **fast-access layer** (typically in-memory) that stores frequently accessed data to reduce load on the main database.

### 🔧 Tools:

- **Redis**
    
- **Memcached**
    

### 📝 Example:

Instead of querying the database every time:

```js
// Try cache first
const cachedUser = redis.get(`user:123`);
if (cachedUser) return cachedUser;

// Fallback to DB
const user = await db.users.findOne({ id: 123 });
redis.set(`user:123`, user);
return user;
```

### ✅ Benefits:

- Greatly improves **response time**.
    
- Reduces load on primary database.
    

### ⚠️ Drawbacks:

- Cache **invalidation** is tricky.
    
- Data may be **stale** if not managed properly.
    

---

## Summary Table

|Topic|Description|Benefits|Drawbacks|
|---|---|---|---|
|Master-Slave Replication|Reads from slaves, writes to master|Load balancing, redundancy|Write bottleneck, replication lag|
|Denormalization|Duplicate data, avoid JOINs|Faster reads|Data inconsistency, more storage|
|SQL Tuning|Optimize queries and indexes|Better performance|Complex and time-consuming|
|Sharding|Split DB horizontally|Infinite horizontal scaling|Complex logic, operational overhead|
|Joins in App Code|Manually combine data|Works with NoSQL, avoids JOINs|More backend logic|
|NoSQL|Schema-less, horizontally scalable DBs|Flexibility, easy scaling|No JOINs, eventual consistency|
|Caching|In-memory store for frequently accessed data|Super fast, reduces DB load|Invalidation complexity|

---

Would you like to go further into **NoSQL vs RDBMS use cases**, **how to design a denormalized schema**, or build a small demo to see these in action?