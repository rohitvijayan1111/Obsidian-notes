
![[Pasted image 20250515163344.png]]



## **1. Introduction to Consistent Hashing**

### 🔹 What is Consistent Hashing?

- A **technique used in distributed systems** to distribute data (e.g., requests, objects, keys) across multiple nodes (e.g., servers) **in a scalable and fault-tolerant way**.
    
- Helps solve **load balancing issues** while maintaining **request stickiness** and **minimizing changes** when servers are added or removed.
    

---

## **2. Context: Server and Client Model**

### 🔸 Scenario

- You develop an algorithm (e.g., facial recognition).
    
- A client accesses it over the internet.
    
- Each time they make a request, they expect a **fast, consistent response**.
    

### 🔸 Terminology

- **Client:** The user's device (e.g., mobile).
    
- **Server:** The machine that runs your algorithm and serves the requests.
    

---

## **3. Problem: Scaling**

### 🔸 Initial Situation

- Your server gets popular → receives many requests.
    
- A single server can’t handle it all.
    

### 🔸 Solution

- Add more servers to distribute the load.
    

---

## **4. Load Balancing**

### 🔸 What is Load Balancing?

- Evenly distributing the incoming **requests (load)** across all available servers.
    
- Ensures **no single server is overwhelmed**.
    

### 🔸 Approach Using Hashing

- Each request has a **Request ID** (e.g., R1, R2).
    
- Use a **hash function** `H()` to convert this request ID into a number.
    
- Use modulo operation to assign it to a server:
    
    mathematica
    
    CopyEdit
    
    `H(R) % N = server_index`
    
    Where `N` is the number of servers.
    

### 🔸 Example

- Assume 4 servers: S0, S1, S2, S3.
    
- Request ID `R1 = 10`
    
    - `H(R1) = 3 → 3 % 4 = 3 → Goes to Server 3 (S3)`
        
- Request ID `R2 = 20`
    
    - `H(R2) = 15 → 15 % 4 = 3 → Also goes to Server 3 (S3)`
        
- Request ID `R3 = 35`
    
    - `H(R3) = 12 → 12 % 4 = 0 → Goes to Server 0 (S0)`
        

### 🔸 Expected Outcome

- If the hash function is uniformly random, load is distributed **evenly**.
    
- Load per server ≈ Total requests ÷ Number of servers.
    

---

## **5. Problem: Adding New Servers**

### 🔸 What Happens When You Add a Server?

- You now have 5 servers.
    
- `H(R) % 5` changes the destination of many requests.
    
- **Almost all requests get reassigned** to different servers.
    

### 🔸 Why This is a Problem

- Requests are **not random**; often tied to a **User ID**.
    
- You want a user to always hit the **same server** (request stickiness).
    
- Each server may cache user-specific data.
    
- If requests get remapped:
    
    - All cache is lost (wasted).
        
    - System performance suffers.
        
    - Expensive recomputation needed.
        

---

## **6. Visual Explanation: Pie Chart View**

### 🔸 Old Hashing (Without Consistent Hashing)

- Servers cover equal ranges of the hash space (e.g., 0–99 split into 25 each).
    
- When a new server is added:
    
    - Existing servers lose a chunk of their hash range.
        
    - **Many mappings (buckets) change**.
        
    - Nearly **100% of the space is remapped**.
        

### 🔸 Why Bad?

- Huge overhead: remapping requests, moving cached data.
    
- Violates request stickiness.
    

---

## **7. The Need for Consistent Hashing**

### 🔸 Goal

- When a new server is added:
    
    - **Only a few keys** (hash ranges) should move to the new server.
        
    - Other requests should continue being handled by the same servers.
        

### 🔸 Ideal Situation (New Hashing with Consistent Hashing)

- Pie is divided such that:
    
    - Each server keeps most of its range.
        
    - Only a **small portion** from each existing server is moved to the new one.
        
    - Change is **minimal but sufficient** to balance the load.
        

---

## **8. Benefits of Consistent Hashing**

