	- Compilation is the process of converting the source code (.cs) into a format that computer can understand
```
.cs -> .dll 
```

# 📘 **Compilation – Summary Notes**

## 🔹 What is Compilation?

- **Compilation** is the process of transforming _human-readable_ source code (e.g., `.cs` files) into a _computer-readable_ format.
    
- Computers **cannot understand** C# code directly — they only understand machine code or low-level instructions.
    
- The output of compilation is **not meant for humans to read**.
    

---

## 🔹 What is a Compiler?

- A **compiler** is a program that translates source code into executable files.
    
- In Visual Studio, the compiler is installed automatically.
    

---

## 🔹 What Files Are Involved?

When you create and build a C# project, several important files and folders appear:

### **1. `.csproj` file**

- Represents the project configuration.
    
- Not directly part of compilation output, but tells the compiler how to build the program.
    

### **2. `Program.cs`**

- Your actual source code (human-readable).
    

### **3. `bin/` and `obj/` folders**

- Contain compilation output and temporary build files.
    

---

## 🔹 What Happens During Build?

### ✔️ _Clean Solution_

- Removes all previously generated build files.
    

### ✔️ _Build Solution_

- Compiles the code and creates new output files in:
    
    ```
    bin/Debug/net6.0/
    ```
    

Here you will find:

### **• `.exe` file**

- The executable application produced by the compiler.
    
- Can be run _without Visual Studio_.
    
- Can be shared with others by copying the folder.
    

### **• `.dll` file**

- **DLL = Dynamic Link Library**
    
- Contains compiled code in a format the computer can understand.
    
- The `.exe` depends on this `.dll` to run.
    
- **If the DLL is removed, the EXE will not work**.
    
- In C#, almost all compiled code ends up in a DLL.
    

---

## 🔹 Why DLLs?

- They allow code to be reused.
    
- Enable separation between different parts of the program.
    
- Reduce duplication and make applications modular.
    

---

## 🔹 Key Takeaways

- **Compilation** = turning human code into machine-understandable code.
    
- **Compiler** = tool that performs this transformation.
    
- **Executable (`.exe`)** = the runnable program.
    
- **DLL (`.dll`)** = compiled code libraries required by the executable.
    
- Building cleans old output and generates fresh compiled files.
    
:

---

# 🔍 **Why is a DLL called a “Library”?**

A **library** in programming is simply:

> **A collection of code that other programs can use.**

It doesn’t matter whether the code is in a text file, a compiled file, or something else —  
if other programs _reuse_ it, programmers call it a **library**.

A DLL contains **functions, classes, and resources** that multiple programs can use.  
So even though it is “just a compiled file,” it _acts as a library of reusable functionality_.


# ✅ **When you have multiple `.cs` files in one project** (does all .cs file combine into one .dll and .exe file?)

All `.cs` files in that project are:

- Compiled together
    
- Combined into **one assembly**  
    → That assembly is either:
    
    - a **.dll** (Class Library, or most modern .NET project types), or
        
    - an **.exe** (Console App or GUI app)



# Structure of Project

---

## 1️⃣ `.csproj`

**Your understanding:**

> framework version and modules used

✅ **Correct**, with a bit more detail:

The `.csproj` file defines:

- **Target framework** (e.g., `net8.0`)
    
- **Dependencies / modules** (NuGet packages)
    
- Build settings (Debug/Release)
    
- Project type (Console, Web, Library)
    

**Example**

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
  </ItemGroup>
</Project>
```

📌 Think of `.csproj` as the **project blueprint**.

---

## 2️⃣ `Properties/`

**Your understanding:**

> it set like .env variables right

⚠ **Partially correct — but not exactly.**

### What `Properties/` actually does:

- Stores **project & launch metadata**
    
- Common file:
    
    - `launchSettings.json`
        

**Example**

```json
{
  "profiles": {
    "MyApp": {
      "commandName": "Project",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### 🔑 Key distinction:

|`.env` files|`Properties/launchSettings.json`|
|---|---|
|Used at runtime|Used mainly during **local development**|
|Framework-agnostic|.NET-specific|
|Loaded by app|Loaded by tooling (Visual Studio / `dotnet run`)|

📌 So yes, it **can define environment variables**, but:

- Mostly for **local debugging**
    
- Not meant for production
    

---

## 3️⃣ `bin/`

**Your understanding:**

> compiled output

✅ **Exactly right**

Contains:

- `.exe` or `.dll`
    
- Runtime dependencies
    
- Configuration files
    

Example:

```
bin/Debug/net8.0/MyApp.dll
```

📌 This is what actually runs.

---

## 4️⃣ `obj/`

**Your understanding:**

> temporary file

✅ **Correct**

Contains:

- Intermediate build artifacts
    
- Generated files
    
- Cache for faster builds
    

📌 Safe to delete — it will be regenerated.

---

## ✔ Final Corrected Summary

```
.csproj     → project definition (framework, packages, build rules)
Properties/ → launch & debug settings (can set env vars locally)
bin/        → final compiled output (what runs)
obj/        → temporary build files
```

---

If you want, next we can:

- Compare `launchSettings.json` vs `appsettings.json`
    
- Explain how `.env` works in .NET
    
- Walk through what happens during `dotnet build` step by step