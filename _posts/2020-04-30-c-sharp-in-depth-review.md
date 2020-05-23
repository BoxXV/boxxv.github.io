---
layout: post
title: C# in Depth
subtitle: C# in Depth is a book for those who are passionate about C#. It aims to be a bridge between the existing introductory books and the language specification, something readable but detailed, exploring every aspect of the language from version 2 onwards.
---

![placeholder](http://boxxv.com/img/multithread/41prHleW6NL._SX397_BO1,204,203,200_.jpg "C# in Depth")

✅ Publisher: [Manning Publications](https://www.manning.com/books/c-sharp-in-depth-fourth-edition)

✅ Year: October 8, 2013 - March 2019 (Fourth Edition)

✅ Authors:  Jon Skeet

✅ Language: English

✅ Pages: 616

✅ Size: 14.3 MB


-----

C# in Depth is a book for those who are passionate about C#. It aims to be a bridge between the existing introductory books and the language specification: something readable but detailed, exploring every aspect of the language from version 2 onwards. In the interests of brevity, it doesn't spend much time on C# 1 - readers are already expected to know the first version at least reasonably. Every new feature from C# 2 onwards is covered, however, as shown in the table of contents below.

One of my hobbies is helping other developers on sites such as Stack Overflow. before Stack Overflow came along, I used to post a lot on the C# newsgroups. I've come to appreciate that whatever technologies you might use on top of C# - MVC, WPF, Windows Forms, etc - if you don't have a firm grasp of the language, you'll find it a lot harder. My hope is that C# in Depth helps readers to really "grok" the language, so they feel they're working in tandem with the compiler rather than fighting against it; making the most of new features instead of constantly being caught out by subtle "gotcha" behaviour. 


-----

# Table of contents


## Part 1. Preparing for the journey

### Chapter 1. The changing face of C# development

#### 1.1 Starting with a simple data type
- 1.1.1 The Product type in C# 1
- 1.1.2 Strongly typed collections in C# 2
- 1.1.3 Automatically implemented properties in C# 3
- 1.1.4 Named arguments in C# 4

#### 1.2 Sorting and filtering
- 1.2.1 Sorting products by name
- 1.2.2 Querying collections

#### 1.3 Handling an absence of data
- 1.3.1 Representing an unknown price
- 1.3.2 Optional parameters and default values

#### 1.4 Introducing LINQ
- 1.4.1 Query expressions and in-process queries
- 1.4.2 Querying XML
- 1.4.3 LINQ to SQL

#### 1.5 COM and dynamic typing
- 1.5.1 Simplifying COM interoperability
- 1.5.2 Interoperating with a dynamic language

#### 1.6 Writing asynchronous code without the heartache

#### 1.7 Dissecting the .NET platform
- 1.7.1 C#, the language
- 1.7.2 Runtime
- 1.7.3 Framework libraries

#### 1.8 Making your code super awesome
- 1.8.1 Presenting full programs as snippets
- 1.8.2 Didactic code isn’t production code
- 1.8.3 Your new best friend: the language specification

#### 1.9 Summary

-----

### Chapter 2. Core foundations: building on C# 1

#### 2.1 Delegates
- 2.1.1 A recipe for simple delegates
- 2.1.2 Combining and removing delegates
- 2.1.3 A brief diversion into events
- 2.1.4 Summary of delegates

#### 2.2 Type system characteristics
- 2.2.1 C#’s place in the world of type systems
- 2.2.2 When is C# 1’s type system not rich enough?
- 2.2.3 Summary of type system characteristics

#### 2.3 Value types and reference types
- 2.3.1 Values and references in the real world
- 2.3.2 Value and reference type fundamentals
- 2.3.3 Dispelling myths
- 2.3.4 Boxing and unboxing
- 2.3.5 Summary of value types and reference types

#### 2.4 Beyond C# 1: new features on a solid base
- 2.4.1 Features related to delegates
- 2.4.2 Features related to the type system
- 2.4.3 Features related to value types

#### 2.5 Summary

-----

## Part 2. C# 2: Solving the issues of C# 1

### Chapter 3. Parameterized typing with generics

#### 3.1 Why generics are necessary

#### 3.2 Simple generics for everyday use
- 3.2.1 Learning by example: a generic dictionary
- 3.2.2 Generic types and type parameters
- 3.2.3 Generic methods and reading generic declarations

#### 3.3 Beyond the basics
- 3.3.1 Type constraints
- 3.3.2 Type inference for type arguments of generic methods
- 3.3.3 Implementing generics

#### 3.4 Advanced generics
- 3.4.1 Static fields and static constructors
- 3.4.2 How the JIT compiler handles generics
- 3.4.3 Generic iteration
- 3.4.4 Reflection and generics

#### 3.5 Limitations of generics in C# and other languages
- 3.5.1 Lack of generic variance
- 3.5.2 Lack of operator constraints or a “numeric” constraint
- 3.5.3 Lack of generic properties, indexers, and other member types
- 3.5.4 Comparison with C++ templates
- 3.5.5 Comparison with Java generics

#### 3.6 Summary


-----

### Chapter 4.  Saying nothing with nullable types

#### 4.1 What do you do when you just don’t have a value?
- 4.1.1 Why value type variables can’t be null
- 4.1.2 Patterns for representing null values in C# 1

#### 4.2 System.Nullable<T> and System.Nullable
- 4.2.1 Introducing Nullable<T>
- 4.2.2 Boxing Nullable<T> and unboxing
- 4.2.3 Equality of Nullable<T> instances
- 4.2.4 Support from the nongeneric Nullable class

#### 4.3 C# 2’s syntactic sugar for nullable types
- 4.3.1 The ? modifier
- 4.3.2 Assigning and comparing with null
- 4.3.3 Nullable conversions and operators
- 4.3.4 Nullable logic
- 4.3.5 Using the as operator with nullable types
- 4.3.6 The null coalescing operator

#### 4.4 Novel uses of nullable types
- 4.4.1 Trying an operation without using output parameters
- 4.4.2 Painless comparisons with the null coalescing operator

#### 4.5 Summary


-----

### Chapter 5. Fast-tracked delegates

#### 5.1 Saying goodbye to awkward delegate syntax

#### 5.2 Method group conversions

#### 5.3 Covariance and contravariance
- 5.3.1 Contravariance for delegate parameters
- 5.3.2 Covariance of delegate return types
- 5.3.3 A small risk of incompatibility

#### 5.4 Inline delegate actions with anonymous methods
- 5.4.1 Starting simply: acting on a parameter
- 5.4.2 Returning values from anonymous methods
- 5.4.3 Ignoring delegate parameters

#### 5.5 Capturing variables in anonymous methods
- 5.5.1 Defining closures and different types of variables
- 5.5.2 Examining the behavior of captured variables
- 5.5.3 What’s the point of captured variables?
- 5.5.4 The extended lifetime of captured variables
- 5.5.5 Local variable instantiations
- 5.5.6 Mixtures of shared and distinct variables
- 5.5.7 Captured variable guidelines and summary

#### 5.6 Summary

-----

### Chapter 6. Implementing iterators the easy way

#### 6.1 C# 1: The pain of handwritten iterators

#### 6.2 C# 2: Simple iterators with yield statements
- 6.2.1 Introducing iterator blocks and yield return
- 6.2.2 Visualizing an iterator’s workflow
- 6.2.3 Advanced iterator execution flow
- 6.2.4 Quirks in the implementation

#### 6.3 Real-life iterator examples
- 6.3.1 Iterating over the dates in a timetable
- 6.3.2 Iterating over lines in a file
- 6.3.3 Filtering items lazily using an iterator block and a predicate

#### 6.4 Pseudo-synchronous code with the Concurrency and Coordination Runtime

#### 6.5 Summary

-----

### Chapter 7. Concluding C# 2: the final features

#### 7.1 Partial types
- 7.1.1 Creating a type with multiple files
- 7.1.2 Uses of partial types
- 7.1.3 Partial methods—C# 3 only!

#### 7.2 Static classes

#### 7.3 Separate getter/setter property access

#### 7.4 Namespace aliases
- 7.4.1 Qualifying namespace aliases
- 7.4.2 The global namespace alias
- 7.4.3 Extern aliases

#### 7.5 Pragma directives
- 7.5.1 Warning pragmas
- 7.5.2 Checksum pragmas

#### 7.6 Fixed-size buffers in unsafe code

#### 7.7 Exposing internal members to selected assemblies
- 7.7.1 Friend assemblies in the simple case
- 7.7.2 Why use InternalsVisibleTo?
- 7.7.3 InternalsVisibleTo and signed assemblies

#### 7.8 Summary


-----

## Part 3. C# 3: Revolutionizing data access

### Chapter 8. Cutting fluff with a smart compiler

#### 8.1 Automatically implemented properties

#### 8.2 Implicit typing of local variables
- 8.2.1 Using var to declare a local variable
- 8.2.2 Restrictions on implicit typing
- 8.2.3 Pros and cons of implicit typing
- 8.2.4 Recommendations

#### 8.3 Simplified initialization
- 8.3.1 Defining some sample types
- 8.3.2 Setting simple properties
- 8.3.3 Setting properties on embedded objects
- 8.3.4 Collection initializers
- 8.3.5 Uses of initialization features

#### 8.4 Implicitly typed arrays

#### 8.5 Anonymous types
- 8.5.1 First encounters of the anonymous kind
- 8.5.2 Members of anonymous types
- 8.5.3 Projection initializers
- 8.5.4 What’s the point?

#### 8.6 Summary

-----

### Chapter 9. Lambda expressions and expression trees

#### 9.1 Lambda expressions as delegates
- 9.1.1 Preliminaries: Introducing the Func<…> delegate types
- 9.1.2 First transformation to a lambda expression
- 9.1.3 Using a single expression as the body
- 9.1.4 Implicitly typed parameter lists
- 9.1.5 Shortcut for a single parameter

#### 9.2 Simple examples using List<T> and events
- 9.2.1 Filtering, sorting, and actions on lists
- 9.2.2 Logging in an event handler

#### 9.3 Expression trees
- 9.3.1 Building expression trees programmatically
- 9.3.2 Compiling expression trees into delegates
- 9.3.3 Converting C# lambda expressions to expression trees
- 9.3.4 Expression trees at the heart of LINQ
- 9.3.5 Expression trees beyond LINQ

#### 9.4 Changes to type inference and overload resolution
- 9.4.1 Reasons for change: streamlining generic method calls
- 9.4.2 Inferred return types of anonymous functions
- 9.4.3 Two-phase type inference
- 9.4.4 Picking the right overloaded method
- 9.4.5 Wrapping up type inference and overload resolution

#### 9.5 Summary

-----

### Chapter 9: Collections

9.1. Immutable Stacks and Queues
- Problem, Solution, Discussion, See Also

9.2. Immutable Lists
- Problem, Solution, Discussion, See Also

9.3. Immutable Sets
- Problem, Solution, Discussion, See Also

9.4. Immutable Dictionaries
- Problem, Solution, Discussion, See Also

9.5. Threadsafe Dictionaries
- Problem, Solution, Discussion, See Also

9.6. Blocking Queues
- Problem, Solution, Discussion, See Also

9.7. Blocking Stacks and Bags
- Problem, Solution, Discussion, See Also

9.8. Asynchronous Queues

9.9. Throttling Queues

9.10. Sampling Queues

9.11. Asynchronous Stacks and Bags

9.12. Blocking/Asynchronous Queues
- Problem, Solution, Discussion, See Also


-----

### Chapter 10: Cancellation

10.1. Issuing Cancellation Requests
- Problem, Solution, Discussion, See Also

10.2. Responding to Cancellation Requests by Polling
- Problem, Solution, Discussion, See Also

10.3. Canceling Due to Timeouts
- Problem, Solution, Discussion, See Also

10.4. Canceling async Code
- Problem, Solution, Discussion, See Also

10.5. Canceling Parallel Code
- Problem, Solution, Discussion, See Also

10.6. Canceling System.Reactive Code
- Problem, Solution, Discussion, See Also

10.7. Canceling Dataflow Meshes
- Problem, Solution, Discussion, See Also

10.8. Injecting Cancellation Requests
- Problem, Solution, Discussion, See Also

10.9. Interop with Other Cancellation Systems
- Problem, Solution, Discussion, See Also


-----

### Chapter 11: Functional-Friendly OOP

11.1. Async Interfaces and Inheritance
- Problem, Solution, Discussion, See Also

11.2. Async Construction: Factories
- Problem, Solution, Discussion, See Also

11.3. Async Construction: The Asynchronous Initialization Pattern
- Problem, Solution, Discussion, See Also

11.4. Async Properties
- Problem, Solution, Discussion, See Also

11.5. Async Events
- Problem, Solution, Discussion, See Also

11.6. Async Disposal
- Problem, Solution, Discussion, See Also


-----

### Chapter 12: Synchronization

12.1. Blocking Locks
- Problem, Solution, Discussion, See Also

12.2. Async Locks
- Problem, Solution, Discussion, See Also

12.3. Blocking Signals
- Problem, Solution, Discussion, See Also

12.4. Async Signals
- Problem, Solution, Discussion, See Also

12.5. Throttling
- Problem, Solution, Discussion, See Also


-----

### Chapter 13: Scheduling

13.1. Scheduling Work to the Thread Pool
- Problem, Solution, Discussion, See Also

13.2. Executing Code with a Task Scheduler
- Problem, Solution, Discussion, See Also

13.3. Scheduling Parallel Code
- Problem, Solution, Discussion, See Also

13.4. Dataflow Synchronization Using Schedulers
- Problem, Solution, Discussion, See Also


-----

### Chapter 14: Scenarios

14.1. Initializing Shared Resources
- Problem, Solution, Discussion, See Also

14.2. System.Reactive Deferred Evaluation
- Problem, Solution, Discussion, See Also

14.3. Asynchronous Data Binding
- Problem, Solution, Discussion, See Also

14.4. Implicit State
- Problem, Solution, Discussion, See Also

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