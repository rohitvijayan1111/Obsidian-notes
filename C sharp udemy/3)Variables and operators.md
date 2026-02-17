
Console.WriteLine
Console.ReadKey()

In c#,once the variable has been declared, its type can't be changed only the value can(should be of the declared type)

- a variable can't be redeclared in the scope

string -> double quotes

Declaration 
initialization 
init at declaration

Variable, values dont get intialized automatically,but for fields it is initialized
NOTE:
- u cant use a variable before init ? what error comes **(Use of unassigned local variable 'x')**->**compile-time error** in **C#**
 ```
Compile-time errors occur when the compiler cannot prove that a variable (local) is definitely assigned before it is used — regardless of whether it is a value type or reference type

int x;
if (condition)
{
    x = 10;
}
Console.WriteLine(x); // ❌ error

```

- use can use keywords as variable name using "@" sign
- Compile-time error: _Cannot implicitly convert type_->assigning a value of the wrong type to a variable 
- Strongly typed-> means datatype of a variable cannot be changed
- When you run a console app **by double-clicking the `.exe` file** (or in some older setups), the console window may close instantly when the program finishes.
-   C# is a statically-typed programming language, which means..

`Console.ReadKey()` keeps the window open so you can **see the output**.

# operator precedence
a=10
b=5

![[Pasted image 20251215103235.png]]

OUTPUT:
Addition105
Error (since subtraction10(becomes a string)- b) -.wont be allowed
Multiplication 50
Division 2
John Smith

we can add paranthesis to this , to avoid such issue



for readline:
```C#
Console.ReadLine()// nothing should be put in
```

![[Pasted image 20251215105736.png]]



Breakpoint:
click on the side of the code line or press F9

to move forward from breakpoint, oneline F10 or ![[Pasted image 20251215110001.png]]

- we can hover over the variables to see the value of it.

Quickwatch:

- Select the string, right "Quickwatch", u can put in expression and test its workings
![[Pasted image 20251215111110.png]]

# Comparison and Logical operators

**SHORT-CIRCUTING**
- If the first part of the operand in || , C# would not execute the second operand
- same for &&, if first false, then second operand isnt checked


Methods

![[Pasted image 20251215160242.png]]



![[Pasted image 20251215162132.png]]

- methods can be used before they can be declared 




Perfect 👍 Let’s go **step by step** and connect it directly to _why variables behave differently_.

---

# Stack vs Heap in C# (Simple & Clear)

## 1️⃣ Stack Memory

### What goes on the stack?

- **Local variables**
    
- **Method parameters**
    
- **Method call information**
    

```csharp
void Test()
{
    int x = 10; // stack
}
```

### Key characteristics

- **Very fast**
    
- **Automatically managed**
    
- **Memory cleared when method exits**
    
- **Small & short-lived**
    

### Why locals are NOT auto-initialized

- Stack memory is reused
    
- It may contain **old garbage values**
    
- Auto-initializing every local variable would:
    
    - Hurt performance
        
    - Hide programming mistakes
        

So C# says:

> ❝ You must initialize local variables yourself ❞

That’s why this is illegal:

```csharp
int x;
Console.WriteLine(x); // ❌ compiler error
```

---

## 2️⃣ Heap Memory

### What goes on the heap?

- **Objects**
    
- **Class fields**
    
- **Arrays**
    
- **Reference types**
    

```csharp
class Test
{
    int y; // heap (field)
}
```

### Key characteristics

- **Slower than stack**
    
- **Managed by Garbage Collector (GC)**
    
- **Lives longer**
    
- **Shared across methods**
    

### Why fields ARE auto-initialized

Before an object is used, the **CLR zeroes out heap memory**.

This guarantees:

- No leftover data
    
- No security leaks
    
- Safe garbage collection
    

```csharp
Test t = new Test();
Console.WriteLine(t.y); // prints 0
```

---

## 3️⃣ Visual Mental Model

```
STACK (fast, short-lived)
-------------------------
int x;
int y;
method calls
parameters

HEAP (safe, managed)
--------------------
objects
class fields
arrays
strings
```

---

## 4️⃣ Why C# Enforces This Difference

### Design Goals of C#

✔ Performance  
✔ Safety  
✔ Bug prevention

|Memory|Initialized?|Why|
|---|---|---|
|Stack (locals)|❌ No|Speed + force correctness|
|Heap (fields)|✅ Yes|Safety + GC requirements|

---

## 5️⃣ Important Rule to Remember

> **Compiler protects locals**  
> **Runtime protects fields**

That one line explains **everything**.

---

## 6️⃣ Structs (Bridge Between Stack & Heap)

```csharp
struct S
{
    public int a;
}
```

```csharp
S s;
Console.WriteLine(s.a); // ❌ error
```

But:

```csharp
S s = new S();
Console.WriteLine(s.a); // 0
```

Why?

- Structs can live on stack **or** heap
    
- C# enforces explicit initialization unless `new` is used
    

---

## 7️⃣ Final Summary

- Local variables → **stack → must initialize**
    
- Fields → **heap → auto-initialized**
    
- This is **intentional**, not a limitation
    
- It makes C# both **fast and safe**
    

---

If you want next, I can explain:

- **Definite assignment rules** in detail
    
- **Why `new` initializes structs**
    
- **Why arrays are always initialized**
    
- **Stack vs Heap in interviews (trick questions)**