|Feature|Description|
|---|---|
|🔁 **Minimal Change**|Only a few keys move when a node is added or removed.|
|📊 **Balanced Load**|Distributes load evenly among servers (with proper virtual nodes).|
|🔄 **Scalability**|Easily add/remove nodes without heavy data reshuffling.|
|💾 **Request Stickiness**|Requests for the same user go to the same server, enabling caching.|

---

## **9. Key Takeaways**

- Hashing + Modulo works only when the number of servers doesn't change.
    
- Naive load balancing causes huge changes when servers are added.
    
- **Consistent Hashing is a smarter way**:
    
    - Adds stability to key-server mapping.
        
    - Keeps cache valid longer.
        
    - Reduces load during scale operations.


---
>Notes to self:
* Load balancing distributes requests across servers.
* You can use `hash(r_id) % n_servers` to get the server index for a request `r_id`.
    -> Drawback: if you add an extra server `n_servers` changes and `r_id` will end up on a different server. This is bad because often we want to map requests with the same ids consistently to the same servers (there could e.g. be cached data there that we want to reuse).
* "Consistent hashing" hashes with a constant denominator `M`, e.g. `hash(r_id) % M`, and then maps the resulting integer onto a server index. Each server has a range of integers that map to their index.
* The pie example demonstrates, that if an extra server is added, the hashing function stays the same, and one can then change the range-to-server-index mapping slightly so that it remains likely that an `r_id` gets mapped to the same server as before the server addition.


>For anyone confused by the pie chart, the explanation he does makes sense only when you watch the whole video. In a nutshell, when you at first have 4 servers, each server handles 25% of the users. The hashing function takes users' user id or some other information that somehow encapsulates the user data (and is consistent) so any time you want to, for example, fetch a user profile you do it via the same server over and over again since user id never changes (therefore hash of a user id never changes and will always point to the same server). The server remembers that and it creates a local cache for that information for that user so that it doesn't have to execute the (expensive) action of calculating user profile data, but instead just fetches it from the local cache quickly instead. Once your userbase becomes big enough and you require more processing power you will have to add more servers. Once you add more servers to the mix, the user distribution among server will change. Like in the example from the video, he added one server (from 4 servers to 5 servers). Each server needs to now handle 20% of the users. So here is where the explanation for the pie chart comes from.

>Since the first server s0 handles 25% of the users, you need to take that 5% and assign it to 2nd server s1. The first server s0 no longer serves the 5% of the users it used to, so the local cache for those users becomes invalidated (i.e. useless, so we need to fetch that information again and re-cache it on a different server that is now responsible for those users). Second server s1 now handles 25%+5%=30% of the traffic, but it needs to handle 20%. We take 10% of its users and assign it to the third server s2. Again like before, the second server s1 lost 10% of its users and with it the local cache for those users' information becomes useless. Those 10% of users become third server's users, so the third server s2 handles 25%+10%=35% of the traffic. We take third server's 15% (remember, it needs to handle only 20%) and give it to the fourth server s3. Fourth server now handles 25%+15%=40% of the traffic. Like before, fourth server lost 20% of its users (if we're unlucky and careless with re-assignment of numbers it lost ALL of its previous users and got all other servers' users instead) and therefore those 20% of users' local cache becomes useless adding to the workload of other servers. Since fourth server handles 40% of the traffic, we take 20% of its users and give it to the new fifth server s4. Now all servers handle users uniformly but the way we assigned those users is inefficient. So to remedy that, we need to look at how to perform our hashing and mapping of users better when expanding the system.

----

# Consistent Hashing

---

## 🧠 **What Problem Are We Solving?**

### ❌ The Problem with Normal Hashing

Suppose you have some **servers (S1, S2, S3, S4)** and you want to distribute **requests (users, cache keys, database shards, etc.)** among them. A naive way would be:

```python
server_index = hash(request_id) % number_of_servers
```

But here's the **problem**:

- If you **add** or **remove** a server, the value of `number_of_servers` changes.
    
- This changes the result of the modulo operation.
    
- **Almost all request mappings will change**, even if only **one server** was added or removed.
    

