- procedural programming
- spaghetti code
- ![[Pasted image 20251217160703.png]]![[Pasted image 20251217160718.png]]
- ![[Pasted image 20251217160819.png]]
- ![[Pasted image 20251217160921.png]]
- ![[Pasted image 20251217161014.png]]![[Pasted image 20251217161034.png]]
- ![[Pasted image 20251217161044.png]]


DOUBT:
- how methods belong to objects?? shouldnt it be the class
- In C#, a top-level class is `internal` by default, while a nested class is `private` by default.

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

![[Pasted image 20251218101354.png]]
![[Pasted image 20251218101642.png]]
FOr public, it must be in pascal Case
![[Pasted image 20251218101822.png]]
- After defining the default constructor won't work and would through an error
- ![[Pasted image 20251218101851.png]]
- Default values, can be set to the fields, if in constructor any value for that field is provided , it would get overridden
- LEARN DATETIME


# TOP LEVEL STATEMENTS

![[Pasted image 20251218103441.png]]
- We can have only a single file where they class need not be defined and inside which all code must be written. It gets internally converted to a Class
- SO ALL CODE IN C#, must be written inside a **class**
- ![[Pasted image 20251218103637.png]]
  THEY CANNOT HAVE ACCESS MODIFER, Specification, it can only be accessed only inside this file


# Adding methods to classes

![[Pasted image 20251218103900.png]]

![[Pasted image 20251218103944.png]]
- default access modifier for a method in a class, is **Private**


# Encapsulation
![[Pasted image 20251218104306.png]]

![[Pasted image 20251218104507.png]]


# Method Overloading

> To create a constructor quickly in VS Community, we need to type ctor and tab button twice, it will create an constructor,with any parameter, so to add them, right click on those fields that you want to add to the constructor and quick action and refactoring, add parameters to the constructor name()


![[Pasted image 20251218110004.png]]

- The method signature should be different


# Constructor Overloading

- needs to be distinguishable by the paramter


# Calling one constructor from other

![[Pasted image 20251218110308.png]]
![[Pasted image 20251218110342.png]]

![[Pasted image 20251218110605.png]]


# Expression bodied methods
- can be used when there is only one expression in the method
![[Pasted image 20251218110620.png]]

# this keyword

- can be used to pass the instance / object in a method
- to assign values
- to can constructor 



![[Pasted image 20251218111020.png]]



# optional parameter


![[Pasted image 20251218111503.png]]

- giving the default value for the parameter, makes it optional
- ![[Pasted image 20251218111626.png]]![[Pasted image 20251218111654.png]]
- ![[Pasted image 20251218111806.png]]![[Pasted image 20251218111840.png]]
- ![[Pasted image 20251218111857.png]]


# nameof

![[Pasted image 20251218113354.png]]



# readonly

![[Pasted image 20251218114628.png]]
![[Pasted image 20251218114648.png]]
![[Pasted image 20251218114711.png]]

- cant give var, for const variable 
- const variable name must be in capital letter
- ![[Pasted image 20251218114937.png]]
![[Pasted image 20251218114906.png]]
- for const, normal addition operations are fine, but method calling wont be allowed  
- for readonly, the default value will be used, if nothing is given


# Properties

- getter and setter methods , are called properties in c#
- ![[Pasted image 20251218120453.png]]
- ![[Pasted image 20251218120548.png]]
> So by default, the getter and setter are defined??


# Backing field
![[Pasted image 20251218120822.png]]
![[Pasted image 20251218120841.png]]

![[Pasted image 20251218121143.png]]
![[Pasted image 20251218121032.png]]
value can be only set during the declaration or in the constructor, even when trying to set value inside the same class it , would throw error


![[Pasted image 20251218122038.png]]


# working of properties
This is a **very common and very good confusion** — you’re touching the core idea of **what properties actually are in C#** 👍  
Let’s clear it up cleanly and conceptually.

---

## Short answer (key idea)

> **A property is NOT a variable.**
> 
> A property is a **pair of methods** (`get` and `set`) that _access_ a variable (a **field**).

---

## How it really works under the hood

### Field (actual variable in memory)

```csharp
private int _age;
```

- This is a real variable
    
- It stores data in memory
    

---

### Property (controlled access to the field)

```csharp
public int Age
{
    get { return _age; }
    set { _age = value; }
}
```

- `get` → method that **returns the field**
    
- `set` → method that **assigns the field**
    
- `value` → implicit parameter to `set`
    

So when you write:

```csharp
person.Age = 25;
```

What actually happens:

```csharp
set_Age(25);
```

---

## Why properties exist at all

If we only used public fields:

```csharp
public int Age;
```

❌ No validation  
❌ No control  
❌ Breaking changes if logic is added later

With properties:

```csharp
public int Age
{
    get => _age;
    set
    {
        if (value >= 0)
            _age = value;
    }
}
```

✔ Validation  
✔ Encapsulation  
✔ Future-proof design

---

## What about auto-properties?

This is where confusion usually comes from.

```csharp
public int Age { get; set; }
```

You **don’t see a field**, but it **still exists**.

The compiler secretly generates:

```csharp
private int <Age>k__BackingField;
```

So:

- Property still uses a field
    
- The field is just **hidden**
    

---

## Summary Table

|Concept|Field|Property|
|---|---|---|
|Stores data|✅ Yes|❌ No|
|Has memory|✅ Yes|❌ No|
|Contains logic|❌ No|✅ Yes|
|Accessed like variable|✅ Yes|✅ Yes|
|Encapsulation|❌ No|✅ Yes|

---

## Mental model (important)

> **Field = storage**  
> **Property = gatekeeper**

---

## Interview-ready one-liner 🎯

> In C#, a property does not store data itself; it provides controlled access to a field, which is the actual variable that holds the data.

---

If you want, next I can explain:

- Why C# discourages public fields
    
- Difference between properties and methods
    
- `get; private set;` and `init`
    

Just ask 😊

![[Pasted image 20251218122632.png]]


# Object intializer

- if we dont define the value for the properties it, will be assigned a default value according to its type
- ![[Pasted image 20251218123508.png]]


 WHat will happen if we pass the same value from both the constructor and the object intializer
 - the one sent via the constructor is called first, as it is invoked first
 - then the object initialzer executes and overrides to its value
 - works only when the property has a public access scope and not private
 - To solve tha problem new keyword called init is used, the value could be set only when the object is created.


# Computed properties

![[Pasted image 20251218124207.png]]
- calling this property, each time will build a string which may not be very efficient


- METHOD ressembles actions and properties ressembles data
- ![[Pasted image 20251218124434.png]]
- DOUBT:
  - how will the compiler know if we are defining a property or a method, when defining similar to expression body method
  - ![[Pasted image 20251218124615.png]]

![[Pasted image 20251218130048.png]]


# static method

![[Pasted image 20251218131050.png]]


![[Pasted image 20251218131151.png]]
- Static method can be only called with the class name and not with the object
- a static method should not call an non static method , as it might have value restricted to the object
- ![[Pasted image 20251218131458.png]]
- ![[Pasted image 20251218131537.png]]
- 