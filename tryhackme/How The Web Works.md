

# DNS


Absolutely! Let's break down the **working of DNS (Domain Name System)** in a way that's **complete, clear, and beginner-friendly**, yet technical enough for deeper understanding.

---

## 🌐 What Is DNS?

**DNS** is like the **phonebook of the internet**.

Humans access websites using names (like `www.google.com`), but computers access them using IP addresses (like `142.250.190.36`). The **Domain Name System (DNS)** translates human-readable domain names into IP addresses that computers use to communicate.

---

## 🧭 Basic Steps in DNS Resolution (When You Type a URL in Your Browser)

### 1. **User Types a Domain Name**

You type `www.example.com` into your browser.

---

### 2. **Browser Checks Cache**

Your computer or browser first checks its **DNS cache** to see if it recently looked up `www.example.com`.

- ✅ If found, it uses the cached IP address (fast!)
    
- ❌ If not found, it starts a full DNS resolution process.
    

---

### 3. **Query Sent to Recursive Resolver (ISP or Third-party like Google DNS)**

The request goes to a **recursive DNS resolver** — usually your ISP’s or a custom one like **Google DNS (8.8.8.8)** or **Cloudflare (1.1.1.1)**.

This resolver acts like a **middleman** that asks other servers to find the answer.

---

### 4. **Recursive Resolver Contacts the Root DNS Server**

The resolver asks the **Root DNS Server** (there are 13 sets globally) for the IP of the **Top-Level Domain (TLD) server** (like `.com`, `.net`, `.org`).

- The root server replies: "I don’t know `www.example.com`, but here’s the address of the `.com` TLD server."
    

---

### 5. **Recursive Resolver Contacts the TLD Server**

> The authoritative server is often also known as the nameserver for the domain

The resolver asks the `.com` **TLD server**:

> “Where is `example.com`?”

- The TLD server replies with the IP address of the **Authoritative DNS Server** for `example.com`.
    
>  DNS records all come with a TTL (Time To Live) value. This value is a number represented in seconds that the response should be saved for locally until you have to look it up again. Caching saves on having to make a DNS request every time you communicate with a server.
---

### 6. **Recursive Resolver Contacts Authoritative DNS Server**

The resolver then contacts the **Authoritative Name Server** for `example.com`.

- It asks: “What’s the IP address of `www.example.com`?”
    
- The server replies: “The IP is `93.184.216.34`.”
    

---

### 7. **Resolver Sends the IP to Your Browser**

The resolver gives the IP address to your computer/browser, which can now connect directly to the web server at `93.184.216.34`.

---

### 8. **Browser Sends HTTP(S) Request to the Web Server**

Your browser now knows where to go, and it makes an HTTP or HTTPS request to `93.184.216.34`, and the website loads.

---

## 🧠 Visual Recap (Step-by-Step)

```
You → Browser → DNS Cache → ❌ Not Found
   → Recursive Resolver
     → Root Server → .com TLD Server
       → Authoritative DNS Server
         → IP Address for www.example.com
           → Website Loads
```

---

## 🧰 Additional DNS Concepts

|Concept|Description|
|---|---|
|**Caching**|Speeds up DNS by saving recent lookups.|
|**TTL (Time to Live)**|How long a DNS record stays in cache.|
|**A Record**|Maps domain name to IPv4 address.|
|**AAAA Record**|Maps domain name to IPv6 address.|
|**CNAME**|Alias for another domain name.|
|**MX Record**|Specifies mail server for email delivery.|
|**DNSSEC**|Adds security to DNS using cryptographic signatures to prevent spoofing.|

---

## 🛡️ Security Note: DNS Can Be Attacked

DNS is essential but vulnerable:

- **DNS spoofing/poisoning**: Sending fake IP addresses.
    
- **DNS hijacking**: Redirecting traffic through malicious servers.
    

This is why secure alternatives like **DNS over HTTPS (DoH)** and **DNSSEC** are becoming common.

---

Would you like to see:

- A **real-world DNS trace** example?
    
