- Cryptography is the practice of encoding information in a manner that it cannot be decoded without access to the required decryption key.
- Cryptography consists of two main operations: encryption, which transforms plain-text information into ciphertext using an encryption key, and decryption, which transforms ciphertext back into plain text using a decryption key


Cryptography has several important goals
- confidentiality
- integrity
- authentication,
- nonrepudiation



A cipher is a method used to scramble or obfuscate characters to hide their value. Ciphering is the process of using a cipher to do that type of scrambling to a message.

The two primary types of nonmathematical cryptography, or ciphering methods, are 
- substitution and 
- transposition.

**Substitution Ciphers**

- A substitution cipher is a type of coding or ciphering system that changes one character or symbol into another

- One of the oldest known substitution ciphers is called the Caesar cipher.]
- The system involves simply shifting all letters a certain number of spaces in the alphabet

ROT13
ROT13, or “rotate 13,” is another simple substitution cipher. The ROT13 cipher works the same way as the Caesar cipher but rotates every letter 13 places in the alphabet.


# Polyalphabetic Substitution


Vigenère cipher


Alright — let’s slow this right down so it clicks.  
The Vigenère cipher sounds complicated, but once you see the **pattern**, it’s actually quite logical.

---

## 1️⃣ The problem it solves

- A **simple substitution** (like Caesar shift) always shifts letters the same way.  
    Example: shift by +3 → `A→D`, `B→E`, etc.
    
- That’s easy to break because letter frequencies in English remain the same.
    
- **Polyalphabetic substitution** changes the shift every letter — making patterns harder to detect.
    

---

## 2️⃣ The secret ingredient: a keyword

- The keyword tells you **how much to shift each letter**.
    
- Each letter of the keyword corresponds to a shift number:
    

```
A → shift by 0 (no change)
B → shift by 1
C → shift by 2
...
Z → shift by 25
```

---

## 3️⃣ Example: “SECRET MESSAGE” with keyword “APPLE”

We write the keyword repeatedly so it matches the message length:

```
Plain:  S  E  C  R  E  T   M  E  S  S  A  G  E
Key:    A  P  P  L  E  A   P  P  L  E  A  P  P
```

---

## 4️⃣ Encryption process

For **each letter**:

1. Find the **shift** based on the key letter.
    
2. Shift the plain text letter forward in the alphabet.
    
3. Wrap around if needed.
    

Let’s do the first few:

- **First letter**:
    
    - Plain = `S`
        
    - Key = `A` → shift 0
        
    - `S` shifted by 0 = `S`
        
- **Second letter**:
    
    - Plain = `E`
        
    - Key = `P` → P is the 16th letter (shift 15 in 0-based counting)
        
    - Shift `E` forward by 15 → `T`
        
- **Third letter**:
    
    - Plain = `C`
        
    - Key = `P` (shift 15)
        
    - Shift `C` forward by 15 → `R`
        
- Keep going… you get:  
    `S T R C I T B T D W A V T`
    

---

## 5️⃣ Why the Vigenère table exists

The **Vigenère table** is just a big lookup chart so you don’t have to do number math in your head.

- Columns = plaintext letters
    
- Rows = key letters
    
- Intersection = encrypted letter
    

Example:  
Find row “P”, column “E” → result = “T”

---

## 6️⃣ Decryption

To reverse it:

1. Take the key letter.
    
2. Go to **that row** in the table.
    
3. Find the ciphertext letter in that row.
    
4. Look **upwards** to the top column — that’s the plaintext.
    
Transposition Ciphers
A transposition cipher involves transposing or scrambling the letters in a certain manner. Typically, a message is broken into blocks of equal size, and each block is then scrambled.

![[Pasted image 20250809193212.png]]

Columunar transposition

![[Pasted image 20250809193229.png]]

The Enigma Machine

