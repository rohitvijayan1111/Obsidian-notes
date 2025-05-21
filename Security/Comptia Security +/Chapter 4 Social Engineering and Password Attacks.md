
- Social engineering  - focuses on human side of information security
	- Social engineering is the practice of manipulating people through a variety of strategies to accomplish desired actions
- works because it causes the target to react to a situation and that many make the target nervous or worried about a result or scenario.
- Principles:
	- Authority,
	- Intimidation - scaring/bullying
	- Consensus based- others agreed
	- Scarcity - golden opportunity
	- familirality based- using names that u know
	- Trust
	- urgency

### Phishing 
- Phishing is an social engineering attack to gain user information(sensitive) through sms, call,mail etc
- TYPES:
	- **Smishing**- through SMS
	- **Vishing**- through voice/call
	- **Spear phishing** - gather information of an individual /organization
	- **Whaling** - targeting big heads- **CEO/CFO**
- Mitigations 
	- Technical - Using Filtering tools
	- Non technical- User awarness

### Vishing
- Vishing is phishing accomplished via voice or voicemail messages. Vishing attacks rely on phone calls to social-engineer targets into disclosing personal, financial, or other useful information, or to send funds.

### Smishing - email isn't smishing
- Smishing relies on text messages as part of the phishing scam. Whereas other scams often rely on targets disclosing information via social engineering, smishing scams frequently attempt to get users to click on a link in a text message

### Misinformation and Disinformation and Malinformation 
- Misinformation - **inaccurate information** that is **shared * *without the intent to deceive.*
- Disinformation -  **inaccurate information** that is **shared * *WITH the intent to deceive.*
- Malinformation -  **accurate information** that is **shared * *with the intent to deceive.*


TRUST FRAMEWORK:
1. Tell your story.
2. Ready your team. 
3. Understand and assess MDM. 
4. Strategize response.
5. Track outcomes.


### Impersonation 
- Pretending to be someone else to gain trust, access, or information.

|**Impersonation**|**Identity Fraud/Theft**|
|---|---|
|Pretending to be someone — not always a real person|Using **someone’s real personal information**|
|Can be **general** (e.g., delivery driver) or **specific** (e.g., John from IT)|Usually **very specific** and involves stealing real identity data|
|Often used in social engineering|Often used for financial gain (e.g., credit card fraud)|

### Business Email Compromise (BEC) / Email account compromise
- BEC is a **type of cyberattack** where an attacker uses **email that appears legitimate** to trick individuals into performing actions
- techniques:
	- Using compromised accounts
	- Sending spoofed emails
	- Using common fake but similar domain techniques 
	- Using malware or other tools
- Mitigations :
	- MFA
	- policy
	- awareness training 

### **What is Pretexting?**

- **Definition**:  
    Pretexting is when an attacker **creates a false scenario (a "pretext")** to justify why they’re interacting with the target.
    
- It’s all about **building trust** and **credibility** so the victim doesn’t suspect anything is wrong.

### **What is a Watering Hole Attack?**

- **Definition**:  
    A **watering hole attack** is a **targeted cyberattack** where attackers **compromise a website** that they know a specific group of users **frequently visits**.
    
- The name comes from the idea of a **"watering hole" in nature**, where predators wait for prey. In cyber terms, the "prey" is the user, and the "hole" is a website the user trusts.
### **What is Brand Impersonation?**

- **Definition**:  
    Brand impersonation is a type of phishing where attackers send emails (or create websites) that **look like they come from a trusted company** (e.g., PayPal, Amazon, Microsoft, banks, etc.).
    
- These emails **mimic real branding** — including logos, colors, fonts, email templates, and even URLs that look almost real.

### **What is Typosquatting?**

- **Definition**:  
    Typosquatting (also known as **URL hijacking**) is when attackers **register domain names** that are **common misspellings** or **variations** of popular websites (e.g., `amason.com` instead of `amazon.com`).
    
- The goal is to **trick users who make typing mistakes** into visiting a **malicious or misleading site**.

### **What is Pharming?**

- Pharming **hijacks the DNS resolution process** so that even if you type the correct website URL (like `amazon.com`), you get sent to a **fake, malicious website** without realizing it.

	- Host file manipulation
	- DNS server hijacking

You're diving into an important part of the **Security+ exam** — password-related attacks. Let’s break down the three main types you're studying:

---

### 🔐 **1. Brute-Force Attacks**

- **Definition**: Tries **every possible password combination** until the correct one is found.
    
- **How it works**: It may use rules or patterns to prioritize more likely passwords (e.g., appending numbers or capitalizing the first letter), but at its core, it **keeps guessing until it works**.
    
- **Time-consuming** but **guaranteed** to succeed eventually — if no protections are in place.
    
- **Mitigations**:
    
    - Account lockout policies
        
    - Rate-limiting login attempts
        
    - Strong password policies
        

---

### 🧪 **2. Password Spraying**

- **Definition**: A type of brute-force attack where the attacker uses **a few common passwords** (like `Spring2025!`, `Password1`, or `Welcome123`) against **many different accounts**.
    
- **Why it works**:
    
    - Avoids detection by **not triggering account lockouts** from repeated login failures on the same account.
        
    - Takes advantage of the fact that **many users use weak or common passwords**.
        
- **Example**:
    
    - Attacker tries `GoTeam2025!` across hundreds of usernames on a sports fan site.
        
- **Mitigations**:
    
    - Use MFA (multi-factor authentication)
        
    - Enforce complex, unique passwords
        
    - Monitor for failed login attempts across many accounts
        

---

### 📖 **3. Dictionary Attacks**

- **Definition**: Uses a **predefined list of words** (a "dictionary") to guess passwords.
    
- **Tools**: Tools like **John the Ripper** or **Hydra** often come with wordlists.
    
- **Real-world customization**:
    
    - Attackers build custom dictionaries based on **reconnaissance** (e.g., pet names, local sports teams, employee names).
        
- **Difference from brute-force**:
    
    - Instead of trying every possible combination, it **only tries what's in the list** — faster, but not guaranteed.
        
- **Mitigations**:
    
    - Enforce use of passphrases or randomly generated passwords
        
    - Use MFA
        
    - Avoid common words and personal details
        

---

### 🔁 **Summary Table**

|Attack Type|Method|Target Scope|Speed|Common Tools|
|---|---|---|---|---|
|Brute-force|All combinations|Single account|Slow|Hydra, John the Ripper|
|Password Spraying|Few common passwords on many users|Many accounts|Fast|Custom scripts, CrackMapExec|
|Dictionary Attack|Known wordlists|Usually one account|Medium|John the Ripper, THC Hydra|

---

Would you like to go over how MFA or account lockout policies stop these attacks in practice?


## Terminologies 
- MDM- Misinformation ,disinformation , malinformation
- BEC- Business email compromise 
- EAC- Email account compromise

