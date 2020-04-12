---
layout: post
title: Head First Design Patterns Tiếng Việt
subtitle: Your brain on Design Patterns
---

## Mục lục

✅ Chapter 1: Intro to Design Patterns

✅ Chapter 2: the Observer Pattern

✅ Chapter 3: the Decorator Pattern

✅ Chapter 4: the Factory Pattern

✅ Chapter 5: the Singleton Pattern

✅ Chapter 6: the Command Pattern

✅ Chapter 7: the Adapter and Facade Patterns

✅ Chapter 8: the Template Method Pattern

✅ Chapter 9: the Iterator and Composite Patterns

✅ Chapter 10: the State Pattern

✅ Chapter 11: the Proxy Pattern

✅ Chapter 12: Compound Patterns

✅ Chapter 13: Better Living with Patterns


-----
### Chương 1: Strategy Pattern (Mẫu chiến lược)

**Strategy Pattern – Chào mừng đến với Design Patterns**

Ai đó đã giải quyết những vấn đề của bạn. Trong chương này Strategy Pattern (Mẫu chiến lược), bạn sẽ học được lý do tại sao (và làm thế nào) bạn có thể khai thác kiến thức và kinh nghiệm của những developer khác. Trước khi chúng ta hoàn thành, chúng ta sẽ xem xét việc sử dụng và lợi ích của các mẫu thiết kế, xem xét một số nguyên tắc thiết kế OO chính và xem qua một ví dụ về cách một mẫu hoạt động. Cách tốt nhất để sử dụng các mẫu là suy nghĩ về chúng và sau đó nhận ra nơi nào cần sử dụng trong thiết kế của bạn và các ứng dụng hiện có, nơi bạn có thể áp dụng chúng. Thay vì tự viết code, với các mẫu thiết kế bạn có được kinh nghiệm sử dụng lại code (reuse code).

**Bắt đầu với một ứng dụng SimUDuck đơn giản**

Joe làm việc cho một công ty rất thành công trò chơi mô phỏng vịt, SimUDuck. Trò chơi có thể hiển thị rất nhiều loài vịt bơi và tạo ra âm thanh “quack quack”. Thiết kế ban đầu của hệ thống đã sử dụng các kỹ thuật OO tiêu chuẩn và tạo ra một superclass Duck mà tất cả các loại vịt khác sẽ kế thừa nó.

![tempsnip](http://boxxv.com/img/patterns/tempsnip.png "tempsnip")_tempsnip_


### Layouts

- Introduction
- Defining and inflating a layout
- Using RelativeLayout
- Using LinearLayout
- Creating tables – TableLayout and GridLayout
- RecyclerView replaces ListView
- Changing layout properties during runtime 


### Views, Widgets, and Styles 

- Introduction
- Inserting a widget into a layout
- Using graphics to show button state
- Creating a widget at runtime
- Creating a custom component
- Applying a style to a View
- Turning a style into a theme
- Selecting a theme based on the Android version


### Menus and Action Mode 

- Introduction
- Creating an options menu
- Modifying menus and menu items during runtime
- Enabling Contextual Action Mode for a view
- Using Contextual Batch Mode with RecyclerView
- Creating a pop-up menu 


###  Fragments

- Introduction
- Creating and using a Fragment
- Adding and removing Fragments during runtime
- Passing data between Fragments
- Handling the Fragment back stack 


### Home Screen Widgets, Search, and the System UI

- Introduction
- Creating a shortcut on the Home screen
- Creating a Home screen widget
- Adding Search to the Action Bar
- Showing your app full-screen 


### Data Storage

- Introduction
- Storing simple data
- Read and write a text file to internal storage
- Read and write a text file to external storage
- Including resource files in your project
- Creating and using an SQLite database
- Accessing data in the background using a Loader
- Accessing external storage with scoped directories in Android N 


### Alerts and Notifications

- Introduction
- Lights, Action, and Sound – getting the user's attention!
- Creating a Toast with a custom layout
- Displaying a message box with AlertDialog
- Displaying a progress dialog
- Lights, Action, and Sound Redux using Notifications
- Creating a Media Player Notification
- Making a Flashlight with a Heads-Up Notification
- Notifications with Direct Reply 


### Using the Touchscreen and Sensors 

- Introduction
- Listening for click and long-press events
- Recognizing tap and other common gestures
- Pinch-to-zoom with multi-touch gestures
- Swipe-to-Refresh
- Listing available sensors – an introduction to the Android Sensor Framework
- Reading sensor data – using Android Sensor Framework events
- Reading device orientation 


### Graphics and Animation 

- Introduction
- Scaling down large images to avoid Out of Memory exceptions
- A transition animation – defining scenes and applying a transition
- Creating a Compass using sensor data and RotateAnimation
- Creating a slideshow with ViewPager
- Creating a Card Flip Animation with Fragments
- Creating a Zoom Animation with a Custom Transition
- Displaying animated image (GIF/WebP) with the new ImageDecoder library
- Creating a circle image with the new ImageDecoder 


### A First Look at OpenGL ES

- Introduction
- Setting up the OpenGL ES environment
- Drawing shapes on GLSurfaceView
- Applying the projection and camera view while drawing
- Moving the triangle with rotation
- Rotating the triangle with user input 


### Multimedia

- Introduction
- Playing sound effects with SoundPool
- Playing audio with MediaPlayer
- Responding to hardware media controls in your app
- Taking a photo with the default camera app
- Taking a picture using the Camera2 API 


### Telephony, Networks, and the Web 

- Introduction
- How to make a phone call
- Monitoring phone call events
- How to send SMS (text) messages
- Receiving SMS messages
- Displaying a web page in your application
- Checking online status and connection type
- Phone number blocking API 


### Location and Using Geofencing 

- Introduction
- How to get the device location
- Resolving problems reported with the GoogleApiClient OnConnectionFailedListener
- Creating and monitoring a Geofence 


### Getting Your App Ready for the Play Store 

- Introduction
- The Android 6.0 Runtime Permission Model
- How to schedule an alarm
- Receiving notification of device boot
- Using the AsyncTask for background work
- Adding speech recognition to your app
- How to add Google sign-in to your app 

### Getting Started with Kotlin 

- Introduction
- How to create an Android project with Kotlin
- Creating a Toast in Kotlin
- Runtime permission in Kotlin 