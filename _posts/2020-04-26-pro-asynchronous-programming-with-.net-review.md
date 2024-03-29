---
layout: post
title: Pro Asynchronous Programming with .NET
subtitle: Asynchronous programming is an essential skill for the modern .NET developer. Pro Asynchronous Programming with .NET is your guide to using this important programming model to build responsive and scalable applications anywhere on the .NET platform.
---

![Pro Asynchronous Programming with .NET](https://boxxv.github.io/img/multithread/71mFOtFqTNL.jpg "Pro Asynchronous Programming with .NET")

✅ Publisher: [Apress](http://www.apress.com/9781430259206)

✅ Year: December 23, 2013

✅ Authors: Blewett, Richard, Clymer, Andrew, Ltd, Rock Solid Knowledge 

✅ Language: English

✅ Pages: 368

✅ Size: 7.13 MB

✅ Download source code: [pro-asynchronous-programming-w-.net](https://github.com/apress/pro-asynchronous-programming-w-.net)

-----

## Table of contents


### Chapter 1. An Introduction to Asynchronous Programming

1.1 What Is Asynchronous Programming?

1.2 The Drive to Asynchrony

1.3 Mechanisms for Asynchrony
- Multiple Machines
- Multiple Processes
- Multiple Threads

1.4 Thread Scheduling

1.5 Threads and Resources
- Thread-Specific Resources
  + The Stack
  + Thread Local Storage
  + Registers
- Resources Shared by Threads

1.6 Summary

-----

### Chapter 2. The Evolution of the .NET Asynchronous API

2.1 Asynchrony in the World of .NET 1.0
- System.Threading.Thread
  + The Start Method
  + Stopping a Thread
  + Coordinating Threads (Join)
  + Controlling a Thread’s Interaction with COM
  + Issues with the Thread Class
- Using the System Thread Pool
  + Worker and I/O Threads
  + Getting Work on to the Thread Pool

2.2 Changes to Async in .NET 1.1

2.3 Asynchrony in .NET 2.0
- Logical and Physical Separation
- Passing Data into a Thread
- Closures
- SynchronizationContext
- Event-Based Asynchronous Pattern

2.4 Minor Changes in .NET 3.5
- Lambda Expressions
- Thread Pool Heuristics in .NET 3.5

2.5 Big Changes in .NET 4.0
- Remodeling the Thread Pool Queue
- Work-Stealing Queues
- Thread Pool Heuristics in .NET 4.0

2.6 Summary

-----

### Chapter 3. Tasks

3.1 What Is a Task?

3.2 Creating a Compute-Based Task
- Passing Data into a Task
- Dangers of Closures

3.3 Returning Data from a Task
- Creating I/O-Based Tasks

3.4 Error Handling
- Ignoring Errors
  + .NET 4.0
  + .NET 4.5
- Designing Task-Based APIs
- Cancellation
- Progress

3.5 Task Relationships
- Chaining Tasks (Continuations)
  + Why Use Continuations?
- Nested and Child Tasks
  + Why Use Child Tasks?

3.6 Conclusion

-----

### Chapter 4. Basic Thread Safety

4.1 Asynchrony and Data
- It’s Not Always Good to Share
- Immutable State
- Atomic State Transition
- Nonatomic State Transition
- Correctness Is Not the Only Problem
- Thread Safety

4.2 The Interlocked Class
- Basic Operations
- Richer Functions
  + Interlocked.Exchange
  + Interlocked.CompareExchange

4.3 Monitor: The Workhorse of .NET Synchronization
- The lock Keyword
- Timing Out of Monitor Acquisition
- Signaling with Monitors
- Signaling As a Building Block

4.4 Optimizing for Read
- ReaderWriterLock
- ReaderWriterLockSlim

4.5 A Semaphore Out of the Box

4.6 Raising the Starting Gate: ManualResetEventSlim

4.7 CountdownEvent: Simplifying Fork and Join

4.8 Barrier: Rendezvous-Based Synchronization

4.9 Crossing the AppDomain Boundary with WaitHandle
- Mutex
- Semaphore
- Events
- WaitHandle—The Kernel Synchronization Abstraction
- Working with Multiple WaitHandles
  + WaitHandle.WaitAll
  + WaitHandle.WaitAny
  + WaitHandle.SignalAndWait
- Integrating Standard Primitives and Kernel Objects

4.10 Synchronization Is Not the Only Answer

4.11 Conclusion

-----

### Chapter 5. Concurrent Data Structures

5.1 Simplifying Thread Safety

5.2 Lazy<T>

5.3 Concurrent Collections

5.4 ConcurrentDictionary<K,V>
- Locking Mechanics

5.5 ConcurrentQueue<T> and ConcurrentStack<T>

5.6 ConcurrentBag<T>

5.7 Blocking Collections
- Graceful Shutdown
- Consuming Enumerable
- BlockingCollection of X

5.8 Summary

-----

### Chapter 6. Asynchronous UI

6.1 UI Mechanics

6.2 UI Threading Model

6.3 Synchronization Context
- Send and Post
- Task Continuations
- Event-Based Asynchronous Pattern (EAP)
- Background Worker

6.4 Data Binding
- Windows Forms
- Windows Presentation Foundation (WPF)
- WinRT

6.5 WPF Dispatcher
- Obtaining the Dispatcher
- Executing Work Through the Dispatcher

6.6 WinRT Dispatcher
- Obtaining the Dispatcher
- Executing Work Through the Dispatcher

6.7 UI Timers
- Windows Forms Timer
- WinRT and WPF Dispatch Timers

6.8 WPF Freezable Components

6.9 Too Much of a Good Thing

6.10 Summary

-----

### Chapter 7. async and await

7.1 Making Asynchronous Programming Simpler

7.2 What Do async and await Actually Do?
- Returning Values from async Methods
- Should You Always Continue on the UI Thread?
- Task.Delay
- Task.WhenAll
- Task.WhenAll, Error Handling
- Task.WhenAny
- async/await Mechanics

7.3 Summary

-----

### Chapter 8. Everything a Task

8.1 TaskCompletionSource<T>

8.2 Worked Example: Creating a Foreground Task

8.3 Unit Testing and Stubbing Asynchronous Methods

8.4 Building Task-Based Combinators
- Improved WhenAny
- lternative WhenAll, WhenAllOrFail

8.5 Summary

-----

### Chapter 9. Server-Side Async

9.1 Natural Parallelism

9.2 The Problem of I/O

9.3 ASP.NET WebForms
- A Synchronous WebForms Implementation
- Asynchronous Pages in WebForms 4.0
- Asynchronous Pages in WebForms 4.5

9.4 ASP.NET MVC
- Asynchronous MVC Processing in .NET 4.0
- Asynchronous MVC Processing in .NET 4.5

9.5 Windows Communication Foundation
- Asynchronous WCF Services in .NET 4.0
- Asynchronous WCF Services in .NET 4.5

9.6 Using Speech to Text

9.7 Summary

-----

### Chapter 10. TPL Dataflow

10.1 The Building Blocks

10.2 Producer and Consumer Revisited

10.3 Linking Blocks
- Transform Block
- Transform Many Block
- Linking to Multiple Targets

10.4 Shutting Down Gracefully
- Propagating Completion
- Error Handling
- Cancellation

10.5 Glue Blocks
- Buffer Block
- Batch Block
- Broadcast Block
- Joining

10.6 Asynchronous Blocks

10.7 Summary

-----

### Chapter 11. Parallel Programming

11.1 What Is Driving the Need for Parallelism?
- Coarse- and Fine-Grained Parallelism
- Task and Data-Based Parallelism
- Is It Worth Trying to Parallelize Everything?
- Before You Parallelize

11.2 Parallel Class
- Parallel.Invoke
- Parallel Loops

11.3 PLINQ
- Moving from Sequential LINQ to PLINQ
- Influencing and Configuring the Query
- ForAll
- Aggregating Results

11.4 Summary

-----

### Chapter 12. Task Scheduling

12.1 ConcurrentExclusiveSchedulerPair

12.2 Why Write a Task Scheduler?

12.3 The TaskScheduler Abstraction
- Implementing QueueTask
- Implementing GetScheduledTasks
- Implementing TryExecuteTaskInline
- Executing Tasks

12.4 Implementing a Custom Scheduler
- Creating a Basic Implementation
- Adding Threads on Demand
- Removing Idle Threads

12.5 Unit Testing Custom Schedulers
- Controlling Execution Order with Synchronization Primitives
- Adding Members to the Scheduler to Provide Insight
- Deriving a Testable Class from the Scheduler

12.6 Summary

-----

### Chapter 13. Debugging Async with Visual Studio

13.1 Types of Multithreading Bugs
- Data Corruption
- Race Conditions
- Deadlocks
- Runaway Threads

13.2 The Limitations of Using Visual Studio for Debugging
- The Interactive Debugger
- It Works on My Machine

13.3 Multithreaded Visual Studio Debugging Basics
- Breakpoints and Threads
- Locals, Autos, and Watch Windows
- The Call Stack Window
- The Threads Window

13.4 Debugging Tasks
- The Parallel Tasks / Tasks Window
- The Parallel Stacks Window
- The Concurrency Visualizer

-----

### Chapter 14. Debugging Async—Beyond Visual Studio

14.1 Memory Dumps

14.2 Generating a Memory Dump
- Task Manager
- DebugDiag
- ADPLUS

14.3 Analyzing Memory Dump
- WinDbg
- SOS
- SOSEX
- PSSCOR

14.4 Summary


-----

[https://www.apress.com/gp/book/9781430259206](https://www.apress.com/gp/book/9781430259206)  
[https://www.oreilly.com/library/view/pro-asynchronous-programming/9781430259206/](https://www.oreilly.com/library/view/pro-asynchronous-programming/9781430259206/)  
[https://www.amazon.com/Asynchronous-Programming-NET-Richard-Blewett/dp/1430259205](https://www.amazon.com/Asynchronous-Programming-NET-Richard-Blewett/dp/1430259205)

[Pro .NET 4 Parallel Programming in C#](https://www.amazon.com/NET-Parallel-Programming-Experts-Voice/dp/1430229675)