💥 So, one change in infrastructure = major data reshuffling. **This is inefficient and breaks cache locality**.

---

## ✅ **Solution: Consistent Hashing**

Consistent hashing solves this problem by **minimizing the number of requests that get remapped when servers are added or removed**.

### 🌐 Imagine a Ring

Instead of mapping hashes into an array, we map them onto a **circular ring**:

- Imagine numbers from `0` to `M - 1` arranged in a **circle**.
    
- Both servers and requests are **hashed** onto this ring.
    
- Hash(request ID) and Hash(server ID) → both are mapped to positions on the ring.
    

> The range is 0 to `M-1`, where `M` is a large number (say 2³²).

---

## 🔄 **Mapping Requests to Servers**

Now, how do we assign a request to a server?

1. Hash the **request ID** → gives a position on the ring.
    
2. Go **clockwise** on the ring until you find the **first server**.
    
3. Assign the request to that server.
    

**Example:**

- Request hash = 25
    
- Servers are at positions: 10 (S1), 30 (S2), 50 (S3)
    
- Go clockwise from 25 → nearest is 30 → request goes to S2
    

✅ Only nearby values are impacted when a server is added/removed!

---

## 🔁 **Adding or Removing Servers**

Let’s say:

- You add a new server at position 27.
    
- Now, only the requests in the range **(25, 30)** will move to the new server.
    
- All others remain unchanged.
    

### 🔁 If a Server is Removed:

- The requests that were going to it just go to the **next clockwise server**.
    
- Minimal movement, not all requests need to be remapped.
    

---

## 📈 Load Distribution and 1/N

You heard this in the video:

> “So the load factor turns out to be on average, expected 1/N.”

### ❓ What does that mean?

- Suppose you have `N` servers.
    
- If the hash function distributes requests **uniformly**, then each server should get **1/N of the total load**.
    
- This is an **expected value**—the statistical average across time and many requests.
    

However, this assumes:

- The hash function is good.
    
- The distribution of request IDs is uniform.
    

---

## ⚠️ Real-World Problem: Skewed Distribution

When you have **only a few servers**, even if you hash things nicely, the positions on the ring **might cluster** or be uneven.

### 🎯 Example:

Imagine only 4 servers on a 0 to 100 hash ring:

- Server hashes: 10, 20, 90, 95
    
- Lots of space between 20 and 90 → that one server between them gets overloaded.
    

So, even if you expect 1/N load, in reality, one server might get **50%** or more!

---

## 💡 Solution: Virtual Nodes (a.k.a. Virtual Servers)

To fix this **skewed load**, we use **virtual nodes**.

### 🎯 Concept:

- Each physical server is represented **multiple times** on the ring.
    
- Use **K hash functions** to map a server to **K different positions** on the ring.
    
- Each of these is a **virtual node**.
    

### 🧮 Technical Details:

- If you have `N` servers and you use `K` virtual nodes per server, you have `N * K` points on the ring.
    
- Now the distribution is much smoother.
    
- Each virtual node still handles ~1/(N * K) of the load.
    
- Each **physical server** handles **K times that**, so still **~1/N**, but with much less variation.
    

---

### ✅ Example:

Let’s say:

- 4 servers: S1, S2, S3, S4
    
- K = 3 (3 virtual nodes per server)
    
- Now the ring has **12 total server points**, much denser and more uniform.
    

If you remove one server (S1), you remove **3 virtual points**, not one big gap.

- Load from those 3 small regions is distributed among neighboring nodes.
    
- The **impact is spread**, avoiding large jumps in load.
    

---

## 💼 Applications of Consistent Hashing

This is used in real-world systems like:

- **CDNs** and **Web Caches**: like Varnish, Akamai, or Cloudflare
    
- **Distributed Databases**: Cassandra, DynamoDB, Couchbase
    
- **Load Balancers**
    
- **Key-Value Stores**: Redis Clusters, Memcached
    

---

## 🧠 Summary

