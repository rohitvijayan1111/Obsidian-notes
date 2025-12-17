- procedural programming
- spaghetti code
- ![[Pasted image 20251217160703.png]]![[Pasted image 20251217160718.png]]
- ![[Pasted image 20251217160819.png]]
- ![[Pasted image 20251217160921.png]]
- ![[Pasted image 20251217161014.png]]![[Pasted image 20251217161034.png]]
- ![[Pasted image 20251217161044.png]]


DOUBT:
- how methods belong to objects?? shouldnt it be the class

![[Pasted image 20251217161140.png]]
![[Pasted image 20251217161954.png]]


- DATE AND TIME
- ABSTRACTION -> SHOWING ONLY THE NECESSARY DETAIL AND HIDING THE COMPLEXITY


Here’s the **clean, compact summary** 👇

---

## C# Properties vs Methods — Summary

### 1️⃣ `Year`, `Month`, `DayOfWeek` are **NOT fields**

- They are **properties**
    
- They **run code** via a `get` accessor
    
- They just _look_ like variables
    

---

### 2️⃣ Properties ≠ Methods

- **Methods** → actions → **must use `()`**
    
- **Properties** → data/state → **no `()`**
    
- Parentheses are **not optional**
    

---

### 3️⃣ What “State” Means

- State = everything that defines the object
    
- State can be **stored** or **derived**
    
- `DayOfWeek` is **derived state**, not a conversion
    

---

### 4️⃣ When Something Is a Property

Use a **property** when:

- No parameters are needed
    
- No side effects
    
- No object is changed or created
    
- You’re _asking_, not _doing_
    

Examples:

```csharp
date.Year
date.DayOfWeek
string.Length
list.Count
```

---

### 5️⃣ When Something Is a Method

Use a **method** when:

- Work is done
    
- Parameters are required
    
- A new object/value is produced
    
- State is changed or transformed
    

Examples:

```csharp
date.AddDays(1)
date.ToString()
```

---

### 6️⃣ One Rule to Remember

> **Properties = “What is it?”**  
> **Methods = “What does it do?”**

That’s it. Once you keep that rule in mind, C# APIs start making perfect sense.'



![[Pasted image 20251217163238.png]]


>NOTE:
>Usually, in C#, we cant use uninitialized variables
>but with FIELDS IN CLASS, it is initialized with a default value



![[Pasted image 20251217204104.png]]

![[Pasted image 20251217204243.png]]![[Pasted image 20251217204329.png]]
![[Pasted image 20251217204353.png]]
