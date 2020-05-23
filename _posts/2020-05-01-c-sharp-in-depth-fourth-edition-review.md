---
layout: post
title: C# in Depth (4th edition)
subtitle: C# in Depth is a book for those who are passionate about C#. It aims to be a bridge between the existing introductory books and the language specification, something readable but detailed, exploring every aspect of the language from version 2 onwards.
---

![placeholder](http://boxxv.com/img/multithread/Skeet-4ED-HI.png "C# in Depth")

✅ Publisher: [Manning Publications](https://www.manning.com/books/c-sharp-in-depth-fourth-edition)

✅ Year: August 23, 2019 (Fourth Edition)

✅ Authors:Jon Skeet

✅ Language: English

✅ Pages: 528

✅ Size: 4.78 MB

✅ Download source code:  
[source-4thEdition.zip](https://csharpindepth.com/files/source-4thEdition.zip)  
[source-3rdEdition.zip](https://csharpindepth.com/files/source-3rdEdition.zip)  
[source-2ndEdition.zip](https://csharpindepth.com/files/source-2ndEdition.zip)  
[source-1stEdition.zip](https://csharpindepth.com/files/source-1stEdition.zip)

-----

C# in Depth is a book for those who are passionate about C#. It aims to be a bridge between the existing introductory books and the language specification: something readable but detailed, exploring every aspect of the language from version 2 onwards. In the interests of brevity, it doesn't spend much time on C# 1 - readers are already expected to know the first version at least reasonably. Every new feature from C# 2 onwards is covered, however, as shown in the table of contents below.

One of my hobbies is helping other developers on sites such as Stack Overflow. before Stack Overflow came along, I used to post a lot on the C# newsgroups. I've come to appreciate that whatever technologies you might use on top of C# - MVC, WPF, Windows Forms, etc - if you don't have a firm grasp of the language, you'll find it a lot harder. My hope is that C# in Depth helps readers to really "grok" the language, so they feel they're working in tandem with the compiler rather than fighting against it; making the most of new features instead of constantly being caught out by subtle "gotcha" behaviour. 


-----

# Table of contents


## Part 1. C# in context
Part one provides a brief history of the language.


### Chapter 1. Survival of the sharpest

#### 1.1 An evolving language
- 1.1.1 A helpful type system at large and small scales
- 1.1.2 Ever more concise code
- 1.1.3 Simple data access with LINQ
- 1.1.4 Asynchrony
- 1.1.5 Balancing efficiency and complexity
- 1.1.6 Evolution at speed: Using minor versions

#### 1.2 An evolving platform

#### 1.3 An evolving community

#### 1.4 An evolving book
- 1.4.1 Mixed-level coverage
- 1.4.2 Examples using Noda Time
- 1.4.3 Terminology choices

#### Summary

-----

## Part 2 C# 2-5
Part two describes C# versions 2 through 5. This is effectively a rewritten and condensed form of the third edition of this book.


### Chapter 2. C# 2

#### 2.1 Generics
- 2.1.1 Introduction by example: Collections before generics
- 2.1.2 Generics save the day
- 2.1.3 What can be generic?
- 2.1.4 Type inference for type arguments to methods
- 2.1.5 Type constraints
- 2.1.6 The default and typeof operators
- 2.1.7 Generic type initialization and state

#### 2.2 Nullable value types
- 2.2.1 Aim: Expressing an absence of information
- 2.2.2 CLR and framework support: The Nullable<T> struct
- 2.2.3 Language support

#### 2.3 Simplified delegate creation
- 2.3.1 Method group conversions
- 2.3.2 Anonymous methods
- 2.3.3 Delegate compatibility

#### 2.4 Iterators
- 2.4.1 Introduction to iterators
- 2.4.2 Lazy execution
- 2.4.3 Evaluation of yield statements
- 2.4.4 The importance of being lazy
- 2.4.5 Evaluation of finally blocks
- 2.4.6 The importance of finally handling
- 2.4.7 Implementation sketch

#### 2.5 Minor features
- 2.5.1 Partial types
- 2.5.2 Static classes
- 2.5.3 Separate getter/setter access for properties
- 2.5.4 Namespace aliases
- 2.5.5 Pragma directives
- 2.5.6 Fixed-size buffers
- 2.5.7 InternalsVisibleTo

#### Summary

-----


### Chapter 3. C# 3: LINQ and everything that comes with it

#### 3.1 Automatically implemented properties

#### 3.2 Implicit typing
- 3.2.1 Typing terminology
- 3.2.2 Implicitly typed local variables (var)
- 3.2.3 Implicitly typed arrays

#### 3.3 Object and collection initializers
- 3.3.1 Introduction to object and collection initializers
- 3.3.2 Object initializers
- 3.3.3 Collection initializers
- 3.3.4 The benefits of single expressions for initialization

#### 3.4 Anonymous types
- 3.4.1 Syntax and basic behavior
- 3.4.2 The compiler-generated type
- 3.4.3 Limitations

#### 3.5 Lambda expressions
- 3.5.1 Lambda expression syntax
- 3.5.2 Capturing variables
- 3.5.3 Expression trees

#### 3.6 Extension methods
- 3.6.1 Declaring an extension method
- 3.6.2 Invoking an extension method
- 3.6.3 Chaining method calls

#### 3.7 Query expressions
- 3.7.1 Query expressions translate from C# to C#
- 3.7.2 Range variables and transparent identifiers
- 3.7.3 Deciding when to use which syntax for LINQ

#### 3.8 The end result: LINQ

#### Summary


-----

### Chapter 4. C# 4: Improving interoperability

#### 4.1 Dynamic typing
- 4.1.1 Introduction to dynamic typing
- 4.1.2 Dynamic behavior beyond reflection
- 4.1.3 A brief look behind the scenes
- 4.1.4 Limitations and surprises in dynamic typing
- 4.1.5 Usage suggestions

#### 4.2 Optional parameters and named arguments
- 4.2.1 Parameters with default values and arguments with names
- 4.2.2 Determining the meaning of a method call
- 4.2.3 Impact on versioning

#### 4.3 COM interoperability improvements
- 4.3.1 Linking primary interop assemblies
- 4.3.2 Optional parameters in COM
- 4.3.3 Named indexers

#### 4.4 Generic variance
- 4.4.1 Simple examples of variance in action
- 4.4.2 Syntax for variance in interface and delegate declarations
- 4.4.3 Restrictions on using variance
- 4.4.4 Generic variance in practice

#### Summary


-----

### Chapter 5. Writing asynchronous code

#### 5.1 Introducing asynchronous functions
- 5.1.1 First encounters of the asynchronous kind
- 5.1.2 Breaking down the first example

#### 5.2 Thinking about asynchrony
- 5.2.1 Fundamentals of asynchronous execution
- 5.2.2 Synchronization contexts
- 5.2.3 Modeling asynchronous methods

#### 5.3 Async method declarations
- 5.3.1 Return types from async methods
- 5.3.2 Parameters in async methods

#### 5.4 Await expressions
- 5.4.1 The awaitable pattern
- 5.4.2 Restrictions on await expressions

#### 5.5 Wrapping of return values

#### 5.6 Asynchronous method flow
- 5.6.1 What is awaited and when?
- 5.6.2 Evaluation of await expressions
- 5.6.3 The use of awaitable pattern members
- 5.6.4 Exception unwrapping
- 5.6.5 Method completion

#### 5.7 Asynchronous anonymous functions

#### 5.8 Custom task types in C# 7
- 5.8.1 The 99.9% case: ValueTask<TResult>
- 5.8.2 The 0.1% case: Building your own custom task type

#### 5.9 Async main methods in C# 7.1

#### 5.10 Usage tips
- 5.10.1 Avoid context capture by using ConfigureAwait (where appropriate)
- 5.10.2 Enable parallelism by starting multiple independent tasks
- 5.10.3 Avoid mixing synchronous and asynchronous code
- 5.10.4 Allow cancellation wherever possible
- 5.10.5 Testing asynchrony

#### Summary

-----

### Chapter 6. Async implementation

#### 6.1 Structure of the generated code
- 6.1.1 The stub method: Preparation and taking the first step
- 6.1.2 Structure of the state machine
- 6.1.3 The MoveNext() method (high level)
- 6.1.4 The SetStateMachine method and the state machine boxing dance

#### 6.2 A simple MoveNext() implementation
- 6.2.1 A full concrete example
- 6.2.2 MoveNext() method general structure
- 6.2.3 Zooming into an await expression

#### 6.3 How control flow affects MoveNext()
- 6.3.1 Control flow between await expressions is simple
- 6.3.2 Awaiting within a loop
- 6.3.3 Awaiting within a try/finally block

#### 6.4 Execution contexts and flow

#### 6.5 Custom task types revisited

#### Summary

-----

### Chapter 7. C# 5 bonus features

#### 7.1 Capturing variables in foreach loops

#### 7.2 Caller information attributes
- 7.2.1 Basic behavior
- 7.2.2 Logging
- 7.2.3 Simplifying INotifyPropertyChanged implementations
- 7.2.4 Corner cases of caller information attributes
- 7.2.5 Using caller information attributes with old versions of .NET

#### Summary


-----

## Part 3 C# 6
Part three describes C# 6 in detail.


### Chapter 8. Super-sleek properties and expression-bodied members

#### 8.1 A brief history of properties

#### 8.2 Upgrades to automatically implemented properties
- 8.2.1 Read-only automatically implemented properties
- 8.2.2 Initializing automatically implemented properties
- 8.2.3 Automatically implemented properties in structs

#### 8.3 Expression-bodied members
- 8.3.1 Even simpler read-only computed properties
- 8.3.2 Expression-bodied methods, indexers, and operators
- 8.3.3 Restrictions on expression-bodied members in C# 6
- 8.3.4 Guidelines for using expression-bodied members

#### Summary


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

### Chapter 10. Extension methods

#### 10.1 Life before extension methods

#### 10.2 Extension method syntax
- 10.2.1 Declaring extension methods
- 10.2.2 Calling extension methods
- 10.2.3 Extension method discovery
- 10.2.4 Calling a method on a null reference

#### 10.3 Extension methods in .NET 3.5
- 10.3.1 First steps with Enumerable
- 10.3.2 Filtering with Where and chaining method calls together
- 10.3.3 Interlude: haven’t we seen the Where method before?
- 10.3.4 Projections using the Select method and anonymous types
- 10.3.5 Sorting using the OrderBy method
- 10.3.6 Business examples involving chaining

#### 10.4 Usage ideas and guidelines
- 10.4.1 “Extending the world” and making interfaces richer
- 10.4.2 Fluent interfaces
- 10.4.3 Using extension methods sensibly

#### 10.5 Summary


-----

### Chapter 11. Query expressions and LINQ to Objects

#### 11.1 Introducing LINQ
- 11.1.1 Fundamental concepts in LINQ
- 11.1.2 Defining the sample data model

#### 11.2 Simple beginnings: selecting elements
- 11.2.1 Starting with a source and ending with a selection
- 11.2.2 Compiler translations as the basis of query expressions
- 11.2.3 Range variables and nontrivial projections
- 11.2.3 Range variables and nontrivial projections

#### 11.3 Filtering and ordering a sequence
- 11.3.1 Filtering using a where clause
- 11.3.2 Degenerate query expressions
- 11.3.3 Ordering using an orderby clause

#### 11.4 Let clauses and transparent identifiers
- 11.4.1 Introducing an intermediate computation with let
- 11.4.2 Transparent identifiers

#### 11.5 Joins
- 11.5.1 Inner joins using join clauses
- 11.5.2 Group joins with join...into clauses
- 11.5.3 Cross joins and flattening sequences using multiple from clauses

#### 11.6 Groupings and continuations
- 11.6.1 Grouping with the group...by clause
- 11.6.2 Query continuations

#### 11.7 Choosing between query expressions and dot notation
- 11.7.1 Operations that require dot notation
- 11.7.2 Query expressions where dot notation may be simpler
- 11.7.3 Where query expressions shine

#### 11.8 Summary


-----

### Chapter 12. LINQ beyond collections

#### 12.1 Querying a database with LINQ to SQL
- 12.1.1 Getting started: the database and model
- 12.1.2 Initial queries
- 12.1.3 Queries involving joins

#### 12.2 Translations using IQueryable and IQueryProvider
- 12.2.1 Introducing IQueryable<T> and related interfaces
- 12.2.2 Faking it: interface implementations to log calls
- 12.2.3 Gluing expressions together: the Queryable extension methods
- 12.2.4 The fake query provider in action
- 12.2.5 Wrapping up IQueryable

#### 12.3 LINQ-friendly APIs and LINQ to XML
- 12.3.1 Core types in LINQ to XML
- 12.3.2 Declarative construction
- 12.3.3 Queries on single nodes
- 12.3.4 Flattened query operators
- 12.3.5 Working in harmony with LINQ

#### 12.4 Replacing LINQ to Objects with Parallel LINQ
- 12.4.1 Plotting the Mandelbrot set with a single thread
- 12.4.2 Introducing ParallelEnumerable, ParallelQuery, and AsParallel
- 12.4.3 Tweaking parallel queries

#### 12.5 Inverting the query model with LINQ to Rx
- 12.5.1 IObservable<T> and IObserver<T>
- 12.5.2 Starting simply (again)
- 12.5.3 Querying observables
- 12.5.4 What’s the point?

#### 12.6 Extending LINQ to Objects
- 12.6.1 Design and implementation guidelines
- 12.6.2 Sample extension: selecting a random element

#### 12.7 Summary

-----

## Part 4. C# 4: Playing nicely with others

### Chapter 13. Minor changes to simplify code

#### 13.1 Optional parameters and named arguments
- 13.1.1 Optional parameters
- 13.1.2 Named arguments
- 13.1.3 Putting the two together

#### 13.2 Improvements for COM interoperability
- 13.2.1 The horrors of automating Word before C# 4
- 13.2.2 The revenge of optional parameters and named arguments
- 13.2.3 When is a ref parameter not a ref parameter?
- 13.2.4 Calling named indexers
- 13.2.5 Linking primary interop assemblies

#### 13.3 Generic variance for interfaces and delegates
- 13.3.1 Types of variance: covariance and contravariance
- 13.3.2 Using variance in interfaces
- 13.3.3 Using variance in delegates
- 13.3.4 Complex situations
- 13.3.5 Restrictions and notes

#### 13.4 Teeny tiny changes to locking and field-like events
- 13.4.1 Robust locking
- 13.4.2 Changes to field-like events

#### 13.5 Summary

-----

### Chapter 14. Dynamic binding in a static language

#### 14.1 What? When? Why? How?
- 14.1.1 What is dynamic typing?
- 14.1.2 When is dynamic typing useful, and why?
- 14.1.3 How does C# 4 provide dynamic typing?

#### 14.2 The five-minute guide to dynamic

#### 14.3 Examples of dynamic typing
- 14.3.1 COM in general, and Microsoft Office in particular
- 14.3.2 Dynamic languages such as IronPython
- 14.3.3 Dynamic typing in purely managed code

#### 14.4 Looking behind the scenes
- 14.4.1 Introducing the Dynamic Language Runtime
- 14.4.2 DLR core concepts
- 14.4.3 How the C# compiler handles dynamic
- 14.4.4 The C# compiler gets even smarter
- 14.4.5 Restrictions on dynamic code

#### 14.5 Implementing dynamic behavior
- 14.5.1 Using ExpandoObject
- 14.5.2 Using DynamicObject
- 14.5.3 Implementing IDynamicMetaObjectProvider

#### 14.6 Summary


-----

## Part 5. C# 5: Asynchrony made simple

### Chapter 15. Asynchrony with async/await

#### 15.1 Introducing asynchronous functions
- 15.1.1 First encounters of the asynchronous kind
- 15.1.2 Breaking down the first example

#### 15.2 Thinking about asynchrony
- 15.2.1 Fundamentals of asynchronous execution
- 15.2.2 Modeling asynchronous methods

#### 15.3 Syntax and semantics
- 15.3.1 Declaring an async method
- 15.3.2 Return types from async methods
- 15.3.3 The awaitable pattern
- 15.3.4 The flow of await expressions
- 15.3.5 Returning from an async method
- 15.3.6 Exceptions

#### 15.4 Asynchronous anonymous functions

#### 15.5 Implementation details: compiler transformation
- 15.5.1 Overview of the generated code
- 15.5.2 Structure of the skeleton method
- 15.5.3 Structure of the state machine
- 15.5.4 One entry point to rule them all
- 15.5.5 Control around await expressions
- 15.5.6 Keeping track of a stack
- 15.5.7 Finding out more

#### 15.6 Using async/await effectively
- 15.6.1 The task-based asynchronous pattern
- 15.6.2 Composing async operations
- 15.6.3 Unit testing asynchronous code
- 15.6.4 The awaitable pattern redux
- 15.6.5 Asynchronous operations in WinRT

#### 15.7 Summary

-----

### Chapter 16. C# 5 bonus features and closing thoughts

#### 16.1 Changes to captured variables in foreach loops

#### 16.2 Caller information attributes
- 16.2.1 Basic behavior
- 16.2.2 Logging
- 16.2.3 Implementing INotifyPropertyChanged
- 16.2.4 Using caller information attributes without .NET 4.5

#### 16.3 Closing thoughts


-----

[C# in Depth](https://www.amazon.com/C-in-Depth-Jon-Skeet-audiobook/dp/B07WTR5LHN/)  
[https://csharpindepth.com](https://csharpindepth.com)
[C# in Depth, Fourth Edition](https://www.manning.com/books/c-sharp-in-depth-fourth-edition)