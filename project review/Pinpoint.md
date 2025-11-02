## **Pinpoint: AI-Powered Hyperlocal Marketing Platform**

**Powered by Nokia’s NAC and IBM watsonx Orchestrator**

---

### **Problem Statement / Use Case**

Imagine walking past a bakery offering **20% off today**, but you never find out — their visibility disappears the moment you walk by.

Local businesses often face this issue — they lack affordable and effective ways to reach nearby customers. Running ads on platforms like Google or Meta can be costly and inefficient for small businesses. As a result, both **consumers miss out on nearby deals**, and **local business owners lose potential customers**.

---

### **Solution Overview**

**Pinpoint** bridges this gap by connecting local businesses with nearby consumers in real time using AI and hyperlocal technology.

- **For Shop Owners:**  
    They register their store on the platform, add their products, and create promotional campaigns to attract nearby customers.
    
- **For Consumers:**  
    Once they onboard, users receive **real-time notifications** about relevant offers from shops **within their vicinity** — powered by dynamic geofencing.
    

---

### **Unique Geofencing Innovation**

Traditionally, geofences are created **around shops**, and notifications are sent to users who have subscribed to those areas — which limits reach.

**Pinpoint reverses this logic:**  
We create **geofences around users instead of shops**. This means that as users move, they receive notifications from nearby shops **without needing prior subscriptions**, ensuring **maximum visibility** for local businesses.

---

### **Nokia NAC APIs Utilized**

- **Location Retrieval API** – Fetches precise user and shop locations.
    
- **Geofence API** – Triggers events when users enter or exit a defined zone.
	- Creation:
		- to the api, pass the mobile no, lat and long of the user and the radius
	 - Retrival : via subscription id

- Location Verification API-
	- ```
	  def verify_location_nokia(phone_number: str, lat: float, lon: float, timestamp: str = None, radius: float = 50000) -> bool:

	  ```
    
- **Device Status API** – Checks device connectivity to decide whether to send **push notifications** (if online) or **SMS alerts** (if offline).
    

---

### **Platform Features**

- **AI-Generated Campaign Posters** – Custom posters created using HTML templates.
    
- **Real-Time Push Notifications** – Alerts users with engaging offers and images.
- Recommendation Feature: to get the best possible shop/ product with available money/location
    

---

### **Integration with IBM watsonx Orchestrator**

When a shop owner creates a campaign, **watsonx Orchestrator** coordinates multiple specialized AI agents to automate and optimize the process.

#### **Master Agent**

- Manages and orchestrates sub-agents for poster creation, text generation, review analysis, and personalization.
    

#### **Poster Agents (A & B)**

- Receive campaign details such as title, offer, and shop information.
    
- Generate **HTML-based poster designs**, which are then converted into image snapshots and stored in the backend.
    

#### **Push Notification Agent**

- Creates **catchy and personalized notification texts**, similar to Swiggy or Zomato’s style.
    
- Combines the generated text with the campaign image URL and delivers it to users via **Firebase Cloud Messaging (FCM)**.
    

#### **Review Analysis Agent**

- Performs **sentiment analysis** on customer feedback.
    
- Categorizes reviews as positive or negative and identifies **key topics** such as _pricing, service, quality, and ambiance_.
    
- Detects **complaint trends** and satisfaction drivers for businesses.
    

#### **Personalization Agent**

- Analyzes user preferences and engagement history.
    
- Scores and ranks campaigns based on the user’s recent interests.
    
- Pushes **personalized offers** with the highest relevance scores to the user.
    

---

### **Summary**

Pinpoint leverages **Nokia’s advanced network capabilities** and **IBM watsonx’s AI orchestration** to empower local businesses with affordable, automated, and hyper-targeted marketing — ensuring that **no great offer goes unnoticed**.




# Nokia NAC

This Python script is a **helper module for integrating with Nokia’s Network-as-Code APIs via RapidAPI**.  
It allows you to perform advanced **telecom network operations**, such as **geofencing, SIM swap detection, and location verification**, by calling Nokia’s telecom APIs from your backend.

Let’s go step-by-step 👇

---

## 🧩 1. Setup and Configuration

```python
import os
import json
import requests
import certifi
```

These imports allow:

- `os` → access to environment variables (for secrets)
    
- `json` → JSON encoding/decoding
    
- `requests` → make HTTPS API calls
    
- `certifi` → provides SSL certificates for secure HTTPS connections
    

---

### Environment Configuration

```python
NOKIA_BASE_URL = os.getenv("NOKIA_BASE_URL", "https://network-as-code.p-eu.rapidapi.com")
NOKIA_RAPIDAPI_KEY = os.getenv("NOKIA_RAPIDAPI_KEY")
NOKIA_RAPIDAPI_HOST = os.getenv("NOKIA_RAPIDAPI_HOST", "network-as-code.nokia.rapidapi.com")
```

- These variables are loaded from your environment (so you don’t hardcode API keys).
    
- If not provided, it uses default Nokia API endpoints.
    

Then headers are defined for each request:

```python
HEADERS = {
    "x-rapidapi-key": NOKIA_RAPIDAPI_KEY,
    "x-rapidapi-host": NOKIA_RAPIDAPI_HOST,
    "Content-Type": "application/json"
}
```

