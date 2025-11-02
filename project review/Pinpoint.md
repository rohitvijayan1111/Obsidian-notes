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
    
- **Device Status API** – Checks device connectivity to decide whether to send **push notifications** (if online) or **SMS alerts** (if offline).
    

---

### **Platform Features**

- **AI-Generated Campaign Posters** – Custom posters created using HTML templates.
    
- **Real-Time Push Notifications** – Alerts users with engaging offers and images.
    

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


