The **`File` class in C#** is a **static utility class** used for performing common file operations **without manually creating a `FileStream`**.

It belongs to the **`System.IO`** namespace.

Think of it like this:

```text
File class → High-level helper
FileStream → Low-level byte stream
```

So the `File` class internally **creates and uses `FileStream` for you**.

---

# 1. Key Idea of the File Class

The `File` class is:

- **Static**
    
- Provides **shortcut methods**
    
- Used for **simple file operations**
    

Example:

Instead of this (manual):

```csharp
using FileStream fs = new FileStream("data.txt", FileMode.Create);
byte[] data = Encoding.UTF8.GetBytes("Hello");
fs.Write(data, 0, data.Length);
```

You can do:

```csharp
File.WriteAllText("data.txt", "Hello");
```

The `File` class internally does:

```text
Create FileStream
Write data
Close stream
```

---

# 2. Common Operations Provided by File Class

The `File` class mainly provides methods for:

```text
1. Creating files
2. Reading files
3. Writing files
4. Copying files
5. Moving files
6. Deleting files
7. Checking existence
8. File attributes
```

---

# 3. Creating a File

### `File.Create()`

Creates a file and returns a `FileStream`.

```csharp
FileStream fs = File.Create("data.txt");
```

Example:

```csharp
using FileStream fs = File.Create("data.txt");
```

If the file exists → it is **overwritten**.

---

# 4. Checking if File Exists

### `File.Exists()`

```csharp
bool exists = File.Exists("data.txt");
```

Example:

```csharp
if (File.Exists("data.txt"))
{
    Console.WriteLine("File exists");
}
```

Important:

```text
Returns false if file doesn't exist OR access denied
```

---

# 5. Reading Files

### `File.ReadAllText()`

Reads entire file as a string.

```csharp
string text = File.ReadAllText("data.txt");
```

Example file:

```
Hello
World
```

Result:

```text
"Hello\nWorld"
```

---

### `File.ReadAllLines()`

Returns an array of strings.

```csharp
string[] lines = File.ReadAllLines("data.txt");
```

Example result:

```text
lines[0] = "Hello"
lines[1] = "World"
```

---

### `File.ReadAllBytes()`

Reads binary data.

```csharp
byte[] data = File.ReadAllBytes("image.png");
```

Used for:

- images
    
- pdf files
    
- binary files
    

---

# 6. Writing Files

### `File.WriteAllText()`

Writes text to a file.

```csharp
File.WriteAllText("data.txt", "Hello World");
```

If file exists → **overwritten**.

---

### `File.WriteAllLines()`

Writes multiple lines.

```csharp
string[] lines = { "Hello", "World" };

File.WriteAllLines("data.txt", lines);
```

File becomes:

```
Hello
World
```

---

### `File.WriteAllBytes()`

Writes binary data.

```csharp
byte[] data = { 65, 66, 67 };

File.WriteAllBytes("data.txt", data);
```

Result:

```
ABC
```

---

# 7. Appending Data

### `File.AppendAllText()`

Adds text at the end.

```csharp
File.AppendAllText("log.txt", "New entry\n");
```

---

### `File.AppendAllLines()`

```csharp
File.AppendAllLines("log.txt", lines);
```

---

# 8. Copying Files

### `File.Copy()`

```csharp
File.Copy("source.txt", "dest.txt");
```

Overwrite example:

```csharp
File.Copy("source.txt", "dest.txt", true);
```

---

# 9. Moving Files

### `File.Move()`

```csharp
File.Move("old.txt", "new.txt");
```

This can also move files between directories.

---

# 10. Deleting Files

### `File.Delete()`

```csharp
File.Delete("data.txt");
```

Important:

```text
No exception if file doesn't exist
```

But will fail if:

```text
File is open
Permission denied
```

---

# 11. File Attributes

### `File.GetAttributes()`

```csharp
var attr = File.GetAttributes("data.txt");
```

Example attributes:

```text
ReadOnly
Hidden
System
Archive
```

---

### `File.SetAttributes()`

```csharp
File.SetAttributes("data.txt", FileAttributes.ReadOnly);
```

---

# 12. File Time Information

### Creation time

```csharp
DateTime created = File.GetCreationTime("data.txt");
```

---

### Last modified time

```csharp
DateTime modified = File.GetLastWriteTime("data.txt");
```

---

# 13. Asynchronous Methods

Modern .NET also provides async versions.

### `ReadAllTextAsync()`

```csharp
string text = await File.ReadAllTextAsync("data.txt");
```

---

### `WriteAllTextAsync()`

```csharp
await File.WriteAllTextAsync("data.txt", "Hello");
```

These are useful for:

```text
Web applications
Large files
Non-blocking I/O
```

---

# 14. File Class vs FileStream

|Feature|File Class|FileStream|
|---|---|---|
|Type|Static helper|Stream class|
|Complexity|Simple|Low-level|
|Control|Limited|Full control|
|Use case|Small files|Large files / advanced I/O|

Example:

```text
File.ReadAllText → simple
FileStream.Read  → controlled streaming
```

---

# 15. Internal Working

Example:

```csharp
File.WriteAllText("data.txt", "Hello");
```

Internally:

```text
File.WriteAllText
       ↓
Creates FileStream
       ↓
Creates StreamWriter
       ↓
Writes text
       ↓
Closes stream
```

So the actual stack is:

```text
File class
   ↓
StreamWriter
   ↓
FileStream
   ↓
OS file system
   ↓
Disk
```

---

# 16. When to Use File Class

Use `File` class when:

```text
✔ File is small
✔ Simple read/write
✔ No streaming needed
```

Use `FileStream` when:

```text
✔ Large files
✔ Partial reads
✔ Custom buffering
✔ High performance
```

---

# Final Summary

The **`File` class** is a **high-level static helper** that simplifies file operations.

It provides methods like:

```text
Create
Exists
ReadAllText
ReadAllLines
WriteAllText
WriteAllLines
Copy
Move
Delete
Append
```

Internally it still uses:

```text
FileStream
StreamReader
StreamWriter
```

to interact with the operating system.

---

If you want, I can also explain the **`FileInfo` class**, which is closely related but works using **object instances instead of static methods**.