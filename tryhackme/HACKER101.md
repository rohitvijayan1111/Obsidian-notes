
- PYTHON
	- requests package


Must have tools:

- Burp proxy
- Firefox


![[Pasted image 20250901085706.png]]
![[Pasted image 20250901085727.png]]
 ![[Pasted image 20250901091638.png]]
 ![[Pasted image 20250901092633.png]]
 Got it 👍 Let’s break these request headers into **easy, real-world examples** so they’re more understandable:

---

### 1. **Host**

👉 Tells the server _which website_ you want to reach (important if many sites share the same server).  
🔹 Example:

```
Host: www.example.com
```

➡️ This means: “I want the site at [www.example.com.”](http://www.example.com.xn--ivg/)

---

### 2. **Accept**

👉 Tells the server _what kind of content_ your browser/app can handle.  
🔹 Example:

```
Accept: application/json
```

➡️ This means: “Please give me data in JSON format.”  
(If missing, the server often defaults to HTML.)

---

### 3. **Cookie**

👉 Passes along your saved info, like login sessions or preferences.  
🔹 Example:

```
Cookie: sessionId=abc123; theme=dark
```

➡️ This means: “Here’s my login session and I like dark mode.”

---

### 4. **Referer** (misspelled in HTTP as "Referer")

👉 Tells the server the page you came from.  
🔹 Example:

```
Referer: https://www.google.com/
```

➡️ This means: “I clicked a link on Google to get here.”

(_Note_: not always sent when using HTTPS for privacy reasons.)

---

### 5. **Authorization**

👉 Proves your identity to access protected resources.  
🔹 Example:

```
Authorization: Basic YWRtaW46cGFzc3dvcmQ=
```

➡️ This means: “Here’s my username and password, encoded.”  
(Servers decode it back to `admin:password`.)

---

⚡ Think of headers like a **package label** on an online order — they tell the delivery company (server) where it’s going, what’s inside, and who it belongs to.

---

