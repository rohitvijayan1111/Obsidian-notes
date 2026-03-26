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


# Thread pool

A **Thread Pool** is a collection of pre-created, reusable worker threads managed by the .NET runtime. Instead of creating and destroying threads manually, you submit work items and the pool handles execution efficiently.

---

### Why Thread Pool?

|Problem with Manual Threads|Thread Pool Solution|
|---|---|
|Thread creation is expensive (~1MB stack, OS overhead)|Threads are pre-created and reused|
|Too many threads causes context-switching overhead|Pool limits and manages thread count|
|Developer manages thread lifecycle|Runtime handles it automatically|
|No built-in load balancing|Pool dynamically adjusts thread count|

---

### How It Works Internally

```
Your Code                  Thread Pool                    OS
   │                           │                           │
   │── Submit Work Item ───────▶│                           │
   │                           │── Assign to idle thread ──▶│
   │                           │                           │── Execute Work
   │                           │◀── Thread becomes idle ───│
   │                           │── Pick next work item ────▶│
   │                           │                           │
```

The pool maintains a **global queue** for work items, and each thread also has a **local queue** (work-stealing queue) for better performance.

---

### Core Architecture

csharp

```csharp
/*
  Thread Pool Internal Structure:
  
  ┌─────────────────────────────────────────┐
  │             Thread Pool                 │
  │                                         │
  │  Global Queue: [Task1][Task2][Task3]... │
  │                                         │
  │  Worker Threads:                        │
  │  ┌──────────┐  ┌──────────┐            │
  │  │ Thread 1 │  │ Thread 2 │  ...       │
  │  │ LocalQ:[]│  │ LocalQ:[]│            │
  │  └──────────┘  └──────────┘            │
  │                                         │
  │  Min Threads: Environment.ProcessorCount│
  │  Max Threads: 32767 (default)           │
  └─────────────────────────────────────────┘
*/
```


### Ways to Use the Thread Pool

```
 ThreadPool.QueueUserWorkItem(DoWork, "Hello from pool!");
- Task<int> t2 = Task.Run(() => { Console.WriteLine($"Task 2 on Thread: {Thread.CurrentThread.ManagedThreadId}"); return 42; }); await Task.WhenAll(t1, t2
-   Parallel.ForEach(data, number => { Console.WriteLine($"Processing {number} on Thread {Thread.CurrentThread.ManagedThreadId}"); 

   ThreadPool.GetMinThreads(out int minWorker, out int minIO);
        ThreadPool.GetMaxThreads(out int maxWorker, out int maxIO);

        Console.WriteLine($"Min Worker Threads : {minWorker}");
        Console.WriteLine($"Min IO Threads     : {minIO}");
        Console.WriteLine($"Max Worker Threads : {maxWorker}");
        Console.WriteLine($"Max IO Threads     : {maxIO}");
```


# explain more into the working of the thread pool (theoritical)

## Deep Dive: How the Thread Pool Works Internally

---

### The Big Picture

The .NET Thread Pool is not just a "bag of threads." It is a **sophisticated scheduling and resource management system** built into the CLR (Common Language Runtime). It sits between your application code and the operating system, acting as an intelligent broker for concurrent work.

---

### Layer Architecture

The thread pool operates across three distinct layers:

**Layer 1 — Your Application** You submit work via `Task.Run`, `QueueUserWorkItem`, or `Parallel`. You never directly touch threads here.

**Layer 2 — CLR Thread Pool** The CLR manages queues, thread lifecycle, throttling, and the hill-climbing algorithm. This is the brain of the operation.

**Layer 3 — Operating System** The OS kernel performs actual CPU scheduling. It decides which thread runs on which core at any given nanosecond.

The thread pool operates entirely in Layer 2, abstracting away Layer 3 complexity from your code.

---

### Internal Components in Detail

The thread pool is composed of five major internal components that work together:

**1. Global Queue** **2. Local Work-Stealing Queues** **3. I/O Completion Port (IOCP)** **4. Thread Injection / Retirement Logic** **5. Hill-Climbing Algorithm**

Let's go through each one deeply.

---

### 1. The Global Queue

When you submit a work item via `ThreadPool.QueueUserWorkItem` or `Task.Run` from a non-pool thread, the work item lands in the **Global Queue**.

The global queue is a **thread-safe FIFO queue** protected by a lock. All pool worker threads compete to dequeue from it. This means:

- Work items are generally processed in submission order.
- Under high concurrency, threads contend for the lock, which is a bottleneck.
- This is why the local queue system was introduced — to reduce this contention.

The global queue is the "cold path" — it is used when work enters from outside the pool.

---

### 2. Local Work-Stealing Queues (The Hot Path)

