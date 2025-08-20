
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