- The Enigma machine was created by the German government during World War II to provide secure communications between military and political units.
- The operator was responsible for configuring the machine to use the code of the day by setting the rotary dials at the top of the machine and configuring the wires on the front of the machine. The inner workings of the machine implemented a polyalphabetic substitution, changing the substitution for each character of the message.
- e and energy to a project called Ultra designed to defeat the machine. The effort to defeat Enigma was centered at Bletchley Park in the United Kingdom and was led by pioneering computer scientist Alan Turing.


Steganography


Steganography is the art of using cryptographic techniques to embed secret messages within another file. Steganographic algorithms work by making alterations to the least significant bits of the many bits that make up image files

Steganography is an extremely simple technology to use, with free tools openly available on the Internet. Figure 7.4 shows the entire interface of one such tool, OpenStego

Steganography can also be used for legitimate purposes, however. Adding digital watermarks to documents to protect intellectual property is accomplished by means of steganography



# Protecting Data at Rest with Different Levels of Encryption

## Encrypting Data on Disk

- Full-disk encryption (FDE) 
	- is a form of encryption where all the data on a hard drive is automatically encrypted, including the operating system and system files
	- However, once the system is booted, the entire disk is accessible, which means data is vulnerable if the system is compromised while running

- Partition encryption
	- is similar to FDE but targets a specific partition of a hard drive instead of the entire disk
	- Partition encryption is particularly useful when dealing with dual-boot systems or when segregating sensitive data

- File-level encryption focuses on individual files. This method allows users to encrypt specific files rather than entire drives or partitions

- Volume encryption involves encrypting a set “volume” on a storage device, which could contain several folders and files
- Volume encryption is useful when you want to encrypt a large amount of data at once but don't need to encrypt an entire disk or partition.


# Encryption of DB

## 1️⃣ Database-Level Encryption

This means you encrypt **big chunks of the database all at once**.

### Two main types:

**A. Transparent Data Encryption (TDE)**

- Encrypts the _entire database_ (or the whole storage file).
    
- Works “under the hood” — applications don’t need to change their code.
    
- Protects data **at rest** (on disk).
    
- Example: If someone steals the database file, they can’t read it without the encryption key.
    
- Downside: If an attacker hacks the running database server, they can still see decrypted data.
    

**B. Column-Level Encryption (CLE)**

- Encrypts **specific columns** in a table (like passwords, credit card numbers, SSNs).
    
- Other columns stay unencrypted for performance.
    
- Good for targeting only the sensitive parts.
    
- Requires some application-level work to encrypt/decrypt the column values.
    

---

## 2️⃣ Record-Level Encryption

- Instead of encrypting whole columns or the entire database, you encrypt **individual rows (records)**.
    
- Each record could even have a **different encryption key**.
    
- Offers **very fine control** over who can see what.
    
- Often used in **multi-tenant** or **shared databases**, where each user or organization’s data must be isolated.
    
- More secure but more complex to manage (many keys, more encryption operations).
    

---

## 3️⃣ Quick comparison

|Level|Scope|Pros|Cons|
|---|---|---|---|
|**TDE**|Whole database file|Easy to set up, protects at rest|Can’t stop insiders with DB access|
|**CLE**|Specific columns|Efficient, targeted|Application changes needed|
|**Record-level**|Individual rows|Very granular, great isolation|Complex key management, slower|


## 3️⃣ The **challenge–response** process

1. **Bob says**: “Hi Alice, I’m Bob.”
    
2. **Alice says**: “If you’re really Bob, prove it — here’s a random word: `HELLO`.”
    
3. Bob **applies the shared code** (reverse the letters) → `OLLEH`.
    
4. Bob sends back `OLLEH` to Alice.
    
5. Alice checks:
    
    - She reverses it → `HELLO`
        
    - Matches her challenge? ✅ Yes.
        
6. Alice now **trusts that Bob knows the secret**, so he must be the real Bob.

## 5️⃣ Real-life equivalent

In real systems:

- The “challenge” is a **random number (nonce)**.
    
- The “code” is an encryption algorithm or hash function with a **secret key**.
    
- This prevents replay attacks and ensures you’re talking to the genuine user.
