---
layout: post
title: Concurrency in C# Cookbook - Asynchronous, Parallel, and Multithreaded Programming
subtitle: If you’re one of many developers still uncertain about concurrent and multithreaded development, this practical cookbook will change your mind. With more than 85 code-rich recipes in this updated second edition, author Stephen Cleary demonstrates parallel processing and asynchronous programming techniques using libraries and language features in .NET and C# 8.0.
---

![placeholder](http://boxxv.com/img/multithread/lrg.jpg "Concurrency in C# Cookbook: Asynchronous, Parallel, and Multithreaded Programming")

✅ Publisher: [O'Reilly Media](https://www.oreilly.com/library/view/concurrency-in-c/9781492054498/)

✅ Year: August 20, 2019

✅ Authors: Stephen Cleary

✅ Language: English

✅ Pages: 254

✅ Size: 2.38 MB


-----

Concurrency is now more common in responsive and scalable application development, but it’s still extremely difficult to code. The detailed solutions in this cookbook show you how modern tools raise the level of abstraction, making concurrency much easier than before. Complete with ready-to-use code and discussions about how and why solutions work, these recipes help you:
- Get up to speed on concurrency and async and parallel programming
- Use async and await for asynchronous operations
- Enhance your code with asynchronous streams
- Explore parallel programming with .NET’s Task Parallel Library
- Create dataflow pipelines with .NET’s TPL Dataflow library
- Understand the capabilities that System.Reactive builds on top of LINQ
- Utilize threadsafe and immutable collections
- Learn how to conduct unit testing with concurrent code
- Make the thread pool work for you
- Enable clean, cooperative cancellation
- Examine scenarios for combining concurrent approaches
- Dive into asynchronous-friendly object-oriented programming
- Recognize and write adapters for code using older asynchronous styles


-----

## Table of contents


### Preface
- Who Should Read This Book
- Why I Wrote This Book
- Navigating This Book
- Online Resources
- Conventions Used in This Book
- Safari® Books Online
- How to Contact Us
- Acknowledgments

-----

### Chapter 1. Concurrency: An Overview

1.1. Introduction to Concurrency

1.2. Introduction to Asynchronous Programming

1.3. Introduction to Parallel Programming

1.4. Introduction to Reactive Programming (Rx)

1.5. Introduction to Dataflows

1.6. Introduction to Multithreaded Programming

1.7. Collections for Concurrent Applications

1.8. Modern Design

1.9. Summary of Key Technologies

-----

### Chapter 2. Async Basics

2.1. Pausing for a Period of Time
- Problem, Solution, Discussion, See Also

2.2. Returning Completed Tasks
- Problem, Solution, Discussion, See Also

2.3. Reporting Progress
- Problem, Solution, Discussion, See Also

2.4. Waiting for a Set of Tasks to Complete
- Problem, Solution, Discussion, See Also

2.5. Waiting for Any Task to Complete
- Problem, Solution, Discussion, See Also

2.6. Processing Tasks as They Complete
- Problem, Solution, Discussion, See Also

2.7. Avoiding Context for Continuations
- Problem, Solution, Discussion, See Also

2.8. Handling Exceptions from async Task Methods
- Problem, Solution, Discussion, See Also

2.9. Handling Exceptions from async void Methods
- Problem, Solution, Discussion, See Also

2.10. Creating a ValueTask

2.11. Consuming a ValueTask 


-----

### Chapter 3: Asynchronous Streams

- Asynchronous Streams and Task<T>
- Asynchronous Streams and IEnumerable<T>
- Asynchronous Streams and Task<IEnumerable<T>>
- Asynchronous Streams and IObservable<T>
- Summary

3.1. Creating Asynchronous Streams

3.2. Consuming Asynchronous Streams

3.3. Using LINQ with Asynchronous Streams

3.4. Asynchronous Streams and Cancellation


-----

### Chapter 4: Parallel Basics

4.1. Parallel Processing of Data
- Problem, Solution, Discussion, See Also

4.2. Parallel Aggregation
- Problem, Solution, Discussion, See Also

4.3. Parallel Invocation
- Problem, Solution, Discussion, See Also

4.4. Dynamic Parallelism
- Problem, Solution, Discussion, See Also

4.5. Parallel LINQ
- Problem, Solution, Discussion, See Also


-----

### Chapter 5: Dataflow Basics

5.1. Linking Blocks
5.2. Propagating Errors
5.3. Unlinking Blocks
5.4. Throttling Blocks
5.5. Parallel Processing with Dataflow Blocks
5.6. Creating Custom Blocks


-----

### Chapter 6: System.Reactive Basics

6.1. Converting .NET Events
6.2. Sending Notifications to a Context
6.3. Grouping Event Data with Windows and Buffers
6.4. Taming Event Streams with Throttling and Sampling
6.5. Timeouts


-----

### Chapter 7: Testing

7.1. Unit Testing async Methods
7.2. Unit Testing async Methods Expected to Fail
7.3. Unit Testing async void Methods
7.4. Unit Testing Dataflow Meshes
7.5. Unit Testing System.Reactive Observables
7.6. Unit Testing System.Reactive Observables with Faked Scheduling

-----

### Chapter 8: Interop

8.1. Async Wrappers for “Async” Methods with “Completed” Events
8.2. Async Wrappers for “Begin/End” Methods
8.3. Async Wrappers for Anything
8.4. Async Wrappers for Parallel Code
8.5. Async Wrappers for System.Reactive Observables
8.6. System.Reactive Observable Wrappers for async Code
8.7. Asynchronous Streams and Dataflow Meshes
8.8. System.Reactive Observables and Dataflow Meshes
8.9. Converting System.Reactive Observables to Asynchronous Streams


-----

### Chapter 9: Collections

9.1. Immutable Stacks and Queues
9.2. Immutable Lists
9.3. Immutable Sets
9.4. Immutable Dictionaries
9.5. Threadsafe Dictionaries
9.6. Blocking Queues
9.7. Blocking Stacks and Bags
9.8. Asynchronous Queues
9.9. Throttling Queues
9.10. Sampling Queues
9.11. Asynchronous Stacks and Bags
9.12. Blocking/Asynchronous Queues


-----

### Chapter 10: Cancellation

10.1. Issuing Cancellation Requests
10.2. Responding to Cancellation Requests by Polling
10.3. Canceling Due to Timeouts
10.4. Canceling async Code
10.5. Canceling Parallel Code
10.6. Canceling System.Reactive Code
10.7. Canceling Dataflow Meshes
10.8. Injecting Cancellation Requests
10.9. Interop with Other Cancellation Systems


-----

### Chapter 11: Functional-Friendly OOP

11.1. Async Interfaces and Inheritance
11.2. Async Construction: Factories
11.3. Async Construction: The Asynchronous Initialization Pattern
11.4. Async Properties
11.5. Async Events
11.6. Async Disposal

-----

### Chapter 12: Synchronization

12.1. Blocking Locks
12.2. Async Locks
12.3. Blocking Signals
12.4. Async Signals
12.5. Throttling



-----

### Chapter 13: Scheduling

13.1. Scheduling Work to the Thread Pool
13.2. Executing Code with a Task Scheduler
13.3. Scheduling Parallel Code
13.4. Dataflow Synchronization Using Schedulers


-----

### Chapter 14: Scenarios

14.1. Initializing Shared Resources
14.2. System.Reactive Deferred Evaluation
14.3. Asynchronous Data Binding
14.4. Implicit State
14.5. Identical Synchronous and Asynchronous Code
14.6. Railway Programming with Dataflow Meshes
14.7. Throttling Progress Updates

-----

### Legacy Platform Support

- Legacy Platform Support for Async
- Legacy Platform Support for Dataflow
- Legacy Platform Support for System.Reactive


-----

### Recognizing and Interpreting Asynchronous Patterns

- Task-Based Asynchronous Pattern (TAP)
- Asynchronous Programming Model (APM)
- Event-Based Asynchronous Programming (EAP)
- Continuation Passing Style (CPS)
- Custom Async Patterns
- ISynchronizeInvoke


-----

[https://www.oreilly.com/library/view/concurrency-in-c/9781492054498/](https://www.oreilly.com/library/view/concurrency-in-c/9781492054498/)  
[https://www.amazon.com/Concurrency-Cookbook-Asynchronous-Multithreaded-Programming-ebook/dp/B07WRN3SSK/](https://www.amazon.com/Concurrency-Cookbook-Asynchronous-Multithreaded-Programming-ebook/dp/B07WRN3SSK/)