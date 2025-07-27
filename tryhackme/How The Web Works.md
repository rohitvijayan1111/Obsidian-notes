

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



# HTTP status code

**HTTP Status Codes:**

In the previous task, you learnt that when a HTTP server responds, the first line always contains a status code informing the client of the outcome of their request and also potentially how to handle it. These status codes can be broken down into 5 different ranges:

|   |   |
|---|---|
|**100-199 - Information Response**|These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common.|
|**200-299 - Success**|This range of status codes is used to tell the client their request was successful.|
|**300-399 - Redirection**|These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether.|
|**400-499 - Client Errors**|Used to inform the client that there was an error with their request.|
|**500-599 - Server Errors**|This is reserved for errors happening on the server-side and usually indicate quite a major problem with the server handling the request.|

**Common HTTP Status Codes:**

There are a lot of different HTTP status codes and that's not including the fact that applications can even define their own, we'll go over the most common HTTP responses you are likely to come across:

|   |   |
|---|---|
|**200 - OK**|The request was completed successfully.|
|**201 - Created**|A resource has been created (for example a new user or new blog post).|
|**301 - Moved Permanently**|This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead.|
|**302 - Found**|Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may change again in the near future.|
|**400 - Bad Request**|This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expected a certain parameter that the client didn't send.|
|**401 - Not Authorised**|You are not currently allowed to view this resource until you have authorised with the web application, most commonly with a username and password.|
|**403 - Forbidden**|You do not have permission to view this resource whether you are logged in or not.|
|**405 - Method Not Allowed**|The resource does not allow this method request, for example, you send a GET request to the resource /create-account when it was expecting a POST request instead.|
|**404 - Page Not Found**|The page/resource you requested does not exist.|
|**500 - Internal Service Error**|The server has encountered some kind of error with your request that it doesn't know how to handle properly.|
|**503 - Service Unavailable**|This server cannot handle your request as it's either overloaded or down for maintenance.|

If you are a visual learner, also check out a great [http.cat](https://http.cat/) resource to study status codes. Now, click the "View Site" button on the right to see what some of these HTTP status messages look like in a browser.



# Cookie

![[Pasted image 20250727181046.png]]



# header

Headers are additional bits of data you can send to the web server when making requests.

Although no headers are strictly required when making a HTTP request, you’ll find it difficult to view a website properly.

**Common Request Headers**

﻿These are headers that are sent from the client (usually your browser) to the server.  

**Host:** Some web servers host multiple websites so by providing the host headers you can tell it which one you require, otherwise you'll just receive the default website for the server.  

**User-Agent:** This is your browser software and version number, telling the web server your browser software helps it format the website properly for your browser and also some elements of HTML, JavaScript and CSS are only available in certain browsers.  

**Content-Length:** When sending data to a web server such as in a form, the content length tells the web server how much data to expect in the web request. This way the server can ensure it isn't missing any data.

**Accept-Encoding:** Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.

  

**Cookie:** Data sent to the server to help remember your information (see cookies task for more information).  

**Common Response Headers**

These are the headers that are returned to the client from the server after a request.

**Set-Cookie:** Information to store which gets sent back to the web server on each request (see cookies task for more information).  

**Cache-Control:** How long to store the content of the response in the browser's cache before it requests it again.  

**Content-Type:** This tells the client what type of data is being returned, i.e., HTML, CSS, JavaScript, Images, PDF, Video, etc. Using the content-type header the browser then knows how to process the data.  

**Content-Encoding:** What method has been used to compress the data to make it smaller when sending it over the internet.


