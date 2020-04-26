---
layout: post
title: Pro Asynchronous Programming with .NET
subtitle: Asynchronous programming is an essential skill for the modern .NET developer. Pro Asynchronous Programming with .NET is your guide to using this important programming model to build responsive and scalable applications anywhere on the .NET platform.
---

✅ Publisher: [Apress](http://www.apress.com/9781430259206)

✅ Year: December 23, 2013

✅ Authors: Blewett, Richard, Clymer, Andrew, Ltd, Rock Solid Knowledge 

✅ Language: English

✅ Pages: 368

✅ Size: 7.13 MB

✅ Download source code: [pro-asynchronous-programming-w-.net](https://github.com/apress/pro-asynchronous-programming-w-.net)

-----

## Mục lục


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

### 9. Multimedia

9.1 Playing a YouTube Video

9.2 Capturing Video Using MediaRecorder

9.3 Using Android’s Face Detection Capability

9.4 Playing Audio from a File

9.5 Playing Audio Without Interaction

9.6 Using Speech to Text

9.7 Making the Device Speak with Text-to-Speech


### 10. Data Persistence

10.1 Reading and Writing Files in Internal and External Storage

10.2 Getting File and Directory Information

10.3 Reading a File Shipped with the App Rather than in the Filesystem

10.4 Getting Space Information About the SD Card

10.5 Providing a Preference Activity

10.6 Checking the Consistency of Default Shared Preferences

10.7 Using a SQLite Database in an Android Application

10.8 Performing Advanced Text Searches on a SQLite Database

10.9 Working with Dates in SQLite

10.10 Exposing Non-SQL Data as a SQL Cursor

10.11 Displaying Data with a CursorLoader

10.12 Parsing JSON Using JSONObject

10.13 Parsing an XML Document Using the DOM API

10.14 Storing and Retrieving Data via a Content Provider

10.15 Writing a Content Provider

10.16 Adding a Contact Through the Contacts Content Provider

10.17 Reading Contact Data Using a Content Provider

10.18 Implementing Drag and Drop

10.19 Sharing Files via a FileProvider

10.20 Backing Up Your SQLite Data to the Cloud with a SyncAdapter

10.21 Storing Data in the Cloud with Google Firebase


### 11. Telephone Applications

11.1 Doing Something When the Phone Rings

11.2 Processing Outgoing Phone Calls

11.3 Dialing the Phone

11.4 Sending Single-part or Multipart SMS Messages

11.5 Receiving an SMS Message

11.6 Using Emulator Controls to Send SMS Messages to the Emulator

11.7 Using Android’s TelephonyManager to Obtain Device Information


### 12. Networked Applications

12.1 Consuming a RESTful Web Service Using a URLConnection

12.2 Consuming a RESTful Web Service with Volley

12.3 Notifying Your App with Google Cloud Messaging “Push Messaging”

12.4 Extracting Information from Unstructured Text Using Regular Expressions

12.5 Parsing RSS/Atom Feeds Using ROME

12.6 Using MD5 to Digest Clear Text

12.7 Converting Text into Hyperlinks

12.8 Accessing a Web Page Using a WebView

12.9 Customizing a WebView

12.10 Writing an Inter-Process Communication Service


### 13. Gaming and Animation

13.1 Building an Android Game Using flixel-gdx

13.2 Building an Android Game Using AndEngine

13.3 Processing Timed Keyboard Input


### 14. Social Networking

14.1 Authenticating Users with OAUTH2

14.2 Integrating Social Networking Using HTTP

14.3 Loading a User’s Twitter Timeline Using HTML or JSON


### 15. Location and Map Applications

15.1 Getting Location Information

15.2 Accessing GPS Information in Your Application

15.3 Mocking GPS Coordinates on a Device

15.4 Using Geocoding and Reverse Geocoding

15.5 Getting Ready for Google Maps API V2 Development

15.6 Using the Google Maps API V2

15.7 Displaying Map Data Using OpenStreetMap

15.8 Creating Overlays in OpenStreetMap Maps

15.9 Using a Scale on an OpenStreetMap Map

15.10 Handling Touch Events on an OpenStreetMap Overlay

15.11 Getting Location Updates with OpenStreetMap Maps


### 16. Accelerometer

16.1 Checking for the Presence or Absence of a Sensor

16.2 Using the Accelerometer to Detect Shaking

16.3 Checking Whether a Device Is Facing Up or Down

16.4 Reading the Temperature Sensor


### 17. Bluetooth

17.1 Enabling Bluetooth and Making the Device Discoverable

17.2 Connecting to a Bluetooth-Enabled Device

17.3 Accepting Connections from a Bluetooth Device

17.4 Implementing Bluetooth Device Discovery


### 18. System and Device Control

18.1 Accessing Phone Network/Connectivity Information

18.2 Obtaining Information from the Manifest File

18.3 Changing Incoming Call Notification to Silent, Vibrate, or Normal

18.4 Copying Text and Getting Text from the Clipboard

18.5 Using LED-Based Notifications

18.6 Making the Device Vibrate

18.7 Determining Whether a Given Application Is Running


### 19. All the World’s Not Java: Other Programming Languages and Frameworks

19.1 Learning About Cross-Platform Solutions

19.2 Running Shell Commands from Your Application

19.3 Running Native C/C++ Code with JNI on the NDK

19.4 Getting Started with SL4A, the Scripting Layer for Android

19.5 Creating Alerts in SL4A

19.6 Fetching Your Google Documents and Displaying Them in a ListView Using SL4A

19.7 Sharing SL4A Scripts in QR Codes

19.8 Using Native Handset Functionality from a WebView via JavaScript

19.9 Building a Cross-Platform App with Xamarin

19.10 Creating a Cross-Platform App Using PhoneGap/Cordova


### 20. All the World’s Not English: Strings and Internationalization

20.1 Internationalizing Application Text

20.2 Finding and Translating Strings

20.3 Handling the Nuances of strings.xml


### 21. Packaging, Deploying, and Distributing/Selling Your App

21.1 Creating a Signing Certificate and Using It to Sign Your Application

21.2 Distributing Your Application via the Google Play Store

21.3 Distributing Your Application via Other App Stores

21.4 Monetizing Your App with AdMob

21.5 Obfuscating and Optimizing with ProGuard

21.6 Hosting Your App on Your Own Server

21.7 Creating a “Self-Updating” App

21.8 Providing a Link to Other Published Apps in the Google Play Store