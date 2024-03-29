---
layout: post
title: C# in Depth (4th edition)
subtitle: C# in Depth is a book for those who are passionate about C#. It aims to be a bridge between the existing introductory books and the language specification, something readable but detailed, exploring every aspect of the language from version 2 onwards.
---

![placeholder](https://boxxv.github.io/img/multithread/Skeet-4ED-HI.png "C# in Depth")

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

### Chapter 9. Stringy features

#### 9.1 A recap on string formatting in .NET
- 9.1.1 Simple string formatting
- 9.1.2 Custom formatting with format strings
- 9.1.3 Localization

#### 9.2 Introducing interpolated string literals
- 9.2.1 Simple interpolation
- 9.2.2 Format strings in interpolated string literals
- 9.2.3 Interpolated verbatim string literals
- 9.2.4 Compiler handling of interpolated string literals (part 1)

#### 9.3 Localization using FormattableString
- 9.3.1 Compiler handling of interpolated string literals (part 2)
- 9.3.2 Formatting a FormattableString in a specific culture
- 9.3.3 Other uses for FormattableString
- 9.3.4 Using FormattableString with older versions of .NET

#### 9.4 Uses, guidelines, and limitations
- 9.4.1 Developers and machines, but maybe not end users
- 9.4.2 Hard limitations of interpolated string literals
- 9.4.3 When you can but really shouldn?t

#### 9.5 Accessing identifiers with nameof
- 9.5.1 First examples of nameof
- 9.5.2 Common uses of nameof
- 9.5.3 Tricks and traps when using nameof

#### Summary


-----

### Chapter 10. A smörgåsbord of features for concise code

#### 10.1 Using static directives
- 10.1.1 Importing static members
- 10.1.2 Extension methods and using static

#### 10.2 Object and collection initializer enhancements
- 10.2.1 Indexers in object initializers
- 10.2.2 Using extension methods in collection initializers
- 10.2.3 Test code vs. production code

#### 10.3 The null conditional operator
- 10.3.1 Simple and safe property dereferencing
- 10.3.2 The null conditional operator in more detail
- 10.3.3 Handling Boolean comparisons
- 10.3.4 Indexers and the null conditional operator
- 10.3.5 Working effectively with the null conditional operator
- 10.3.6 Limitations of the null conditional operator

#### 10.4 Exception filters
- 10.4.1 Syntax and semantics of exception filters
- 10.4.2 Retrying operations
- 10.4.3 Logging as a side effect
- 10.4.4 Individual, case-specific exception filters
- 10.4.5 Why not just throw?

#### Summary


-----

## Part 4. C# 4: Playing nicely with others
Part four addresses C# 7 (all the way up to C# 7.3) and completes the book by peering a short distance into the future.


### Chapter 11. Composition using tuples

#### 11.1 Introduction to tuples

#### 11.2 Tuple literals and tuple types
- 11.2.1 Syntax
- 11.2.2 Inferred element names for tuple literals (C# 7.1)
- 11.2.3 Tuples as bags of variables

#### 11.3 Tuple types and conversions
- 11.3.1 Types of tuple literals
- 11.3.2 Conversions from tuple literals to tuple types
- 11.3.3 Conversions between tuple types
- 11.3.4 Uses of conversions
- 11.3.5 Element name checking in inheritance
- 11.3.6 Equality and inequality operators (C# 7.3)

#### 11.4 Tuples in the CLR
- 11.4.1 Introducing System.ValueTuple<...>
- 11.4.2 Element name handling
- 11.4.3 Tuple conversion implementations
- 11.4.4 String representations of tuples
- 11.4.5 Regular equality and ordering comparisons
- 11.4.6 Structural equality and ordering comparisons
- 11.4.7 Womples and large tuples
- 11.4.8 The nongeneric ValueTuple struct
- 11.4.8 The nongeneric ValueTuple struct

#### 11.5 Alternatives to tuples
- 11.5.1 System.Tuple<...>
- 11.5.2 Anonymous types
- 11.5.3 Named types

#### 11.6 Uses and recommendations
- 11.6.1 Nonpublic APIs and easily changed code
- 11.6.2 Local variables
- 11.6.3 Fields
- 11.6.4 Tuples and dynamic don?t play together nicely

#### Summary


-----

### Chapter 12. Deconstruction and pattern matching

#### 12.1 Deconstruction of tuples
- 12.1.1 Deconstruction to new variables
- 12.1.2 Deconstruction assignments to existing variables and properties
- 12.1.3 Details of tuple literal deconstruction

#### 12.2 Deconstruction of nontuple types
- 12.2.1 Instance deconstruction methods
- 12.2.2 Extension deconstruction methods and overloading
- 12.2.3 Compiler handling of Deconstruct calls

#### 12.3 Introduction to pattern matching

#### 12.4 Patterns available in C# 7.0
- 12.4.1 Constant patterns
- 12.4.2 Type patterns
- 12.4.3 The var pattern

#### 12.5 Using patterns with the is operator

#### 12.6 Using patterns with switch statements
- 12.6.1 Guard clauses
- 12.6.2 Pattern variable scope for case labels
- 12.6.3 Evaluation order of pattern-based switch statements

#### 12.7 Thoughts on usage
- 12.7.1 Spotting deconstruction opportunities
- 12.7.2 Spotting pattern matching opportunities


#### Summary

-----


### Chapter 13. Improving efficiency with more pass by reference

#### 13.1 Recap: What do you know about ref?

#### 13.2 Ref locals and ref returns
- 13.2.1 Ref localsts
- 13.2.2 Ref returns
- 13.2.3 The conditional ?: operator and ref values (C# 7.2)
- 13.2.4 Ref readonly (C# 7.2)

#### 13.3 in parameters (C# 7.2)
- 13.3.1 Compatibility considerations
- 13.3.2 The surprising mutability of in parameters: External changes
- 13.3.3 Overloading with in parameters
- 13.3.4 Guidance for in parameters

#### 13.4 Declaring structs as readonly (C# 7.2)
- 13.4.1 Background: Implicit copying with read-only variables
- 13.4.2 The readonly modifier for structs
- 13.4.3 XML serialization is implicitly read-write

#### 13.5 Extension methods with ref or in parameters (C# 7.2)
- 13.5.1 Using ref/in parameters in extension methods to avoid copying
- 13.5.2 Restrictions on ref and in extension methods

#### 13.6 Ref-like structs (C# 7.2)
- 13.6.1 Rules for ref-like structs
- 13.6.2 Span<T> and stackalloc
- 13.6.3 IL representation of ref-like structs

#### Summary

-----

### Chapter 14. Concise code in C# 7

#### 14.1 Local methods
- 14.1.1 Variable access within local methods
- 14.1.2 Local method implementations
- 14.1.3 Usage guidelines

#### 14.2 Out variables
- 14.2.1 Inline variable declarations for out parameters
- 14.2.2 Restrictions lifted in C# 7.3 for out variables and pattern variables

#### 14.3 Improvements to numeric literals
- 14.3.1 Binary integer literals
- 14.3.2 Underscore separators

#### 14.4 Throw expressions

#### 14.5 Default literals (C# 7.1)

#### 14.6 Nontrailing named arguments (C# 7.2)

#### 14.7 Private protected access (C# 7.2)

#### 14.8 Minor improvements in C# 7.3
- 14.8.1 Generic type constraints
- 14.8.2 Overload resolution improvements
- 14.8.3 Attributes for fields backing automatically implemented properties

#### Summary


-----

### Chapter 15. C# 8 and beyond

#### 15.1 Nullable reference types
- 15.1.1 What problem do nullable reference types solve?
- 15.1.2 Changing the meaning when using reference types
- 15.1.3 Enter nullable reference types
- 15.1.4 Nullable reference types at compile time and execution time
- 15.1.5 The damn it or bang operator
- 15.1.6 Experiences of nullable reference type migration
- 15.1.7 Future improvements

#### 15.2 Switch expressions

#### 15.3 Recursive pattern matching
- 15.3.1 Matching properties in patterns
- 15.3.2 Deconstruction patterns
- 15.3.3 Omitting types from patterns

#### 15.4 Indexes and ranges
- 15.4.1 Index and Range types and literals
- 15.4.2 Applying indexes and ranges

#### 15.5 More async integration
- 15.5.1 Asynchronous resource disposal with using await
- 15.5.2 Asynchronous iteration with foreach await
- 15.5.3 Asynchronous iterators

#### 15.6 Features not yet in preview
- 15.6.1 Default interface methods
- 15.6.2 Record types
- 15.6.3 Even more features in brief

#### 15.7 Getting involved

#### Summary


-----

[C# in Depth](https://www.amazon.com/C-in-Depth-Jon-Skeet-audiobook/dp/B07WTR5LHN/)  
[https://csharpindepth.com](https://csharpindepth.com)  
[C# in Depth, Fourth Edition](https://www.manning.com/books/c-sharp-in-depth-fourth-edition)  
[https://livebook.manning.com/book/c-sharp-in-depth-fourth-edition](https://livebook.manning.com/book/c-sharp-in-depth-fourth-edition/about-this-book/)