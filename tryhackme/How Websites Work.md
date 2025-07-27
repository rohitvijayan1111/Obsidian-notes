There are two major components that make up a website:

1. Front End (Client-Side) - the way your browser renders a website.
2. Back End (Server-Side) - a server that processes your request and returns a response.

There are many other processes involved in your browser making a request to a web server, but for now, you just need to understand that you make a request to a server, and it responds with data your browser uses to render information to you.



# HTML


- The `<!DOCTYPE html>` defines that the page is a HTML5 document. This helps with standardisation across different browsers and tells the browser to use HTML5 to interpret the page.


**Load Balancers**

When a website's traffic starts getting quite large or is running an application that needs to have high availability, one web server might no longer do the job. Load balancers provide two main features, ensuring high traffic websites can handle the load and providing a failover if a server becomes unresponsive.

When you request a website with a load balancer, the load balancer will receive your request first and then forward it to one of the multiple servers behind it. The load balancer uses different algorithms to help it decide which server is best to deal with the request. A couple of examples of these algorithms are **round-robin**, which sends it to each server in turn, or **weighted**, which checks how many requests a server is currently dealing with and sends it to the least busy server.

Load balancers also perform periodic checks with each server to ensure they are running correctly; this is called a **health check**. If a server doesn't respond appropriately or doesn't respond, the load balancer will stop sending traffic until it responds appropriately again.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/829e340231cd8aa9f5ed2fa5c464ea80.svg)  

**CDN (Content Delivery Networks)**

A CDN can be an excellent resource for cutting down traffic to a busy website. It allows you to host static files from your website, such as JavaScript, CSS, Images, Videos, and host them across thousands of servers all over the world. When a user requests one of the hosted files, the CDN works out where the nearest server is physically located and sends the request there instead of potentially the other side of the world.  

**Databases  
**

Often websites will need a way of storing information for their users. Webservers can communicate with databases to store and recall data from them. Databases can range from just a simple plain text file up to complex clusters of multiple servers providing speed and resilience. You'll come across some common databases: MySQL, MSSQL, MongoDB, Postgres, and more; each has its specific features.

**WAF (Web Application Firewall)**

A WAF sits between your web request and the web server; its primary purpose is to protect the webserver from hacking or denial of service attacks. It analyses the web requests for common attack techniques, whether the request is from a real browser rather than a bot. It also checks if an excessive amount of web requests are being sent by utilising something called rate limiting, which will only allow a certain amount of requests from an IP per second. If a request is deemed a potential attack, it will be dropped and never sent to the webserver.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/24cb6468b4e51e8d8bbe7872e96a22b3.svg)


Sure! Here's a clear explanation of how web servers work, based on the content you shared:

---

### **What is a Web Server?**

A **web server** is a piece of software (and sometimes the physical machine running it) that delivers content—like web pages, images, and videos—to users (clients) over the internet using the **HTTP protocol**.

When you type a URL like `http://www.example.com/picture.jpg`, the web server checks its **root directory** (usually something like `/var/www/html` on Linux) and sends back the file if it exists.

Popular web servers include:

- **Apache**
    
- **Nginx**
    
- **IIS** (from Microsoft)
    
- **Node.js** (JavaScript-based)
    

---

### **Virtual Hosts**

A single web server can host **multiple websites** using **virtual hosts**. Each virtual host can serve a different site based on the domain name in the HTTP request.

For example:

- `one.com` → `/var/www/website_one`
    
- `two.com` → `/var/www/website_two`
    

If there's no match to the requested domain, the **default site** is served.

---

### **Static vs. Dynamic Content**

#### **Static Content:**

- Files that **don’t change** per user.
    
- Examples: images, CSS, JavaScript, fixed HTML files.
    
- Served **as-is** from the disk.
    

#### **Dynamic Content:**

- Content that **changes** based on user actions or data.
    
- Examples: blog posts, search results, user profiles.
    
- Requires **backend processing** using scripting or programming.
    

---

### **Frontend vs Backend**

- **Frontend**: What you see in the browser (HTML, CSS, JavaScript).
    
- **Backend**: The server-side logic that generates or manipulates content behind the scenes.
    

You **can't see backend code** in the browser; you only see its result (usually HTML).

---

### **Scripting and Backend Languages**

These are programming languages that run on the server (backend) to make websites **interactive**. They can:

- Connect to databases
    
- Process user input
    
- Call APIs or services
    

Examples:

- **PHP**
    
- **Python**
    
- **Ruby**
    
- **NodeJS**
    
- **Perl**
    

#### Example: PHP

If you visit:

```
http://example.com/index.php?name=adam
```

And `index.php` contains:

```php
<html><body>Hello <?php echo $_GET["name"]; ?></body></html>
```

You’ll see this in your browser:

```html
<html><body>Hello adam</body></html>
```

Even though the **PHP code runs on the server**, users only get the **final HTML output**.

---

### **Why This Matters**

Dynamic content makes the web powerful—but it also introduces **security risks** if developers don’t write secure code. That’s why learning how web servers and backends work is critical for web development and cybersecurity.

---

Let me know if you’d like a visual diagram or analogy to help with any part!