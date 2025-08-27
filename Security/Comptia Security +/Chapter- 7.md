
- Cryptography is the practice of encoding information in a manner that it cannot be decoded without access to the required decryption key.
- ciphertext ->  the text that is  encrypted.


- nonrepudiation, ensures that individuals can prove to a third party that a message came from its purported sender
- A cipher is a method used to scramble or obfuscate characters to hide their value.



TYPES NON MATHEMATICAL CRYPTOGRAPHY
- Substitution 
- Transposition 


Substitution Ciphers

- A substitution cipher is a type of coding or ciphering system that changes one character or symbol into another
- **Caesar cipher Substitution**. It was purportedly used by Julius Caesar. The system involves simply shifting all letters a certain number of spaces in the alphabet
- ROT13
	ROT13, or “rotate 13,” is another simple substitution cipher. The ROT13 cipher works the same way as the Caesar cipher but rotates every letter 13 places in the alphabet. 
-  **Polyalphabetic Substitution**
	- **Polyalphabetic substitution** improves security by using **multiple substitution alphabets** instead of just one.
	-  or example, you might shift the first letter by three to the right, the second letter by two to the right, and the third letter by one to the left
	- ### **2. How it Works**

- Choose a **keyword** (e.g., `LEMON`).
    
- Repeat the keyword to match the plaintext length.
    
- Each letter of the keyword decides the Caesar shift for that position.
    

👉 Formula:

Ci=(Pi+Ki)mod  26C_i = (P_i + K_i) \mod 26Ci​=(Pi​+Ki​)mod26

Where:

- PiP_iPi​ = position of plaintext letter
    
- KiK_iKi​ = position of keyword letter
    
- CiC_iCi​ = ciphertext letter
    

---

### **3. Example: Vigenère Cipher** (famous polyalphabetic cipher)

#### Plaintext:
`ATTACKATDAWN`
#### Keyword:
`LEMONLEMONLE`
#### Step-by-step:
- A (0) + L (11) = L (11)
- T (19) + E (4) = X (23)
- T (19) + M (12) = F (5)
- A (0) + O (14) = O (14)
- C (2) + N (13) = P (15)
- K (10) + L (11) = V (21)
- ... (continue process)
#### Ciphertext:
`LXFOPVEFRNHR`

## Enigma Machine 
- The **Enigma Machine** was a **polyalphabetic substitution cipher device** used by Nazi Germany during **World War II** to encrypt military communications.
- Operators would configure the machine each day using a **key setting** (rotor positions, plugboard connections, etc.), which determined the encryption scheme.
- When a letter was typed, the machine substituted it through multiple layers of electrical and mechanical scrambling, producing a ciphered letter.
- Mission ULTRA was launched to decode the working of the enigma machine, UK won the war by deciphering the working of the enigma machine


## Steganography
 - **Steganography** is the art and science of **hiding information** (such as text, files, or messages) inside other media (like images, audio, or video) so that it is **not visible to the human eye**.
- Example: Hiding a secret text message inside an image file, so the image looks unchanged but carries hidden data.
- openStego is a tool used to do steganography by uploading an image and text that needed to be embedded in it
- An legitimate usage of steganography - > to verify the orginality of the document by adding watermark to it


## Types of cryptography systems

- Symmetric cryptosystems use a shared secret key available to all users of the cryptosystem.
- Asymmetric cryptosystems use individual combinations of public and private keys for each user of the system
- Obfuscation is a concept closely related to confidentiality. It is the practice of making it intentionally difficult for humans to understand how code works

## Encrypting Data on Disk

### Full Disk Encryption (FDE)
- Full-disk encryption (FDE) is a form of encryption where all the data on a hard drive is automatically encrypted, including the operating system and system files
- once the system is booted, the entire disk is accessible, which means data is vulnerable if the system is compromised while running.
### Partition encryption
- Partition encryption is similar to FDE but targets a specific partition of a hard drive instead of the entire disk.
- useful when dealing with dual-boot systems or when segregating sensitive data
### File-level encryption
- File-level encryption focuses on individual files. This method allows users to encrypt specific files rather than entire drives or partitions
### Volume encryption
- Volume encryption involves encrypting a set “volume” on a storage device, which could contain several folders and files.
- Volume encryption is useful when you want to encrypt a large amount of data at once but don't need to encrypt an entire disk or partition.


## Encrypting Database Data
- Database encryption targets data at the database level. It's a method used to protect sensitive information stored in a database from access by unauthorized individuals
### Transparent Database encryption (TDE)
- Transparent Data Encryption (TDE), which encrypts the entire database,
### Column-level Encryption (CLE)
- which allows for specific columns within tables to be encrypted.
### Record -level encryption
- is a more granular form of database encryption. It allows individual records within a database to be encrypted

