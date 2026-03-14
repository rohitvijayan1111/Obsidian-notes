Before learning **`StreamReader` and `StreamWriter`**, it’s important to know one key idea:

> `StreamReader` and `StreamWriter` **do not access files directly**.  
> They operate **on top of a stream**, usually a `FileStream`.

So the layering becomes:

```text
Disk
 ↓
Operating System
 ↓
FileStream (byte-level stream)
 ↓
StreamReader / StreamWriter (text-level stream)
 ↓
Your C# code (strings)
```

`FileStream` works with **bytes**, while `StreamReader/Writer` work with **text (characters)**.

---

# 1. Why StreamReader and StreamWriter Exist

Files are stored as **bytes**, but applications usually deal with **text**.

Example file content:

```
Hello World
```

On disk this is actually bytes:

```text
48 65 6C 6C 6F 20 57 6F 72 6C 64
```

Handling this manually with `FileStream` is inconvenient.

Example with `FileStream`:

```csharp
FileStream fs = new FileStream("data.txt", FileMode.Open);
byte[] buffer = new byte[100];

int bytesRead = fs.Read(buffer, 0, buffer.Length);
string text = System.Text.Encoding.UTF8.GetString(buffer, 0, bytesRead);
```

`StreamReader` simplifies this.

---

# 2. StreamReader (Reading Text)

`StreamReader` converts **bytes → characters** automatically.

Example:

```csharp
using System.IO;

StreamReader reader = new StreamReader("data.txt");

string text = reader.ReadToEnd();

reader.Close();
```

Simpler with `using`:

```csharp
using StreamReader reader = new StreamReader("data.txt");
string text = reader.ReadToEnd();
```

---

# 3. Internal Working of StreamReader

Internally:

```
Disk
 ↓
OS Page Cache
 ↓
FileStream buffer (bytes)
 ↓
StreamReader buffer (chars)
 ↓
Your string
```

So there are **two buffers**:

1. FileStream byte buffer
    
2. StreamReader character buffer
    

---

# 4. Important StreamReader Methods

### Read()

Reads one character.

```csharp
int ch = reader.Read();
```

Returns:

- character code
    
- `-1` if end of file
    

Example:

```csharp
int ch;
while((ch = reader.Read()) != -1)
{
    Console.Write((char)ch);
}
```

---

### ReadLine()

Reads a single line.

```csharp
string line = reader.ReadLine();
```

Example:

```csharp
string line;

while((line = reader.ReadLine()) != null)
{
    Console.WriteLine(line);
}
```

---

### ReadToEnd()

Reads the entire file.

```csharp
string text = reader.ReadToEnd();
```

Good for **small files**, but not for huge files.

---

# 5. StreamWriter (Writing Text)

`StreamWriter` converts **characters → bytes**.

Example:

```csharp
using StreamWriter writer = new StreamWriter("data.txt");

writer.WriteLine("Hello");
writer.WriteLine("World");
```

File content becomes:

```
Hello
World
```

---

# 6. Internal Working of StreamWriter

```
Your string
 ↓
StreamWriter char buffer
 ↓
Encoding (UTF-8 etc.)
 ↓
FileStream byte buffer
 ↓
OS cache
 ↓
Disk
```

So writing involves **encoding characters into bytes**.

---

# 7. Important StreamWriter Methods

### Write()

Writes text without newline.

```csharp
writer.Write("Hello ");
writer.Write("World");
```

Output:

```
Hello World
```

---

### WriteLine()

Writes text plus newline.

```csharp
writer.WriteLine("Hello");
writer.WriteLine("World");
```

Output:

```
Hello
World
```

---

### Flush()

Forces buffered data to be written.

```csharp
writer.Flush();
```

Normally flushing happens automatically when closing.

---

# 8. Encoding

Text files must use an **encoding**.

Common encodings:

- UTF-8
    
- UTF-16
    
- ASCII
    

Example:

```csharp
using StreamWriter writer =
    new StreamWriter("data.txt", false, System.Text.Encoding.UTF8);
```

Encoding controls how characters become bytes.

Example:

```
A → 41 (ASCII)
€ → E2 82 AC (UTF-8)
```

---

# 9. Relationship Between Classes

```
Stream (abstract base class)
      │
      ├── FileStream
      │
      ├── NetworkStream
      │
      └── MemoryStream

Text layer
      │
      ├── StreamReader
      └── StreamWriter
```

`StreamReader/Writer` can wrap **any stream**, not just files.

Example:

```csharp
FileStream fs = new FileStream("data.txt", FileMode.Open);
StreamReader reader = new StreamReader(fs);
```

---

# 10. Example: Complete Read Program

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        using StreamReader reader = new StreamReader("data.txt");

        string line;

        while((line = reader.ReadLine()) != null)
        {
            Console.WriteLine(line);
        }
    }
}
```

---

# 11. Example: Complete Write Program

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        using StreamWriter writer = new StreamWriter("data.txt");

        writer.WriteLine("First line");
        writer.WriteLine("Second line");
    }
}
```

---

# 12. FileStream vs StreamReader/Writer

|Feature|FileStream|StreamReader/Writer|
|---|---|---|
|Data type|bytes|text|
|Encoding|manual|automatic|
|Usage|binary files|text files|
|Examples|images, PDFs|logs, config files|

---

# Final Mental Model

```
Text File Reading

Disk
 ↓
FileStream (byte stream)
 ↓
StreamReader (text decoder)
 ↓
string in your program
```

```
Text File Writing

string
 ↓
StreamWriter (encoding)
 ↓
FileStream
 ↓
Disk
```

---

If you want, the **next powerful concept** to learn is:

**How asynchronous file reading works (`ReadAsync`, `WriteAsync`) and why it is much faster for large files and servers.**

It also connects with **I/O completion ports and OS async I/O**, which builds directly on everything we discussed.