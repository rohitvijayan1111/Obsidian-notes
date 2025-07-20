
**Objectives:**
- will need to be familiar with each of them,
- how to tell them apart,
- how you can identify them, 
- and common techniques used in combatting them.
**Malware**
- The term malware describes a wide range of software that is intentionally designed to cause harm to systems and devices, networks, or users.

Ransomware
- Ransomware is malware that takes over a computer and then demands a ransom
- types of ransomware, including crypto malware,
- Scareware-threatening to report the user to law enforcement due to pirated software or pornography, or Leakware / Doxware-threatening to expose sensitive information

🧾 **Common Indicators of Compromise (IoCs)**
  These are **warning signs** that ransomware may be present:
1. **C2 (Command & Control) Communication**
    - Device connects to known malicious IPs or domains
2. **Abuse of Legitimate Tools**
    - Use of tools like PowerShell, PsExec, or WMI in unusual ways
3. **Lateral Movement**
    - Malware tries to spread to other systems on the same network
4. **File Encryption**
    - Files become inaccessible, often with strange extensions
5. **Ransom Note Displayed**
    - User sees a message demanding payment
6. **Data Exfiltration**
    - Large file transfers to external IPs
        

---

## 🛡️ **Defense Against Ransomware**

| Control/Tool              | Description                                                       |
| ------------------------- | ----------------------------------------------------------------- |
| **Backups**               | Most important defense. Must be **offline/off-site** or immutable |
| **Antivirus/Antimalware** | Detects known ransomware signatures or behaviors                  |
| **Email Filtering**       | Blocks phishing emails and attachments                            |
| **Patch Management**      | Fixes vulnerabilities ransomware may exploit                      |
| **Network Segmentation**  | Limits the spread across internal systems                         |
| **User Training**         | Helps avoid phishing and social engineering traps                 |
## 🧨 **Trojans & Remote Access Trojans (RATs)**

### 🔍 **What is a Trojan?**

- A **Trojan** is malicious software disguised as a legitimate application.
    
- It **doesn’t replicate** like a virus or worm.
    
- It tricks users into **installing or running** it, then performs malicious actions in the background.
    

---

### 👁️‍🗨️ **What is a RAT (Remote Access Trojan)?**

- A special type of Trojan that **provides remote control** to an attacker.
    
- Acts like **legitimate remote access tools** (e.g., TeamViewer, AnyDesk).
    
- Often gives full access: file browsing, webcam/microphone access, keystroke logging, and more.
    
- **Hard to detect**, especially when attackers use known tools or legitimate-looking apps.
## 🛡️ **How Trojans and RATs Are Detected and Mitigated**

### 🔐 **Detection Techniques**

|Tool/Method|Role|
|---|---|
|**Antivirus/Antimalware**|Signature-based detection of known malware|
|**EDR (Endpoint Detection & Response)**|Behavioral monitoring, anomaly detection|
|**Network Monitoring**|Detects C2 (Command & Control) traffic or strange DNS queries|
|**Application Control**|Restricts what users can install or run|
|**Heuristics & Sandboxing**|Detects suspicious behavior even in unknown files|

---

### 🧯 **Mitigation Techniques**

|Practice|Explanation|
|---|---|
|**Security Awareness Training**|Educate users not to download apps from untrusted sources|
|**Application Whitelisting**|Only allow approved apps to be installed|
|**Restrict Admin Privileges**|Prevent users from installing software or modifying system settings|
|**Use official app stores**|Third-party apps pose greater risk|
|**Regular Software Updates**|Patch vulnerabilities that RATs exploit|
|**Monitor false positives cautiously**|Avoid disabling detection of legitimate tools used as RATs|


### 🛡️ What is **EDR (Endpoint Detection and Response)?**

**EDR** is a **security solution** that monitors, detects, investigates, and responds to threats on **endpoint devices** (like laptops, desktops, and servers). It goes beyond traditional antivirus by focusing on **behavior, visibility, and response**.