Each worker thread in the pool has its own **local double-ended queue (deque)**. This is the most important performance optimization in the thread pool.

**How items enter the local queue:** When a pool thread itself creates new tasks (spawning child tasks inside a `Task.Run`), those child tasks go into that thread's _local queue_ instead of the global queue. This completely avoids lock contention on the global queue.

**How items leave the local queue:** The owning thread pops work from the **top** of its local deque (LIFO order). This is intentional — the most recently queued task is likely still "warm" in the CPU cache, giving better cache locality.

**Work Stealing:** When a thread runs out of local work, instead of going idle, it becomes a **thief**. It looks at other threads' local deques and steals work from the **bottom** (the oldest end). This is why it's called a work-stealing queue — stealing from the bottom while the owner pops from the top means they never conflict on the same end, minimizing synchronization.

This design means:

- Threads stay busy as long as any work exists anywhere in the system.
- Cache-warm tasks run on the thread that created them.
- Inter-thread coordination is minimized.

---

### 3. I/O Completion Port (IOCP)

The thread pool actually contains **two separate pools**:

**Worker Thread Pool** — handles CPU-bound work items (your `Task.Run` lambdas, `QueueUserWorkItem` callbacks).

**I/O Thread Pool** — handles completion of asynchronous I/O operations (file reads, network calls, database queries).

The I/O thread pool is built on top of the Windows **I/O Completion Port** (IOCP) mechanism, or its equivalent on Linux/macOS. Here is how it works:

When you do `await File.ReadAllTextAsync(...)`, the .NET runtime issues the I/O request to the OS and **immediately releases the thread back to the pool**. The thread does not sit and wait. The OS performs the I/O asynchronously in the kernel.

When the I/O completes, the OS places a completion notification on the IOCP. An I/O pool thread picks up that notification and executes the continuation — the code after your `await`.

This is why `async/await` is so powerful. A single I/O thread can service thousands of in-flight I/O operations, because it only activates when an operation actually completes, not while waiting.

---

### 4. Thread Injection and Retirement Logic

The pool dynamically changes the number of active threads based on load. This logic answers two questions: **when to add a thread** and **when to remove a thread**.

**Thread Injection (Adding Threads):**

When all current worker threads are busy and new work items are sitting in the global queue waiting, the pool considers injecting a new thread. However, it does not inject immediately — it waits approximately **500 milliseconds** before adding a new thread.

This delay is intentional. Many workloads have short bursts where threads are briefly busy. If the pool injected immediately on every queue backup, it would create far too many threads during transient spikes. The 500ms gate prevents this overreaction.

If work items are still waiting after 500ms, a new thread is injected. This continues until either the queue drains or the maximum thread count is reached.

**Thread Retirement (Removing Threads):**

When a thread has been idle for approximately **2 minutes**, it is retired and its OS resources are reclaimed. This keeps the pool lean during low-activity periods.

The minimum thread count acts as a floor — the pool will never retire below the minimum, ensuring a baseline of threads is always ready for immediate work.

---

### 5. The Hill-Climbing Algorithm

This is the most intellectually interesting part of the thread pool. The hill-climbing algorithm is responsible for continuously tuning the number of active threads to **maximize throughput**, not just keep threads busy.

**The core insight:** More threads do not always mean more throughput. Beyond a certain point, adding threads introduces context-switching overhead that actually reduces throughput. The optimal thread count depends on the workload, hardware, and current system state — and it changes over time.

**How hill-climbing works:**

The algorithm treats thread count as a variable to optimize, and throughput (work items completed per second) as the metric to maximize. It works like this:

It observes the current throughput at the current thread count. Then it makes a small experimental change — either adding or removing a thread — and observes the new throughput. If throughput improved, it continues moving in that direction (like climbing a hill). If throughput decreased, it reverses direction.

This is a form of **stochastic gradient ascent**. The "hill" is the throughput curve as a function of thread count, and the algorithm continuously searches for the peak of that curve.

The algorithm samples throughput every 200 milliseconds and makes adjustments. It is designed to react quickly to workload changes while avoiding wild oscillations in thread count.



# Execution Context:

## Execution Context in C#

---

### What is Execution Context?

An **Execution Context** is a container that captures and carries the _ambient environment_ of a thread — all the contextual information that defines "who is running this code, under what conditions, and with what identity."

When work moves from one thread to another (via thread pool, `Task`, `await`, etc.), the execution context **flows automatically** with it, ensuring the new thread has the same contextual environment as the originating thread.

Think of it as the **invisible backpack** every thread carries — containing identity, security permissions, diagnostic data, and more. When you hand work to another thread, you hand it a copy of your backpack.

---

### Why Does It Exist?

Without execution context, the following problems would occur:

- A thread pool thread picks up your work but **loses your user identity** — security checks fail.
- A log message from an async continuation has **no correlation ID** — distributed tracing breaks.
- A child task cannot access **ambient data** set by its parent — context-dependent logic silently fails.
- Impersonation set before an `await` **disappears** after the await resumes — security holes open up.

Execution context exists to make threading **transparent** with respect to ambient environment.

---

### What Does Execution Context Contain?

Execution context is not a single value — it is a **composite of several sub-contexts**, each responsible for a different concern:

```
ExecutionContext
│
├── SecurityContext
│     ├── WindowsIdentity (impersonation)
│     └── Permission sets
│
├── SynchronizationContext
│     └── How continuations are scheduled
│           (UI thread, ASP.NET request thread, etc.)
│
├── LogicalCallContext
│     └── Logical data slots (legacy remoting)
│
├── AsyncLocal<T> values
│     └── Ambient data that flows across awaits
│
└── CallContext (legacy)
```

---

### 1. SecurityContext — Identity and Permissions

The `SecurityContext` carries the **Windows identity and permission grants** of the originating thread. It ensures that when work is offloaded to a pool thread, the pool thread runs with the same security identity.

```csharp
using System;
using System.Security.Principal;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // Simulate setting a custom identity on the current thread
        var identity = new GenericIdentity("Alice");
        var principal = new GenericPrincipal(identity, new[] { "Admin" });
        Thread.CurrentPrincipal = principal;

        Console.WriteLine($"Before await: {Thread.CurrentPrincipal.Identity.Name}");
        // Output: Alice

        await Task.Delay(100);

        // Even though we may be on a different thread now,
        // the principal flows through execution context
        Console.WriteLine($"After await: {Thread.CurrentPrincipal.Identity.Name}");
        // Output: Alice  ← context flowed automatically
    }
}
```

---

### 2. SynchronizationContext — Where Continuations Run

`SynchronizationContext` answers the question: **"Which thread should run the code after an await?"**

Different environments install different synchronization contexts:

|Environment|SynchronizationContext|Effect|
|---|---|---|
|WinForms / WPF|`WindowsFormsSyncContext` / `DispatcherSyncContext`|Continuations run on UI thread|
|ASP.NET (classic)|`AspNetSynchronizationContext`|Continuations run on request thread|
|Console / ASP.NET Core|`null` (no context)|Continuations run on any pool thread|
|Unit Test frameworks|Custom context|Continuations run in test context|

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // Console app has no SynchronizationContext (null)
        Console.WriteLine($"SyncContext: {SynchronizationContext.Current ?? null}");
        // Output: null

        await Task.Delay(100);

        // Continuation runs on thread pool — any available thread
        Console.WriteLine($"Thread after await: {Thread.CurrentThread.ManagedThreadId}");
    }
}
```

**ConfigureAwait(false)** explicitly tells the awaiter to **not capture** the synchronization context, allowing the continuation to run on any pool thread — a critical performance optimization in library code:

```csharp
// Library code — don't force continuation onto original context
await SomeOperationAsync().ConfigureAwait(false);
// Continuation runs on thread pool, not UI thread
// Avoids deadlocks in certain synchronization contexts
```

---

### 3. AsyncLocal<T> — The Most Important Flow Mechanism

`AsyncLocal<T>` is the modern, correct way to flow ambient data across async operations. It is the backbone of how frameworks like ASP.NET Core flow request data, correlation IDs, and more.

**Key behavior:** Values set in a parent flow **down** to children, but changes made in a child do **not** flow back up to the parent.

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    // Declare an AsyncLocal — flows across awaits and child tasks
    static AsyncLocal<string> _correlationId = new AsyncLocal<string>();

    static async Task Main()
    {
        _correlationId.Value = "REQ-001";
        Console.WriteLine($"Main: {_correlationId.Value}");
        // Output: REQ-001

        await ChildOperationAsync();

        // Child's change does NOT affect parent
        Console.WriteLine($"Main after child: {_correlationId.Value}");
        // Output: REQ-001  ← unchanged
    }

    static async Task ChildOperationAsync()
    {
        // Receives parent's value
        Console.WriteLine($"Child start: {_correlationId.Value}");
        // Output: REQ-001

        // Modifying creates a new scope — does not affect parent
        _correlationId.Value = "REQ-001-CHILD";

        await Task.Delay(50);

        Console.WriteLine($"Child end: {_correlationId.Value}");
        // Output: REQ-001-CHILD
    }
}
```