- A breakdown of **DNS records** types?
    
- Or info on **how DNS differs from VPN**?


**TLD (Top-Level Domain)**

A TLD is the most righthand part of a domain name. So, for example, the [tryhackme.com](http://tryhackme.com/) TLD is **.com**. There are two types of TLD, gTLD (Generic Top Level) and ccTLD (Country Code Top Level Domain). Historically a gTLD was meant to tell the user the domain name's purpose; for example, a .com would be for commercial purposes, .org for an organisation, .edu for education and .gov for government. And a ccTLD was used for geographical purposes, for example, .ca for sites based in Canada, .co.uk for sites based in the United Kingdom and so on. Due to such demand, there is an influx of new gTLDs ranging from .online , .club , .website , .biz and so many more. For a full list of over 2000 TLDs [click here](https://data.iana.org/TLD/tlds-alpha-by-domain.txt).

**Second-Level Domain**

Taking [tryhackme.com](http://tryhackme.com/) as an example, the .com part is the TLD, and tryhackme is the Second Level Domain. When registering a domain name, the second-level domain is limited to 63 characters + the TLD and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens).

**Subdomain**

A subdomain sits on the left-hand side of the Second-Level Domain using a period to separate it; for example, in the name [admin.tryhackme.com](http://admin.tryhackme.com/) the admin part is the subdomain. A subdomain name has the same creation restrictions as a Second-Level Domain, being limited to 63 characters and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens). You can use multiple subdomains split with periods to create longer names, such as [jupiter.servers.tryhackme.com](http://jupiter.servers.tryhackme.com/). But the length must be kept to 253 characters or less. There is no limit to the number of subdomains you can create for your domain name


# 🧠 What Are DNS Records?

DNS records are entries in a DNS **zone file** stored on an **authoritative DNS server**. Each record **tells the internet** how to handle requests for a domain or subdomain.

Now let's explore the **most common DNS record types**:

---

## 1. 🧭 **A Record** (Address Record)

### 🔹 Purpose:

Maps a **domain or subdomain** to an **IPv4 address** (e.g., `104.26.10.229`).

### 🔧 Example:

```
example.com.      A      104.26.10.229
```

### 📌 Use Case:

When you visit `example.com`, your browser needs to know **which server** (IP address) to contact. The A record provides that IPv4 address.

---

## 2. 🌍 **AAAA Record** (IPv6 Address Record)

### 🔹 Purpose:

Maps a **domain or subdomain** to an **IPv6 address** (e.g., `2606:4700:20::681a:be5`).

### 🔧 Example:

```
example.com.      AAAA   2606:4700:20::681a:be5
```

### 📌 Use Case:

Just like A records, but for IPv6 networks. They help ensure future compatibility as IPv4 addresses become scarce.

---

## 3. 🔗 **CNAME Record** (Canonical Name Record)

### 🔹 Purpose:

Creates an **alias** of one domain to another domain name (not to an IP).

### 🔧 Example:

```
store.tryhackme.com.     CNAME     shops.shopify.com.
```

### 📌 Use Case:

Used when a subdomain (like `store.tryhackme.com`) is managed or hosted by a third-party service (like Shopify).  
It tells DNS:

> “Look at `shops.shopify.com` for the real address.”

Then another DNS lookup is performed on `shops.shopify.com` to get the actual IP.

---

## 4. 📧 **MX Record** (Mail Exchange Record)

### 🔹 Purpose:

Specifies the **mail servers** responsible for receiving email on behalf of the domain.

### 🔧 Example:

```
tryhackme.com.    MX     10 alt1.aspmx.l.google.com.
tryhackme.com.    MX     20 alt2.aspmx.l.google.com.
```

- The number (10, 20, etc.) is the **priority**.
    
- Lower numbers are tried **first**.
    
- If one mail server fails, the next one is tried.
    

### 📌 Use Case:

Used in **email delivery** — so when someone sends an email to `user@tryhackme.com`, the mail server knows where to deliver it.

---

## 5. 📝 **TXT Record** (Text Record)

### 🔹 Purpose:

Holds arbitrary **text data** for the domain. Used for:

- **Verification** (Google, Microsoft, etc.)
    
- **Email security** (SPF, DKIM, DMARC)
    

### 🔧 Example:

```
tryhackme.com.    TXT    "v=spf1 include:_spf.google.com ~all"
```

### 📌 Use Case:

#### a. **SPF** (Sender Policy Framework)

Specifies which servers are allowed to send email on behalf of your domain — helps **prevent spam and spoofing**.

#### b. **Domain Verification**

Third-party services (like Google Workspace) ask you to add a TXT record to prove **you own the domain**.

#### c. **Custom Metadata**

Some use TXT records for analytics tags, blockchain identities, or other experimental purposes.

---

## ✅ Summary Table

|Record Type|Maps to / Used for|Example|
|---|---|---|
|**A**|IPv4 address|`example.com → 104.26.10.229`|
|**AAAA**|IPv6 address|`example.com → 2606:4700:20::681a:be5`|
|**CNAME**|Another domain|`store.example.com → shops.shopify.com`|
|**MX**|Mail servers|`example.com → alt1.aspmx.l.google.com (priority 10)`|
|**TXT**|Text data (SPF, verification, etc.)|`"v=spf1 include:_spf.google.com ~all"`|

---

## 🔐 Security Tip:

Incorrect or missing **MX** and **TXT** records are a **common cause of email delivery problems**, and improper CNAMEs can break services if you're relying on third-party providers.

---

Would you like help **looking up real DNS records** for a domain, or maybe a **walkthrough on setting up SPF/DKIM** for email security?




#  HTTP IN DETAIL

**What is HTTP? (HyperText Transfer Protocol)**

HTTP is what's used whenever you view a website, developed by Tim Berners-Lee and his team between 1989-1991. HTTP is the set of rules used for communicating with web servers for the transmitting of webpage data, whether that is HTML, Images, Videos, etc.

**What is HTTPS?** ****(HyperText Transfer Protocol Secure)****  

HTTPS is the secure version of HTTP. HTTPS data is encrypted so it not only stops people from seeing the data you are receiving and sending, but it also gives you assurances that you're talking to the correct web server and not something impersonating it.




# Requests And Responses 

**Making a Request**

It's possible to make a request to a web server with just one line **GET / HTTP/1.1**

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/09e70200e7af451077081a3ee3d3708c.png)

But for a much richer web experience, you’ll need to send other data as well. This other data is sent in what is called headers, where headers contain extra information to give to the web server you’re communicating with, but we’ll go more into this in the Header task.

**Example Request:**

```http
GET / HTTP/1.1

Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

To breakdown each line of this request:

**Line 1:** This request is sending the GET method ( more on this in the HTTP Methods task ), request the home page with / and telling the web server we are using HTTP protocol version 1.1.

**Line 2:** We tell the web server we want the website tryhackme.com

**Line 3:** We tell the web server we are using the Firefox version 87 Browser

**Line 4:** We are telling the web server that the web page that referred us to this one is [https://tryhackme.com](https://tryhackme.com/)

**Line 5:** HTTP requests always end with a blank line to inform the web server that the request has finished.

**Example Response:**

```http
HTTP/1.1 200 OK

Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98


<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>
```

To breakdown each line of the response:

**Line 1:** HTTP 1.1 is the version of the HTTP protocol the server is using and then followed by the HTTP Status Code in this case "200 OK" which tells us the request has completed successfully.

**Line 2:** This tells us the web server software and version number.

**Line 3:** The current date, time and timezone of the web server.

**Line 4:** The Content-Type header tells the client what sort of information is going to be sent, such as HTML, images, videos, pdf, XML.

**Line 5:** Content-Length tells the client how long the response is, this way we can confirm no data is missing.

**Line 6:** HTTP response contains a blank line to confirm the end of the HTTP response.

**Lines 7-14:** The information that has been requested, in this instance the homepage.