## Authentication

- **Challenge-Response Protocol**
    - Used to verify the identity of a system or user without directly transmitting the secret key.
    - **Process:**
        1. **System A** sends an authentication request to **System B**.
        2. **System B** generates a random challenge (a message or number) and sends it to **System A**.
        3. **System A** encrypts the challenge using the **shared secret key** and sends it back.
        4. **System B** decrypts the response and checks if it matches the original challenge.
        5. If the values match, **System A is authenticated**.
- **Key Used:**
    - Both systems share the same **symmetric key** for encryption and decryption.


## 1️⃣ What is a cryptographic key?

- A **key** in cryptography is just a **big number**.
- That number controls how data is scrambled (encryption) or unscrambled (decryption).
- Without the right key, you can’t make sense of the encrypted data.
## 2️⃣ Key length and key space

- **Key length** = how many bits long the key is.  
    Example: 128-bit key → a binary number with 128 digits (each digit is 0 or 1).
- **Key space** = the total number of possible keys you could pick.  
    Formula: 2n2^n2n, where _n_ = key length.

Examples:
- 3-bit key → 23=82^3 = 823=8 possible keys (`000` to `111`).
- 128-bit key → 2128≈3.4×10382^{128} ≈ 3.4 × 10^{38}2128≈3.4×1038 possibilities.  
    (That’s an astronomically huge number — practically impossible to brute-force.)
    
## 3️⃣ Why it matters
- The **larger the key space**, the harder it is for an attacker to guess the right key by brute force.
- Example:
    - A 56-bit key (DES) can be brute-forced with enough computers in hours/days.
    - A 128-bit or 256-bit key is so huge that brute-forcing would take longer than the age of the universe.


## Kerckhoffs’ Principle

Kerckhoffs’ Principle says:  
👉 _A cryptographic system must remain secure even if the attacker knows everything about it — except the secret key._

In other words:
- The **algorithm** is public.
- The **key** is secret.
- Security comes **only from the secrecy of the key**, not from hiding how the system works.
    
## 2️⃣ Why this matters
- If an algorithm is secret (“security through obscurity”), it **can’t be peer-reviewed**. That often means hidden flaws.
- Once the algorithm leaks (and it almost always does), the entire system collapses.
- Public algorithms (like AES, RSA, SHA) have been tested by thousands of experts. If they hold up to years of scrutiny, we can trust them.
## 3️⃣ Real-world analogy

🔒 **Bad security through obscurity:**
- Imagine a lock where the _design of the lock_ must stay secret for it to be safe.
- If someone studies the lock or makes a copy, the lock is worthless

🔑 **Kerckhoffs-style security:**
- The _design of the lock_ is public — anyone can study how it works.
- What keeps it secure is that only the owner knows the **key** that fits the lock.

## 2️⃣ Types of keys

There are **two main styles of cryptosystems**:
- **Private key (Secret key) systems**
    - One shared key for both encryption & decryption.
    - Example: **AES** (symmetric cryptography).
    - Problem: securely sharing that key with others.
        
- **Public key systems**
    - Each person has a **key pair**:
        - **Public key** (can be shared with everyone)
        - **Private key** (kept secret)
    - What’s encrypted with one can be decrypted with the other.
    - Example: **RSA, ECC** (asymmetric cryptography).
    - Solves the “key sharing” problem.

## 3️⃣ Terminology
- **Cryptographic keys = cryptovariables** (just another word for keys).
- **Cryptography** = creating codes and ciphers (defense).
- **Cryptanalysis** = breaking codes and ciphers (attack).
- **Cryptology** = both combined (the entire science of codes).
- **Cryptosystem** = the actual implementation of a cipher (the algorithm + hardware/software + key management).

## 2️⃣ Two main types of ciphers

### 🔹 A. Block Ciphers
- Work on **fixed-size chunks (“blocks”)** of data at a time.
- Example block sizes: 64 bits, 128 bits
- The same encryption operation is applied to the entire block.
    
**Examples in history:**
- **Transposition ciphers** (like reversing an entire word, or rearranging letters in a whole block).
- **Columnar transposition** (arrange text in a grid and read it out in a different order).

**Modern block ciphers:**
- **AES** (Advanced Encryption Standard)
- **DES/3DES**
They’re the workhorses of modern cryptography.

---
### 🔹 B. Stream Ciphers
- Work on data **one character or one bit at a time** — like a continuous flow (“stream”).
- They don’t wait for a full block, they encrypt/decrypt as data comes in.
**Examples in history:**
- **Caesar cipher** (shifting each letter individually).
- **One-time pad** (each letter is encrypted independently using a random key character).
    
**Modern stream ciphers:**
- RC4 (older, not secure now)
- Salsa20, ChaCha20 (widely used today, very fast).
---