---

## 📍 2. Geofencing APIs

### a. Create a Geofence Subscription

```python
def create_geofence_subscription(phone_number: str, lat: float, lon: float, radius: int = 2000):
```

This function **creates a geofencing event subscription** — it tells Nokia’s system to **monitor if a device (phone number)** enters or leaves a given circular area.

It sends this payload:

```python
payload = {
    "protocol": "HTTP",
    "sink": "http://192.168.1.11:5000/api/geofence/callback",
    "types": ["org.camaraproject.geofencing-subscriptions.v0.area-left"],
    "config": {
        "subscriptionDetail": {
            "device": {"phoneNumber": phone_number},
            "area": {
                "areaType": "CIRCLE",
                "center": {"latitude": lat, "longitude": lon},
                "radius": radius
            }
        },
        "initialEvent": True,
        "subscriptionMaxEvents": 10,
        "subscriptionExpireTime": "2045-03-22T05:40:58.469Z"
    }
}
```

- `sink` → your callback URL (Nokia sends an HTTP POST when the event triggers)
    
- `types` → defines when the event triggers (here, when **leaving the area**)
    
- `initialEvent` → triggers once right after creation (optional)
    
- `subscriptionMaxEvents` → how many times it can trigger before expiring
    
- `subscriptionExpireTime` → expiry date
    

📤 Makes a POST request to:

```
/geofencing-subscriptions/v0.3/subscriptions
```

---

### b. Retrieve Geofence Subscription

```python
def retrieve_geofence_subscription(subscription_id: str):
```

Fetches details of an existing geofencing subscription using its ID.

📤 GET request to:

```
/geofencing-subscriptions/v0.3/subscriptions/{subscription_id}
```

---

### c. Delete Geofence Subscription

```python
def delete_geofence_subscription(subscription_id: str):
```

Deletes an existing geofencing subscription.

📤 DELETE request to:

```
/geofencing-subscriptions/v0.3/subscriptions/{subscription_id}
```

---

### d. List All Geofencing Subscriptions

```python
def list_geofence_subscriptions():
```

Lists all current geofencing subscriptions for your account.

📤 GET request to:

```
/geofencing-subscriptions/v0.3/subscriptions
```

---

## 📡 3. Location Verification

```python
def verify_location_nokia(phone_number: str, lat: float, lon: float, timestamp: str = None, radius: float = 50000) -> bool:
```

This checks **if a phone is (or was recently) inside a specific geographic area**.

📤 POST to:

```
/location-verification/v1/verify
```

Payload example:

```json
{
  "device": {"phoneNumber": "+919876543210"},
  "area": {
    "areaType": "CIRCLE",
    "center": {"latitude": 12.9716, "longitude": 77.5946},
    "radius": 50000
  }
}
```

✅ Returns `True` if the user was in that area, `False` otherwise.

---

## 📲 4. SIM Swap Check

Used for **fraud prevention** or **identity verification**.

### a. Check SIM Swap Status

```python
def check_sim_swap(phone_number: str, max_age: int = 240):
```

Checks whether a **SIM card linked to a phone number** was swapped within the last `max_age` hours.

📤 POST to:

```
/passthrough/camara/v1/sim-swap/sim-swap/v0/check
```

If recently swapped, it may indicate **fraud** (like number porting attacks).

---

### b. Retrieve SIM Swap Date

```python
def retrieve_sim_swap_date(phone_number: str):
```

Gets the **exact date/time of the last SIM swap** for a given phone number.

📤 POST to:

```
/passthrough/camara/v1/sim-swap/sim-swap/v0/retrieve-date
```

---

## 🗺️ (Commented Out) — Retrieve Device Location

The commented-out function:

```python
# def get_device_location(phone_number: str):
```

Would retrieve a phone’s **current or last known location**, but it’s disabled — probably due to needing specific API access or higher-level permissions.

---

## ⚙️ Summary Table

|Function|Purpose|API Endpoint|
|---|---|---|
|`create_geofence_subscription`|Set up event trigger for when user leaves area|`/geofencing-subscriptions/.../subscriptions`|
|`retrieve_geofence_subscription`|Fetch details of a subscription|`/geofencing-subscriptions/.../{id}`|
|`delete_geofence_subscription`|Remove a subscription|`/geofencing-subscriptions/.../{id}`|
|`list_geofence_subscriptions`|List all active geofences|`/geofencing-subscriptions/.../subscriptions`|
|`verify_location_nokia`|Check if device is within an area|`/location-verification/v1/verify`|
|`check_sim_swap`|Detect recent SIM swap|`/sim-swap/v0/check`|
|`retrieve_sim_swap_date`|Get timestamp of last SIM swap|`/sim-swap/v0/retrieve-date`|

---

## 💡 Practical Use Cases

- **Delivery apps:** confirm delivery agent stays within zone
    
- **Banking/Fintech:** detect SIM swap before OTP login
    
- **Telecom apps:** trigger alert when user moves outside defined region
    
- **Security systems:** geofencing alerts for specific personnel or assets
    

---

Would you like me to show how to **integrate this file into a Flask API backend** (so you can receive Nokia geofence callbacks and trigger business logic)?