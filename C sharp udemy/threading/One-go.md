# Process
- A process is just a collection of resources that is used by a single instance of an application. Each process is given a virtual address

# Concurrency
Concurrency means:

> Structuring a program so multiple tasks can make progress independently.

# Context switching
## 🔹 Context Switching (Critical)

When switching threads:

1. Save current thread state:
    - CPU registers
    - Instruction pointer
    - Stack pointer
2. Load next thread state

💥 This is expensive because:

- CPU cache invalidation
- Kernel mode switch
# Thread

## what is thread?

## overhead of thread:

- **Thread kernel object**: The operating system allocates and initializes one of these data structures for each thread created in the system. (- Thread ID
	- Priority
	- State (Running, Ready, Blocked)
	- Scheduling info
	- **Thread Context (VERY important)**)
- ⚙️ Thread Context (CPU Snapshot)
	- This is the most critical part.
	- It stores:
		- CPU registers (RAX, RBX, etc.)
		- Instruction pointer (where execution is)
		- Stack pointer
- User-mode stack The user-mode stack is used for local variables and arguments passed to methods. It also contains the address indicating what the thread should execute next when the current method returns. By default, Windows allocates 1 MB of memory for each thread’s user-mode stack
- Kernel-Mode Stack (Protected Execution Stack)
	- When your app calls OS:
		File.Read(...)

Arguments come from **user memory (untrusted)**
### What kernel does:

1. Copies arguments → kernel stack
2. Validates them
3. Executes safely

👉 Prevents malicious modification during execution



---

# ⚙️ Hidden Cost: Not Just Memory

Each thread also adds:

- Scheduler overhead
- Context switching cost
- Cache invalidation
- Kernel bookkeeping



# Process of context switching

Every context switch requires that Windows performs the following actions:
1. Save the values in the CPU’s registers to the currently running thread’s context structure inside the thread’s kernel object.
2. Select one thread from the set of existing threads to schedule next. If this thread is owned by another process, then Windows must also switch the virtual address space seen by the CPU before it starts executing any code or touching any data.
3. Load the values in the selected thread’s context structure into the CPU’s registers.


windows performs context switches about every 30 ms

# Thread Priority in C#

Thread priority determines the **order in which threads are scheduled** for execution by the operating system. In C#, this is controlled via the `Thread.Priority` property.

---

### Priority Levels

C# uses the `ThreadPriority` enum with five levels:

|Priority|Value|Description|
|---|---|---|
|`Lowest`|0|Scheduled least frequently|
|`BelowNormal`|1|Below average scheduling|
|`Normal`|2|**Default** for all threads|
|`AboveNormal`|3|Above average scheduling|
|`Highest`|4|Scheduled most frequently|

---

### Basic Usage

```csharp
Thread highThread = new Thread(() =>
{
    Console.WriteLine("High priority thread running");
});

Thread lowThread = new Thread(() =>
{
    Console.WriteLine("Low priority thread running");
});

highThread.Priority = ThreadPriority.Highest;
lowThread.Priority  = ThreadPriority.Lowest;

highThread.Start();
lowThread.Start();
```

---

### How It Works

- Every new thread starts with `ThreadPriority.Normal` by default.
- The OS **scheduler** uses priority as a _hint_ — not a strict guarantee.
- Higher-priority threads get **more CPU time slices**, but lower-priority threads are not completely starved (the OS prevents that).
- Priority interacts with the **process priority class** set at the OS level.

---

### Practical Example — Priority Comparison

```csharp
using System;
using System.Threading;

class Program
{
    static long highCount = 0, lowCount = 0;

    static void Main()
    {
        Thread high = new Thread(() =>
        {
            while (highCount < 1_000_000) highCount++;
        });

        Thread low = new Thread(() =>
        {
            while (lowCount < 1_000_000) lowCount++;
        });

        high.Priority = ThreadPriority.Highest;
        low.Priority  = ThreadPriority.Lowest;

        high.Start();
        low.Start();

        high.Join();
        low.Join();

        Console.WriteLine($"High count: {highCount}");
        Console.WriteLine($"Low count:  {lowCount}");
    }
}
```

In most runs, the high-priority thread will **finish first**.

---

### Important Caveats

**Priority is not deterministic.** The OS makes the final scheduling decision, so results vary across machines and load conditions.

**Starvation risk.** Setting a thread to `Highest` on a busy system can starve other threads, including UI threads — use with caution.

**Avoid priority in most apps.** Modern best practices favor `Task`/`async-await` over manual thread management. `Task` does not expose priority directly.

**Background vs Foreground threads** are separate from priority — `IsBackground` controls whether a thread keeps the process alive, not how often it runs.

---

### Priority with Task Parallel Library (TPL)

`Task` doesn't support priority natively, but you can work around it:

```csharp
// Workaround: run a Task on a manually created high-priority thread
Task.Factory.StartNew(() =>
{
    Thread.CurrentThread.Priority = ThreadPriority.AboveNormal;
    Console.WriteLine("High-priority task work here");
}, TaskCreationOptions.LongRunning);
```

---

### Quick Summary

- Use `Thread.Priority` to hint at scheduling preference.
- Stick to `Normal` unless you have a **specific, measured reason** to change it.
- Prefer `async/await` and `Task` for most concurrent work in modern C#.


