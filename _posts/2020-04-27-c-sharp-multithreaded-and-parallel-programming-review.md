---
layout: post
title: C# Multithreaded and Parallel Programming
subtitle: Develop powerful C# applications to take advantage of today's multicore hardware
---

![placeholder](http://boxxv.com/img/multithread/8321en_cov.jpg "C# Multithreaded and Parallel Programming")

✅ Publisher: [Packt Publishing](https://www.packtpub.com/application-development/c-multithreaded-and-parallel-programming)

✅ Year: December 24, 2014

✅ Authors: Rodney Ringler

✅ Language: English

✅ Pages: 346

✅ Size: 27.7 MB

✅ Download source code: [9781849688321_code.zip](https://www.packtpub.com/codedownloaderrata/index/index/sku/9781849688321)

-----

### Learn
- Explore all the essential methods used for programming multithreaded applications
- Enhance the performance of an application by designing various parallel operations to achieve concurrency
- Build powerful applications using the Task Parallel Library (TPL), which makes concurrent processing of items in a data collection simple
- Implement data parallelism using the Parallel library, concurrent collections, and PLINQ
- Debug your multithreaded applications using the Threads view, Tasks window, Parallel Stacks window, and Parallel Watch window
- Accomplish any given parallel task using two of the most popular parallel patterns for development: Pipelining and producer-consumer
- Get to grips with the Asynchronous Programming Model (APM) to learn to begin and end asynchronous operations

### About
Most modern machines have dual-core processors. This means that the present-day computer has the ability to multitask. Using multiple cores means your applications can process data faster and be more responsive to users. However, to fully exploit this in your applications, you need to write multithreading code.

We will begin by covering some techniques that have been around since the beginning of .NET, including the BackgroundWorker component, timers, and the Thread class. We will use tasks, task factories, and parallel loops to develop multithreaded applications at a higher level than directly creating and managing individual threads. Finally, we will look at the tools Visual Studio provides for debugging parallel applications, common concurrent design patterns, and the latest updates in PLINQ and async.

### Features
- Make use of the latest Visual Studio debugging tools, to manage and debug multiple threads running simultaneously
- Learn how to use the Thread, Task, and Parallel libraries in your C# applications
- Explore the evolution of multithreaded development in C#, starting with BackgroundWorker classes and moving on to threads and tasks and finally covering Async


-----

## Table of contents


### Chapter 1: Understanding Multiprocessing and  Multiple Cores

1.1 [Mono-processor systems – the old gladiators](https://subscription.packtpub.com/book/programming/9781849688321/1/ch01lvl1sec08/mono-processor-systems---the-old-gladiators)
- Single core – only one warrior to fight against everybody
- Doing a tiny bit of each task

1.2 [Multiprocessor systems – many warriors to win a battle](https://subscription.packtpub.com/book/programming/9781849688321/1/ch01lvl1sec09/multiprocessor-systems---many-warriors-to-win-a-battle)

1.3 [Multiple core processors and hyperthreading](https://subscription.packtpub.com/book/programming/9781849688321/1/ch01lvl1sec10/multiple-core-processors-and-hyperthreading)
- Taking advantage of multiple execution cores

1.4 [Examining our hardware](https://subscription.packtpub.com/book/programming/9781849688321/1/ch01lvl1sec11/examining-our-hardware)

1.5 [OS scheduler operations](https://subscription.packtpub.com/book/programming/9781849688321/1/ch01lvl1sec12/os-scheduler-operations)

1.6 [Designing for concurrency](https://subscription.packtpub.com/book/programming/9781849688321/1/ch01lvl1sec13/designing-for-concurrency)
- Estimating performance improvements
- Amdahl's law
- Gustafson's law

1.7 [Summary](https://subscription.packtpub.com/book/programming/9781849688321/1/ch01lvl1sec14/summary)

-----

### Chapter 2: Looking at Multithreaded Classes – BackgroundWorker

2.1 [Getting started with the BackgroundWorker component](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec15/getting-started-with-the-backgroundworker-component)

2.2 [Simple example without a BackgroundWorker object](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec16/simple-example-without-a-backgroundworker-object)
- How to do it
- How does it work?

2.3 [WPF example with an asynchronous BackgroundWorker](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec18/wpf-example-with-an-asynchronous-backgroundworker)
- How to do it
- How does it work?
- How does it work without blocking the UI?
- How to do it
- How does it work?

2.4 [WPF example with an synchronous BackgroundWorker](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec19/wpf-example-with-a-synchronous-backgroundworker)

2.5 [Showing progress](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec20/showing-progress)
- How to do it
- How does it work?

2.6 [Canceling a BackgroundWorker thread](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec21/canceling-a-backgroundworker-thread)
- How to do it
- How does it work?

2.7 [Working with multiple BackgroundWorker components](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec22/working-with-multiple-backgroundworker-components)
- How does it work?
- How does it work?

2.8 [Exploring other examples](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec23/exploring-other-examples)

2.9 [Summary](https://subscription.packtpub.com/book/programming/9781849688321/2/ch02lvl1sec24/summary)

-----

### Chapter 3: Thread Class – Heavyweight Concurrency in C#

3.1 [Creating threads with the Thread class](https://subscription.packtpub.com/book/programming/9781849688321/3/ch03lvl1sec25/creating-threads-with-the-thread-class)
- Let's get started with an encryption program
- How to do it
- How it works

3.2 [Creating an application with threads](https://subscription.packtpub.com/book/programming/9781849688321/3/ch03lvl1sec26/creating-an-application-with-threads)
- How to do it
- How it works

3.3 [Sharing data between threads](https://subscription.packtpub.com/book/programming/9781849688321/3/ch03lvl1sec27/sharing-data-between-threads)
- How to do it
- How it works

3.4 [Passing parameters to threads](https://subscription.packtpub.com/book/programming/9781849688321/3/ch03lvl1sec28/passing-parameters-to-threads)
- How to do it
- How it works
- Have a go hero – concurrent UI feedback

3.5 [Summary](https://subscription.packtpub.com/book/programming/9781849688321/3/ch03lvl1sec29/summary)

-----

### Chapter 4: Advanced Thread Processing

4.1 [Pipelining](https://subscription.packtpub.com/book/programming/9781849688321/4/ch04lvl1sec30/pipelining)
- Explaining pipelining using an image processing application
- How to do it
- How it works
- Understanding the pixels' color compositions

4.2 [Pausing and restarting threads](https://subscription.packtpub.com/book/programming/9781849688321/4/ch04lvl1sec31/pausing-and-restarting-threads)
- How to do it
- How it works

4.3 [Signals between threads](https://subscription.packtpub.com/book/programming/9781849688321/4/ch04lvl1sec32/signals-between-threads)
- How to do it
- How it works
- Using the AutoResetEvent class to handle signals between threads
- Using the WaitHandle class to check  for signals

4.4 [Joining threads](https://subscription.packtpub.com/book/programming/9781849688321/4/ch04lvl1sec33/joining-threads)
- How to do it
- How it works

4.5 [Locking resources to ensure thread-safe data](https://subscription.packtpub.com/book/programming/9781849688321/4/ch04lvl1sec34/locking-resources-to-ensure-thread-safe-data)
- How to do it
- How it works

4.6 [Error handling with threads](https://subscription.packtpub.com/book/programming/9781849688321/4/ch04lvl1sec35/error-handling-with-threads)
- How to do it
- How it works

4.7 [Summary](https://subscription.packtpub.com/book/programming/9781849688321/4/ch04lvl1sec36/summary)

-----

### Chapter 5: Lightweight Concurrency – Task Parallel Library (TPL)

5.1 [Task Parallel Library](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec38/task-parallel-library)

5.2 [Exploring tasks](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec39/exploring-tasks)
- How to do it
- How it works

5.3 [Tasks with return values](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec40/tasks-with-return-values)
- How to do it
- How it works

5.4 [Concurrent collections](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec41/concurrent-collections)
- How to do it
- How it works

5.5 [Exploring the TaskFactory class](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec42/exploring-the-taskfactory-class)
- How to do it
- How it works

5.6 [Task schedulers](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec43/task-schedulers)

5.7 [Introducing the Parallel class](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec44/introducing-the-parallel-class)
- How to do it
- How it works

5.8 [Delegates and lambda expressions](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec45/delegates-and-lambda-expressions)

5.9 [Summary](https://subscription.packtpub.com/book/programming/9781849688321/5/ch05lvl1sec46/summary)

-----

### Chapter 6: Task-based Parallelism

6.1 [Waiting for a task to complete](https://subscription.packtpub.com/book/programming/9781849688321/6/ch06lvl1sec47/waiting-for-a-task-to-complete)
- How to do it
- How it works

6.2 [Waiting for multiple tasks to complete](https://subscription.packtpub.com/book/programming/9781849688321/6/ch06lvl1sec48/waiting-for-multiple-tasks-to-complete)
- How to do it
- How it works

6.3 [Canceling a task](https://subscription.packtpub.com/book/programming/9781849688321/6/ch06lvl1sec49/canceling-a-task)
- How to do it
- How it works

6.4 [Task exception handling](https://subscription.packtpub.com/book/programming/9781849688321/6/ch06lvl1sec50/task-exception-handling)

6.5 [Summary](https://subscription.packtpub.com/book/programming/9781849688321/6/ch06lvl1sec51/summary)

-----

### Chapter 7: Data Parallelism

7.1 [Parallel loop processing](https://subscription.packtpub.com/book/programming/9781849688321/7/ch07lvl1sec53/parallel-loop-processing)
- How to do it
- How it works

7.2 [Data parallelism on collections using Parallel.ForEach](https://subscription.packtpub.com/book/programming/9781849688321/7/ch07lvl1sec54/data-parallelism-on-collections-using-parallel.foreach)
- How to do it
- How it works

7.3 [Canceling a parallel loop](https://subscription.packtpub.com/book/programming/9781849688321/7/ch07lvl1sec55/canceling-a-parallel-loop)
- How to do it
- How it works

7.4 [Handling exceptions in parallel loops](https://subscription.packtpub.com/book/programming/9781849688321/7/ch07lvl1sec56/handling-exceptions-in-parallel-loops)
- How to do it
- How it works

7.5 [Using thread-local variables in parallel loops](https://subscription.packtpub.com/book/programming/9781849688321/7/ch07lvl1sec57/using-thread-local-variables-in-parallel-loops)
- How to do it
- How it works

7.6 [Summary](https://subscription.packtpub.com/book/programming/9781849688321/7/ch07lvl1sec58/summary)

-----

### Chapter 8: Debugging Multithreaded Applications with Visual Studio

8.1 Considerations for debugging multithreaded applications

8.2 Using the Threads window

8.3 Using the Tasks window

8.4 Using the Parallel Stacks window

8.5 Using the Parallel Watch window

8.6 Debugging an entire application
- How to do it
- How it works

8.7 Summary

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

[https://www.packtpub.com/application-development/c-multithreaded-and-parallel-programming](https://www.packtpub.com/application-development/c-multithreaded-and-parallel-programming)  
[https://www.amazon.com/Multithreaded-Parallel-Programming-Rodney-Ringler-ebook/dp/B00RP13BKS/](https://www.amazon.com/Multithreaded-Parallel-Programming-Rodney-Ringler-ebook/dp/B00RP13BKS/)