
OBJECTIVES:
- will learn about different types of malicious activity
	- NEED TO KNOW HOW TO DETECT THEM
	- RESPONSE METHODS THAT ORGANIZATIONS WILL USE

OUTLINE:

---

# 🔐 **What Is Ransomware?**

**Ransomware** is a type of **malware** (malicious software) that **locks or encrypts** a victim’s files or entire system and then **demands a ransom** (usually in cryptocurrency) in exchange for restoring access.

---

### 🧬 **Types of Ransomware:**

1. **Crypto Malware**
    
    - Encrypts files and demands payment to decrypt them.
        
2. **Scareware**
    
    - Tricks users by displaying fake alerts or claiming legal trouble (e.g., piracy, pornography) to scare them into paying.
        
3. **Doxware / Leakware**
    
    - Threatens to leak sensitive or embarrassing data or images unless the ransom is paid.
        

---

### 📬 **How Ransomware Spreads:**

- **Phishing Emails**: Malicious attachments or links that, when clicked, install ransomware.
    
- **Remote Desktop Protocol (RDP)**: Attackers exploit weak RDP credentials to access systems directly.
    
- **Exploiting Vulnerabilities**: In web applications, services, or unpatched systems.
    
- **Drive-by Downloads**: Malware installs when visiting compromised websites.
    

---

### 🚨 **Indicators of Compromise (IoCs) for Ransomware:**

- **C2 (Command & Control) Traffic**: System contacts known malicious IPs or domains.
    
- **Abnormal Use of Legitimate Tools**: Tools like PowerShell, PsExec, or WMI used in unusual ways.
    
- **Lateral Movement**: The malware attempts to spread across the network to other devices.
    
- **File Encryption**: Rapid renaming or modification of files to encrypted formats (.locked, .crypt, etc.).
    
- **Ransom Notes**: Messages displayed to users demanding payment and explaining how to pay.
    
- **Large Data Transfers**: Possible **data exfiltration** before encryption (double extortion).
    

---

### 🛡️ **Defending Against Ransomware:**

1. **Backups**
    
    - Regular and **offline backups** are critical.
        
    - Ensure backups are not connected to the main network (to avoid infection).
        
2. **User Awareness**
    
    - Train staff to identify phishing emails and suspicious links.
        
3. **Patch Management**
    
    - Keep systems and software up-to-date with security patches.
        
4. **Access Controls**
    
    - Limit use of admin accounts and segment networks to contain breaches.
        
5. **Endpoint Protection**
    
    - Use anti-malware and endpoint detection & response (EDR) tools.
        
6. **Incident Response Plan**
    
    - Have a clear, practiced plan for ransomware incidents—**including whether to pay** (note: law enforcement often advises against it).
        

---

### 💰 **Should You Pay the Ransom?**

- **Paying is risky**—there’s no guarantee files will be restored.
    
- Some attackers will:
    
    - **Not deliver the decryption key**
        
    - **Ask for more money**
        
    - **Target you again**
        

It’s generally advised to **report the attack** to authorities and use backups for recovery.

---

Let me know if you'd like a summarized version of this for a presentation, or a comparison chart between ransomware types and delivery methods.


