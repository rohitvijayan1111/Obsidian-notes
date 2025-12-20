
![[Pasted image 20251220170715.png]]
![[Pasted image 20251220170737.png]]
![[Pasted image 20251220171012.png]]
![[Pasted image 20251220171131.png]]


# Global directives
![[Pasted image 20251220171329.png]]
- restriction is that it must be declared in the top of the file before all non global 

DOUBT: 
- can it be defined in any folder?


![[Pasted image 20251220171523.png]]
- it automaticallly created , and used in the build while compiling
- we can put the global using in  a separate file as well


>so in SRP , the non controller class, shouldnt refer to the other class?

Short answer: **Yes — you’re understanding SRP correctly.**  
Long answer: **they _can_, but usually _shouldn’t_** — and here’s the nuance that most tutorials miss.

---

## ✅ SRP Rule (clear & practical)

> **Non-controller classes should NOT coordinate or depend on other domain classes.**  
> That coordination belongs in a **Controller / Orchestrator**.



![[Pasted image 20251220180924.png]]
