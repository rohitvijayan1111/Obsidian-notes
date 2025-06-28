- Conversion from base 10 to base 2
- conversion from base 2 to base 10
- 1's complement -> negation of binary representaion of the no
- 2's complement-> 1's complement +1


![[Pasted image 20250628122512.png]]


![[Pasted image 20250628135947.png]] 


> In the Integer representation of 32 bits, the 31 bit(0 indexed) is used to store the sign of the number


>So if we need to store a negative number what is stored is , it is represented in its 2 complements( during 1's complement the sign bit is set to 1)



### 1️⃣ What’s a 32-bit signed integer?

- A **32-bit signed integer** uses 32 bits (binary digits) to represent numbers.
    
- The most significant bit (MSB — the leftmost one) is used as the **sign bit**:
    
    - `0` → positive number (or zero)
        
    - `1` → negative number
        
- That leaves 31 bits for the magnitude of the number.
    

---

### 2️⃣ Range of 32-bit signed integers

Because we have a sign bit, the range splits like this:

- **Positive range** (including zero):
    
    - From `0` to 231−1=2,147,483,6472^{31} - 1 = 2,147,483,647.
        
    - Total count: 2312^{31} numbers (because 0 counts as one of them).
        
- **Negative range**:
    
    - From −1-1 down to −231=−2,147,483,648-2^{31} = -2,147,483,648.
        
    - Total count: 2312^{31} numbers.
        

So together:

231 negatives+231 positives (including zero)=232 unique bit patterns2^{31} \text{ negatives} + 2^{31} \text{ positives (including zero)} = 2^{32} \text{ unique bit patterns}

---

### 3️⃣ Why positive side is one less?

Notice the positive side stops at 231−12^{31} - 1 instead of 2312^{31} exactly — that’s because zero **eats up one positive number slot** (since `000...000` represents 0, a positive number).

---

### 4️⃣ Example of ranges in decimal

- **Negative**: -2,147,483,648 → -1
    
- **Zero**: 0
    
- **Positive**: 1 → 2,147,483,647
    

---

### 5️⃣ Summary answer

✅ **Total positive numbers** (including zero): 2312^{31} distinct values → from 0 up to 231−12^{31} - 1.  
✅ **Total negative numbers**: 2312^{31} distinct values → from −1-1 down to −231-2^{31}.  
✅ Altogether: 2322^{32} combinations, exactly filling 32 bits.

---

Would you like a diagram of the bit patterns or how two’s complement encoding makes this work?


Check if i th bit is set or not

set i th bit

clear the ith bit
	![[Pasted image 20250628143759.png]]

Toggle i th bit-> ^(1<<k)

remove the right most set bit -> n&(n-1)

check if a number is a power of 2 -> n&n-1 = =0

count the no of set bits in a no-> 