|Concept|Description|
|---|---|
|**Problem**|Adding/removing servers remaps most data|
|**Consistent Hashing**|Maps data and servers on a ring to minimize movement|
|**Request Mapping**|Find nearest clockwise server from request hash|
|**Expected Load per Server**|~1/N, where N = number of servers|
|**Skewed Distribution**|Happens when few servers are unevenly placed|
|**Virtual Nodes**|Each server has multiple points (K hash functions) to smooth out load|
|**Effect of Virtual Nodes**|Load becomes uniformly spread, minimal reallocation on changes|

---

## 📌 Key Technical Takeaways

- **Consistent Hashing** ensures minimal data movement.
    
- **Hash range**: typically 0 to 2³² or 2⁶⁴.
    
- **Load factor**: Expected load on each server ≈ 1/N.
    
- **Virtual nodes**: Used to deal with uneven hash distribution.
    
- **K = log N or log M**: Common choice for number of virtual nodes per server.
    
- **Uses**: Caching, Sharding, Load Balancing, Distributed File Systems.
    

---

Exactly — you're **100% on the right track**.

Let’s break this down **technically and operationally** so you can picture how the **load balancer** fits into the **consistent hashing** mechanism.

---

## ✅ YES — This logic is **inside** the Load Balancer

The **load balancer** is the component (or service) that:

- Receives incoming requests
    
- Hashes the request (usually based on a key like user ID, file ID, session ID, etc.)
    
- Finds the correct server (or node) using **consistent hashing on a ring**
    
- Routes the request to that server
    

---

## ⚙️ Step-by-Step: What the Load Balancer Does

Let’s walk through it in order.

---

### 🔹 **Step 1: Incoming Request**

A user makes a request:

- Example: `GET /user/48953/profile`
    
- The key used for hashing might be: `"48953"` (user ID)
    

---

### 🔹 **Step 2: Hash the Key**

The load balancer computes:

```python
hash("48953") % M = position_on_ring
```

This gives a **position on the consistent hash ring**.

---

### 🔹 **Step 3: Go Clockwise on the Ring**

Now the load balancer:

- Starts at `position_on_ring`
    
- Moves **clockwise** on the ring to find the first server ≥ that position
    

That server is now the **owner** of this request.

---

### 🔹 **Step 4: Route the Request**

The load balancer forwards the request to that server over:

- HTTP/HTTPS
    
- gRPC
    
- TCP
    
- or any protocol in use
    

### Example:

If `hash("48953") % 2^32 = 2,345,678,901`, and you have servers at:

```
Server A → 1,000,000,000
Server B → 2,000,000,000
Server C → 3,000,000,000
```

Then:

- `2,345,678,901` maps to Server C (first server clockwise after 2.3B)
    
- So the load balancer routes the traffic to **Server C**
    

---

## 📦 Internally: The Load Balancer Maintains

1. A **map** of virtual nodes → real servers  
    (Especially if using virtual nodes with multiple hash positions per server)
    
2. A **sorted list** (or data structure like a TreeMap or Red-Black Tree) of server positions on the ring  
    → So it can efficiently find the next node clockwise
    
3. **Health checks** to know which servers are online or down  
    → If one goes down, remove its virtual nodes from the ring
    

---

## 🧠 Why This Design Is Great for Scalability

✅ **Minimum disruption** when a server is added or removed  
✅ **No need to remap all requests** like in naive modulo hashing (`hash % N`)  
✅ **Smooth scaling** and **fault tolerance**

---

## 🔁 And Yes — It’s Used in Practice

Big systems like:

- Amazon DynamoDB
    
- Apache Cassandra
    
- Netflix EVCache
    
- Akamai CDN
    
- Memcached clients (e.g., Ketama)
    

...use this exact strategy with consistent hashing in their load balancers or clients.

---

## 💡 TL;DR Summary

|Component|Role|
|---|---|
|Load Balancer|Maintains the hash ring, maps requests to servers|
|Request Key|Hashed into a point on the ring|
|Server Positions|Also hashed into the ring|
|Routing Logic|Move clockwise to find nearest server|
|Outcome|Request is forwarded to that server|

---

Would you like a Python code example of how this works in a simplified way? Or a diagram showing request → ring → server path?

