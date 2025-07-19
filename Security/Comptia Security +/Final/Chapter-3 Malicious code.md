
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
