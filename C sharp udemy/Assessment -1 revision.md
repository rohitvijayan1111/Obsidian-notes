- **COM** stands for **Component Object Model.** existed before .NET
- There are two major disadvantages of the COM Framework. They are as follows:

1. Incomplete Object-Oriented Programming means it will not support all the features of OOPs.
2. Platform Dependent means COM applications can run on only Windows OS.

To overcome the above problems, Microsoft introduces **.NET Framework**.


##### **What does .NET Represent?**

**NET** stands for **Network Enabled Technology** (Internet). In .NET, dot (.) refers to **Object-Oriented,** and NET refers to the internet. So, the complete .NET means through Object-Oriented we can implement internet-based applications.
- Supports cross platform and supports multiple languages.


##### **What is a Framework?**

A framework is a software. Or you can say a framework is a collection of many small technologies integrated together to develop applications that can be executed anywhere.

**What does the .NET Framework Provide?**

The DOT NET Framework provides two things as follows

1. **BCL** (Base Class Libraries)
2. **CLR** (Common Language Runtime)

##### **What is BCL?**

Base Class Libraries (BCL) are designed by Microsoft. Without BCL we can’t write any code in .NET. So, BCL is also known as the basic building block of .NET Programs.

1. **BCL:** The **Base** **Class Library** provides a set of APIs and types for common functionality. It provides types for strings, dates, numbers, etc. The Class Library includes APIs for reading and writing files, connecting to databases, drawing, and more.
##### **What is CLR?**

CLR stands for Common Language Runtime and it is the core component under the .NET framework which is responsible for converting the MSIL (Microsoft Intermediate Language) code into native code. In our CLR session, we will discuss **CLR** in detail.

- Two phase of compilation (By Compiler - converts C# code into MSIL or IL), By CLR (using JIT) to convert MSIL into machine code /native code (native code means code specific to the Operating system)
  
1. **CLR**: The **Common Language Runtime (CLR)** is the execution engine that handles running applications. It provides services like thread management, garbage collection, type safety, exception handling, and more.
- The compiled source code is stored in the assembly as .dll file . The CLR uses this files during runtime to run the application.

##### **What is Exactly .NET?**

.NET is a framework tool that supports many programming languages and many technologies.
- Had three types of .NET:
	- NET Framework - old one, majorly supported windows OS
	- .NET or .NET - cross platform
	- Xamarian - supports mobile application both android and ios

###### **C# is Compiled and Interpreted:**

We know a programming language is either compiled or interpreted. But C# combines both approaches. That’s why C# is called a two-stage system.

First C# compiler CSC translates source code into an intermediate language code known as MSIL (Microsoft Intermediate Language) or CIL (Common Intermediate Language) code. But these MSIL or CIL or IL codes are not machine instructions. So, in the second stage, these MSIL or CIL, or IL codes are interpreted by the C# interpreter (One Component of CLR called JIT- Just in Time Compiler). As a result, machine instructions will be generated which are directly executed by the machine. Hence, we are saying C# is both interpreted and compiled language.

# structure of a program

- namespace (using system, and namespace to hold classes)
- there must be a startup class to hold the main function.


# Console class

- used for IO

PROPERTIES:

- Foregroundcolor
- Backgroundcolor
- Title.

Methods:
- Beep()
- Read() -> reads a character and returns ascii
- ReadLine()
- Write()
- WriteLine()
- ReadKey()


Convert.ToInt32() -> used to convert from various types into int (parseInt only string input). But For string input Convert.ToInt32() internally uses .parseInt


# Datatypes

- byte (1 byte) - range (0 to 255) (By default unsigned, if need signed use sbyte, can store character(ASCII), byte array)

- Char (2 bytes) - used to store character. Follows UTF-16
- Short (2 bytes) or Convert.Int16 
- int (4 bytes) ot Convert.Int32
- long (8 bytes) - Convert.Int64
If need usigned use uChar, etc
So, the byte data type is good if you are reading the raw data or binary data, or the data without doing any kind of transformations or encoding. And char data type is good when you want to represent or show multilingual data or Unicode data to the end user.


##### **When to use Signed and when to use unsigned data type in C#?**

See, if you want to store only positive numbers, then it is recommended to use an unsigned data type, why because with a signed **short data type** the maximum positive number that you can store is **32767** but with unsigned **ushort** data type the maximum positive number you can store is **65535**.

##### **Comparison between Float, Double, and Decimal:**

###### **Size:**

1. Float uses 4 Bytes or 32 bits to represent data.
2. Double uses 8 Bytes or 64 bits to represent data.
3. Decimal uses 16 Bytes or 128 bits to represent data.
###### **Example to Understand Accuracy:**

If you are using a float, then it will print a maximum of 7 digits, if you are using double, maximum it will print 15 digits and if you are using a decimal maximum, it will print 29 digits.