**Real-world use — Correlation ID flowing through an entire request:**

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class RequestPipeline
{
    static AsyncLocal<string> _requestId = new AsyncLocal<string>();

    // Simulates middleware setting a request ID
    static async Task HandleRequestAsync(string requestId)
    {
        _requestId.Value = requestId;
        await ProcessAsync();
    }

    static async Task ProcessAsync()
    {
        // No need to pass requestId as parameter — it flows automatically
        Console.WriteLine($"[{_requestId.Value}] Processing started");
        await SaveToDatabaseAsync();
    }

    static async Task SaveToDatabaseAsync()
    {
        // Still accessible deep in the call chain
        Console.WriteLine($"[{_requestId.Value}] Saving to DB");
        await Task.Delay(100);
        Console.WriteLine($"[{_requestId.Value}] Save complete");
    }

    static async Task Main()
    {
        await Task.WhenAll(
            HandleRequestAsync("REQ-ABC"),
            HandleRequestAsync("REQ-XYZ")
        );
        // Each request's ID flows independently — no mixing
    }
}
```

---

### 4. How Context Flows — The Copy-on-Write Mechanism

Execution context uses a **copy-on-write** strategy for efficiency. Understanding this is critical.

When a thread spawns a child task, the runtime does **not** immediately deep-copy the entire execution context — that would be expensive. Instead, it marks the context as **shared**.

Only when a thread **modifies** a value in its context does the runtime create a **private copy** for that thread. This means:

- Reading ambient data = zero allocation cost.
- Writing ambient data = one copy created, isolated from the parent.
- Parent and child can both read the original values freely with no copying.

```
Parent Thread
  _correlationId = "REQ-001"
       │
       │── spawns child task (context is SHARED, not copied yet)
       │
  Child Thread
       │  reads _correlationId → "REQ-001"  (no copy, reads shared)
       │
       │  writes _correlationId = "REQ-CHILD"
       │  ↓
       │  NOW a copy is made for child only
       │  Child's copy: _correlationId = "REQ-CHILD"
       │  Parent's original: _correlationId = "REQ-001"  ← untouched
```

---

### 5. Suppressing Context Flow

Sometimes you explicitly **do not want** context to flow — for fire-and-forget background work that should be independent of the caller's context:

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    static AsyncLocal<string> _data = new AsyncLocal<string>();

    static void Main()
    {
        _data.Value = "ImportantData";

        // Suppress context flow for background work
        using (ExecutionContext.SuppressFlow())
        {
            Task.Run(() =>
            {
                // Context was NOT flowed — data is gone here
                Console.WriteLine(_data.Value ?? "null");
                // Output: null
            });
        }
        // Flow is automatically restored after the using block

        // Normal task — context flows
        Task.Run(() =>
        {
            Console.WriteLine(_data.Value);
            // Output: ImportantData
        });

        Console.ReadLine();
    }
}
```

**When to suppress:**

- Background telemetry or logging tasks that should not inherit caller's security identity.
- Fire-and-forget operations that are fully independent.
- Performance-critical paths where context overhead is measurable.

---

### 6. Execution Context vs Synchronization Context

These two are frequently confused but serve completely different purposes:

||ExecutionContext|SynchronizationContext|
|---|---|---|
|**Purpose**|Carries ambient data (who, what, diagnostics)|Controls where continuations are scheduled|
|**Flows across awaits?**|Yes, always|Yes, unless ConfigureAwait(false)|
|**Can be suppressed?**|Yes, explicitly|Yes, via ConfigureAwait(false)|
|**Contains**|Security, AsyncLocal values|Scheduling mechanism|
|**Changed by**|Setting AsyncLocal values|Installing a new SyncContext|
|**Used by**|CLR, identity, logging|UI frameworks, ASP.NET|

A simple way to remember it: `ExecutionContext` is about **data**, `SynchronizationContext` is about **location**.

---

### The Full Flow Diagram

```
Thread A                     Thread Pool
    │                             │
    │  _asyncLocal = "REQ-001"    │
    │  Task.Run(() => Work())     │
    │──── captures ExecutionContext ──────────────────▶│
    │                             │  (copy-on-write)   │
    │                             │  Work() executes   │
    │                             │  _asyncLocal still "REQ-001"
    │                             │  _asyncLocal = "CHILD"
    │                             │  → new copy created for this thread
    │                             │  → Thread A's value unchanged
    │◀────────────────────────────│
    │  _asyncLocal = "REQ-001"    │  ← Thread A unaffected
```

---

### Key Takeaways

`ExecutionContext` is the **invisible environment** that travels with every unit of async work in .NET. It ensures that identity, permissions, diagnostic data, and ambient values are preserved transparently across thread boundaries, async continuations, and parallel tasks — without you having to manually pass them through every method signature.

The four things to firmly understand are: it **flows automatically**, it uses **copy-on-write** for efficiency, child modifications **never affect parents**, and it can be **suppressed** when isolation is needed. Everything else in async programming builds on these four behaviors.