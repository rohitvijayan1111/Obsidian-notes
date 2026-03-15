
##### **Points to Remember:**

1. TextWriter is an abstract class belonging to the System.IO namespace.
2. It is used to write a sequential series of characters into a file.
3. It is the base class of StreamWriter and StringWriter which is used to write characters to streams and strings respectively.
4. By default, it is not thread-safe.
5. As it is an abstract class, its object cannot be created. Any class implementing TextWriter must minimally implement its Write(Char) method to create its useful instance.
Like StreamWriter there are also other classes that are derived from the TextWriter class and provide the implementation for the members of TextWriter. The following is the list of derived classes with the help of which we can work with TextWriter:

6. **IndentedTextWriter**: It is used to insert a tab string and to track the current indentation level.
7. **StreamWriter**: It is used to write characters to a stream in a particular encoding.
8. **StringWriter**: It is used to write information to a string. The information is stored in an underlying StringBuilder.
9. **HttpWriter**: It provides an object of TextWriter class that can be accessed through the intrinsic HttpResponse object.
10. **HtmlTextWriter**: It is used to write markup characters and text to an ASP.NET server control output stream.

Understanding **`TextReader` and `TextWriter`** is important because they are the **foundation of all text-based I/O in .NET**. Classes like **`StreamReader`, `StreamWriter`, `StringReader`, and `StringWriter`** are built on top of them.

We’ll break it down step-by-step so you see **why they exist, how they work internally, and how other classes derive from them**.

---

# 1️⃣ What Are TextReader and TextWriter?

`TextReader` and `TextWriter` are **abstract base classes** in **`System.IO`**.

They provide a **common interface for reading and writing text data**.

```text
TextReader → reading characters
TextWriter → writing characters
```

They operate on **characters (`char`)**, not bytes.

---

# 2️⃣ Where They Fit in the IO Architecture

Here is the hierarchy.

```text
Object
   ↓
TextReader (abstract)
   ↓
 ├─ StreamReader
 └─ StringReader

Object
   ↓
TextWriter (abstract)
   ↓
 ├─ StreamWriter
 └─ StringWriter
```

They sit **above streams** in the architecture.

Full stack example:

```text
Disk
 ↓
FileStream
 ↓
StreamReader (inherits TextReader)
 ↓
TextReader methods
 ↓
Your program
```

---

# 3️⃣ Why TextReader and TextWriter Exist

Imagine .NET only had `StreamReader` and `StreamWriter`.

Then APIs would look like this:

```csharp
void PrintFile(StreamReader reader)
```

But what if we wanted to read from:

- a **file**
    
- a **string**
    
- a **network stream**
    

Using `TextReader` solves this.

```csharp
void Print(TextReader reader)
```





---

# 4️⃣ TextReader – Purpose

`TextReader` provides **methods to read characters from a text source**.

Typical sources:

|Source|Implementation|
|---|---|
|File|StreamReader|
|Memory string|StringReader|
|Custom stream|Custom reader|

---

# 5️⃣ Important TextReader Methods

### `Read()`

Reads **one character**.

```csharp
int ch = reader.Read();
```

Returns:

```
character code (0-65535)
-1 if end of stream
```

Example:

```csharp
int ch;

while((ch = reader.Read()) != -1)
{
    Console.Write((char)ch);
}
```

---

### `ReadLine()`

Reads **one line of text**.

```csharp
string line = reader.ReadLine();
```

Stops at:

```
\n
\r\n
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

### `ReadToEnd()`

Reads the entire stream.

```csharp
string text = reader.ReadToEnd();
```

Be careful with **large files**.

---

### `Peek()`

Reads the next character **without advancing the cursor**.

```csharp
int ch = reader.Peek();
```

Example:

```
HELLO
^ pointer
```

Peek returns `H`, but pointer stays.

---

### `Close()`

Closes the reader.

```csharp
reader.Close();
```

Usually replaced by:

```csharp
Dispose()
```

---

# 6️⃣ TextWriter – Purpose

`TextWriter` provides **methods for writing characters to a destination**.

Destinations may be:

|Destination|Implementation|
|---|---|
|File|StreamWriter|
|Memory string|StringWriter|
|Console|Console.Out|

Example:

```csharp
TextWriter writer = Console.Out;
```

---

# 7️⃣ Important TextWriter Methods

### `Write()`

Writes text without newline.

```csharp
writer.Write("Hello");
writer.Write(" World");
```

Result:

```
Hello World
```

---

### `WriteLine()`

Writes text plus newline.

```csharp
writer.WriteLine("Hello");
writer.WriteLine("World");
```

Result:

```
Hello
World
```

---

### `Flush()`

Forces buffered data to be written.

```csharp
writer.Flush();
```

Important for **stream writers**.

---

### `Close()`

Closes the writer.

```csharp
writer.Close();
```

---

# 8️⃣ TextWriter Properties

### `Encoding`

Indicates character encoding.

Example:

```csharp
Encoding encoding = writer.Encoding;
```

Common encodings:

```
UTF8
UTF16
ASCII
```

---

### `NewLine`

Defines newline sequence.

Default:

```
Environment.NewLine
```

Example:

```csharp
writer.NewLine = "\n";
```

---

# 9️⃣ Example Using TextReader

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        TextReader reader = new StreamReader("data.txt");

        string text = reader.ReadToEnd();

        Console.WriteLine(text);

        reader.Close();
    }
}
```

Because of polymorphism:

```csharp
TextReader reader = new StringReader("Hello World");
```

Same code works.

---

# 🔟 Example Using TextWriter

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        TextWriter writer = new StreamWriter("data.txt");

        writer.WriteLine("Hello");
        writer.WriteLine("World");

        writer.Close();
    }
}
```

Or writing to console:

```csharp
TextWriter writer = Console.Out;
writer.WriteLine("Hello Console");
```

---

# 1️⃣1️⃣ Relationship With Other Classes

|Class|Base|
|---|---|
|StreamReader|TextReader|
|StringReader|TextReader|
|StreamWriter|TextWriter|
|StringWriter|TextWriter|

Example:

```csharp
TextReader reader = new StreamReader("file.txt");
```

This works because **StreamReader inherits TextReader**.

---

# 1️⃣2️⃣ Internal Design Idea

The base classes define the **common contract**.

Example simplified:

```csharp
abstract class TextReader
{
    public abstract int Read();
    public abstract string ReadLine();
}
```

Derived classes implement them differently.

Example:

```
StreamReader → reads from FileStream
StringReader → reads from string buffer
```

---

# 1️⃣3️⃣ Real-World Use Case

Example method:

```csharp
void PrintLines(TextReader reader)
{
    string line;

    while((line = reader.ReadLine()) != null)
    {
        Console.WriteLine(line);
    }
}
```

Now you can pass:

```csharp
PrintLines(new StreamReader("file.txt"));
PrintLines(new StringReader("Hello\nWorld"));
```

This is **powerful abstraction**.

---

# 1️⃣4️⃣ Summary

`TextReader` and `TextWriter` are **abstract base classes for text I/O**.

They define **standard methods** for working with characters.

```
TextReader
   ↓
StreamReader (file)
StringReader (memory)

TextWriter
   ↓
StreamWriter (file)
StringWriter (memory)
```

They allow APIs to work with **any text source or destination**.

---

✅ **Key insight**

```
Stream → byte level
TextReader/TextWriter → character level
File class → high level helper
```

---

If you'd like, the next extremely useful concept would be understanding **`BinaryReader` and `BinaryWriter` deeply**, because they introduce **structured binary data formats** (which are very different from text streams).