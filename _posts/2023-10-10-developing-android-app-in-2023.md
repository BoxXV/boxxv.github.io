---
layout: post
title: Phát triển ứng dụng Android năm 2023
subtitle: Developing Android App in 2023
description: Các phương pháp hay nhất và đề xuất phổ biến và mới nhất mà mọi nhà phát triển Android nên biết vào năm 2023
author: "Juraj Kušnier"
image: "img/android-bg.jpg"
tags:
- Android
- Kotlin
- Jetpack
- Compose
- Material Design
---

# Mục lục

- [Mục lục](#mục-lục)
- [Java đã chết, Kotlin trường tồn](#java-đã-chết-kotlin-trường-tồn)
- [Jetpack](#jetpack)
	- [Android Jetpack là gì?](#android-jetpack-là-gì)
		- [Ưu điểm của Android Jetpack](#ưu-điểm-của-android-jetpack)
		- [Lợi ích của Android Jetpack](#lợi-ích-của-android-jetpack)
		- [What's new in Jetpack?](#whats-new-in-jetpack)
	- [I. Architecture](#i-architecture)
		- [1. Data Binding](#1-data-binding)
		- [2. Lifecycles](#2-lifecycles)
		- [3. LiveData](#3-livedata)
		- [4. Navigation](#4-navigation)
		- [5. Paging](#5-paging)
		- [6. Room](#6-room)
		- [7. ViewModel](#7-viewmodel)
		- [8. WorkManager](#8-workmanager)
	- [II. Foundation](#ii-foundation)
		- [1. AppCompat](#1-appcompat)
		- [2. Android KTX](#2-android-ktx)
		- [3. Multidex](#3-multidex)
		- [4. Test](#4-test)
	- [III. UI](#iii-ui)
		- [1. Animation and transitions](#1-animation-and-transitions)
		- [2. Auto](#2-auto)
		- [3. Emoji](#3-emoji)
		- [4. Fragment](#4-fragment)
		- [5. Layout](#5-layout)
		- [6. Palette](#6-palette)
		- [7. TV](#7-tv)
		- [8. Wear OS by Google](#8-wear-os-by-google)
	- [IV. Behavior](#iv-behavior)
		- [Download manager](#download-manager)
		- [1. Media and playback](#1-media-and-playback)
		- [2. Notifications](#2-notifications)
		- [3. Permissions](#3-permissions)
		- [4. Sharing](#4-sharing)
		- [5. Slices](#5-slices)
	- [Jetpack Compose](#jetpack-compose)
- [Kotlin Coroutines](#kotlin-coroutines)
- [Asynchronous Flow](#asynchronous-flow)
- [App Architecture](#app-architecture)
- [Material Design](#material-design)
- [User Experience](#user-experience)
- [Example App](#example-app)
- [Free Resources](#free-resources)
- [Tổng kết](#tổng-kết)



![Android](https://boxxv.github.io/img/2023/android-14-h.jpeg "Android")

Trong bài viết ngắn này, tôi tóm tắt một số đề xuất cũng như thực tiễn tốt nhất và phổ biến mới dành cho nhà phát triển ứng dụng Android. Hãy thoải mái sử dụng chúng khi bạn xây dựng một dự án greenfield mới hoặc khi bạn muốn loại bỏ giao diện cũ khỏi các ứng dụng hiện có của mình.

- [Android Roadmap mind map](https://mind42.com/mindmap/95590371-4d95-4f66-91da-a7afc8e1b198)
- [JetPack compose mind map](https://mind42.com/mindmap/78ed0932-fa34-49a6-b0ab-b330b0ac54ab)

# Java đã chết, Kotlin trường tồn

Nếu bạn thực sự không biết thì đã vài năm trôi qua kể từ khi Google [thông báo](https://developer.android.com/kotlin/first) rằng việc phát triển Android sẽ ưu tiên Kotlin lên hàng đầu. Kotlin không chỉ an toàn hơn, được thiết kế tốt hơn và ít dài dòng hơn Java mà không có Kotlin trong cơ sở mã của bạn, bạn sẽ không thể sử dụng các công cụ và thư viện hiện đại như Jetpack Compose hoặc lập trình không đồng bộ bằng Coroutines.

![Kotlin-first](https://boxxv.github.io/img/2023/5b84c1f10041d41f8d50.jpg "Kotlin-first")

- [Kotlin Foundation](https://kotlinfoundation.org)
- [Android's commitment to Kotlin](https://android-developers.googleblog.com/2019/12/androids-commitment-to-kotlin.html)

# Jetpack

## Android Jetpack là gì?

Jetpack là một bộ các thư viện được Google giới thiệu từ tháng 5 năm 2018. Android Jetpack là một tập hợp các components, tools giúp bạn nhanh chóng tạo ra các ứng dụng Android tuyệt vời. Các components này kết hợp giữa Support Library và Architecture Components.

Có thể phân loại Android Jetpack thành 4 thành phần chính:

- Foumdation components (Ví dụ: ktx, appcompat, multidex, test)
- Architecture components (Ví dụ: Data Binding, Lifecycles, ViewModel, Livedata, Room, Paging, Navigation, WorkManager)
- Behavior components (Ví dụ: Download manager, Media, Notifications, Permissions, Sharing, Slices)
- UI components (Ví dụ: Animations, Auto, Emoji, Fragment, Layout, Palette, TV, Wear OS )

![Jetpack](https://boxxv.github.io/img/2023/36.png "Jetpack")

Nên nhớ đây chỉ là mô hình ở lần giới thiệu đầu tiên của Google về Jetpack. Những thư viện được đánh dấu là `new!` là những thứ mới toanh từ ngày ra mắt, số còn lại thì đã có sẵn rồi.

Một năm sau đó, Google bổ sung vào bộ sưu tập Jetpack này một loạt thư viện nữa. Bao gồm CameraX hay các thư viện nâng cấp cho các thư viện trước đây. Và đặc biệt, thời gian này còn có một khái niệm mới ra đời, đó là Jetpack Compose (đây là gì thì mình sẽ có loạt bài viết riêng, mặc dù chúng cũng nằm trong họ Jetpack nhưng kiến thức về chúng là rất nhiều, do đó mình phải tách ra nói riêng thôi).

### Ưu điểm của Android Jetpack

- **1. Tính “mở”**: 
Để hiểu kỹ hơn và trả lời câu hỏi Android Jetpack là gì? thì hãy xem xét: Các Android Jetpack components được cung cấp dưới dạng các thư viện “mở”, không phải là một phần của nền tảng Android cơ bản. Điều này có nghĩa là bạn có thể dễ dàng áp dụng từng component.

Mỗi khi Android Jetpack có thêm một tính năng mới, bạn có thể dễ dàng thêm nó vào trong ứng dụng của mình, triển khai ứng dụng trên Play Store và cung cấp cho người dùng tất cả các tính năng mới chỉ trong một ngày. Các thư viện mở sẽ được chuyển vào androidx.* namespace mới.

- **2. Tính tương thích ngược**: 
Ngoài ra, ứng dụng của bạn có thể chạy mượt mà trên nhiều phiên bản của Android mà không lo lắng về tính tương thích. Tại sao ư?

Vì đơn giản là Android Jetpack được xây dựng dựa trên Support Library. Mà các thư viện này được các nhà phát triển Android  tạo ra để cung cấp các chức năng độc lập với các phiên Android, và có tính tương thích ngược rất tốt.

Ví dụ như: Ứng dụng của bạn sử dụng Fragment mà lại muốn hỗ trợ Android 3.0 trở xuống? Chính là lúc bạn nghĩ tới Support Library đấy.

- **3. Dễ dàng testing**: 
Hơn nữa, Android Jetpack còn có thiết kế rất tốt cho việc testing. Nó tách biệt giữa phần chức năng và phần test. Điều này giúp bạn dễ dàng kiểm tra, nâng cao chất lượng ứng dụng.

- **4. Các component độc lập với nhau**: 
Mặc dù các components của Android Jetpack được xây dựng để hoạt động cùng nhau. Ví dụ: lifecycle awareness và live data.

Tuy nhiên, bạn không phải bắt buộc phải sử dụng tất cả chúng. Bạn có thể tích hợp từng phần của Android Jetpack để giải quyết một vấn đề của bạn. Điều này giúp cho ứng dụng trở nên nhẹ nhàng.

### Lợi ích của Android Jetpack

- **Tăng hiệu suất phát triển**: Android Jetpack giúp giảm thiểu công việc lặp lại và tăng tốc quá trình phát triển. Các thành phần đã được xây dựng sẵn và tuân theo các chuẩn tốt nhất, giúp nhà phát triển tiết kiệm thời gian và tập trung vào việc sáng tạo.

- **Dễ bảo trì và mở rộng**: Với kiến ​​trúc rõ ràng và các thành phần tương tác tốt với nhau, việc bảo trì và mở rộng ứng dụng trở nên dễ dàng hơn, giúp duy trì chất lượng và tính năng của ứng dụng.

- **Hỗ trợ phiên bản Android đa dạng**: Android Jetpack cung cấp các công cụ giúp ứng dụng hoạt động mượt mà trên nhiều phiên bản Android khác nhau, từ các phiên bản cũ hơn đến các phiên bản mới nhất.

- **Tăng trải nghiệm người dùng**: Nhờ vào các thành phần Behavior như Navigation và Paging, Android Jetpack giúp tạo ra trải nghiệm người dùng tốt hơn, dễ dàng điều hướng và tiếp cận nội dung.

### What's new in Jetpack? 

- [What's new in Jetpack?](https://viblo.asia/p/whats-new-in-jetpack-maGK76yL5j2)


## I. [Architecture](https://developer.android.com/topic/architecture)

Các thành phần ở nhóm này sẽ tập trung vào việc làm sao có thể xây dựng một ứng dụng nhanh chóng, dễ dàng kiểm lỗi cũng như dễ bảo trì, sữa chữa sau này. Có thể kể đến các thành phần này bao gồm `Data Binding`, `Lifecycles`, `LiveData`, `Navigation`, `Paging`, `Room`, `ViewModel`, `WorkManager`, ….

### 1. [Data Binding](https://developer.android.com/topic/libraries/data-binding/)


### 2. [Lifecycles](https://developer.android.com/topic/libraries/architecture/lifecycle)

Quản lý vòng đời Activity và fragment

### 3. [LiveData](https://developer.android.com/topic/libraries/architecture/livedata)

Notify views khi dữ liệu bên dưới thay đổi

### 4. [Navigation](https://developer.android.com/topic/libraries/architecture/navigation.html)

Handle tất cả các chức năng liên quan tới Navigation

Trong khi Activity trong Android được cung cấp để bạn dễ dàng tạo và tương tác với người dùng thông qua UI. Nhưng nó lại không linh hoạt trong việc chia sẻ dữ liệu và chuyển đổi giữa các Activity.

Chính vì vậy mà Activity trở thành một cấu trúc kém lý tưởng để xây dựng điều hướng trong ứng dụng.

Vì vậy, Google I/O 18 đã giới thiệu Navigation component dưới dạng một famework. Navigation component giúp cho bạn dễ dàng tạo điều hướng trong ứng dụng.

Với khả năng hỗ trợ Fragment, bạn sẽ nhận được tất cả các lợi ích từ Architecture Components như Lifecycle và ViewModel trong khi Navigation sẽ xử lý sự phức tạp của FragmentTransilities giùm bạn.

Mình có thể liệt kê một số tính năng hay ho của Navigation component như:

- Hỗ trợ hiệu ứng khi bạn điều hướng giữa các màn hình.
- Tự động xây dựng các hành vi Up và Back.
- Hỗ trợ đầy đủ cho các liên kết sâu ([Deep link](https://developer.android.com/training/app-links/deep-linking))
- Cung cấp công cụ để kết nối Navigation vào các tiện ích UI thích hợp. Như navigation drawer và Bottom Navigation

Cuối cùng, trình chỉnh sửa Navigation Editor trong Android Studio 3.2 còn cho phép bạn xem và quản lý các navigation properties của mình một cách rất trực quan.

- [Android Navigation Component](https://www.youtube.com/playlist?list=PLRoAKls-7kksIt8rkahuC6erNcQy45NYk)
- [Migrate Jetpack Navigation to Navigation Compose](https://developer.android.com/jetpack/compose/migrate/migration-scenarios/navigation)

- [Navigation in Jetpack Compose](https://developer.android.com/courses/pathways/android-basics-compose-unit-4-pathway-2)
- [Codelabs - Navigate between screens with Compose](https://developer.android.com/codelabs/basic-android-kotlin-compose-navigation)
- [Effortless Navigation with Compose](https://blog.stackademic.com/effortless-navigation-with-compose-30d37ddf5625)
- [Navigation Basics in Jetpack Compose](https://youtu.be/glyqjzkc4fk)
- [Full Guide to Nested Navigation Graphs in Jetpack Compose](https://youtu.be/FIEnIBq7Ups)
- [Modular Navigation with Jetpack Compose](https://medium.com/google-developer-experts/modular-navigation-with-jetpack-compose-fda9f6b2bef7)
- [Nested Navigation Graph in Jetpack Compose with Bottom Navigation](https://medium.com/@mathroda/nested-navigation-graph-in-jetpack-compose-with-bottom-navigation-d983c2d4119f)

### 5. [Paging](https://developer.android.com/topic/libraries/architecture/paging)

Phân trang theo yêu cầu từ data source

Thông thường, người ta sẽ không tải toàn bộ dữ liệu và hiển thị ra màn hình. Vì điều đó sẽ vừa tốn thời gian lấy dữ liệu, vừa tốn thời gian và tài nguyên để hiển thị. Do vậy, người ta chỉ tải từng phần của dữ liệu. Đây chính là khái niệm paging.

Paging component giúp việc tải dữ liệu trở nên dễ dàng. Đồng thời giúp việc hiển thị các tập dữ liệu lớn với tốc độ cuộn nhanh hơn, không giới hạn với RecyclerView.

Paging component có thể tải dữ liệu phân trang từ bộ nhớ cục bộ, mạng hoặc cả hai. Nó hoạt động hiệu quả hơn hẳn so với Room, LiveData và RxJava.

### 6. [Room](https://developer.android.com/training/data-storage/room)

Hỗ trợ truy cập và điều khiển dễ dàng hơn trong SQLite database

### 7. [ViewModel](https://developer.android.com/topic/libraries/architecture/viewmodel)

Quản lý dữ liệu liên quan đến giao diện người dùng theo vòng đời

### 8. [WorkManager](https://developer.android.com/topic/libraries/architecture/workmanager)

Quản lý các công việc trong Android background

WorkMananager component là một thư viện cung cấp giải pháp giúp cho các tác vụ chạy nền( background task) được hiệu quả hơn.

Đưa một nhiệm vụ cho WorkManager và để cho nó chọn một cách thích hợp để chạy nó trong nền tùy theo điều kiện. Nó thay thế những thứ như jobs hoặc SyncAdapters.

WorkManager cung cấp một API có khả năng làm việc trên các thiết bị có hoặc không có Google Play Services.

Ngoài ra, WorkManager còn có khả năng tạo biểu đồ công việc và truy vấn trạng thái công việc của bạn.


## II. Foundation

Foundation components cung cấp core system capabilities, các extensions của Kotlin cùng với việc hỗ trợ multidex và automated testing.

Các thành phần ở nhóm này được gọi là các thành phần nền tảng. Cũng như tên gọi, chúng sẽ là các thư viện giúp tác động đến nền tảng của Android, như thư viện tương thích ngược, các thư viện hỗ trợ Kotlin cũng như hỗ trợ cho việc testing. Chúng bao gồm `App Compat`, `Android KTX`, `Multidex`, `Test`, ….

### 1. [AppCompat](https://developer.android.com/topic/libraries/support-library/packages.html#v7-appcompat)

Tương thích ngược với các phiên bản cũ của android

### 2. [Android KTX](https://developer.android.com/kotlin/ktx.html)

Viết code Kotlin ngắn gọn, dễ hiểu hơn

Android KTX cho phép bạn chuyển đổi mã Kotlin từ như thế này:

```java
view.viewTreeObserver.addOnPreDrawListener(
  object : ViewTreeObserver.OnPreDrawListener {
    override fun onPreDraw(): Boolean {
      viewTreeObserver.removeOnPreDrawListener(this)
      actionToBeTriggered()
      return true
    }
});
```

thành mã ngắn gọn hơn rất nhiều:

```kotlin
view.doOnPreDraw { actionToBeTriggered() }
```

### 3. [Multidex](https://developer.android.com/build/multidex)

Cung cấp khả năng hỗ trợ cho apps apps với multiple DEX files

### 4. [Test](https://developer.android.com/training/testing)

Framwork cho Android testing bao gồm unit và runtime UI tests


## III. UI

Nó giúp chúng ta xây dựng nên ứng dụng với giao diện đẹp hơn, chuyên nghiệp hơn và sáng sủa hơn. Như `Animation and transitions`, `Auto`, `Emoji`, `Fragment`, `Layout`, `Palette`, `TV`, `Wear`, ….

### 1. [Animation and transitions](https://developer.android.com/develop/ui/views/animations)

Di chuyển widgets và các transition giữa các màn hình

### 2. [Auto](https://developer.android.com/cars)

Thành phần giúp phát triển ứng dụng cho Android Auto.

### 3. [Emoji](https://developer.android.com/develop/ui/views/text-and-emoji/emoji-compat)

Kích hoạt và cập nhật các emoji cho các nền tảng cũ

### 4. [Fragment](https://developer.android.com/guide/fragments)

Một thành phần cơ bản trong UI

### 5. [Layout](https://developer.android.com/develop/ui/views/layout/declaring-layout)

Bố trí các widgets bằng cách sử dụng thuật toán khác nhau

### 6. [Palette](https://developer.android.com/develop/ui/views/graphics/palette-colors)

Trình chọn màu

### 7. [TV](https://developer.android.com/tv)

Thành phần giúp phát triển ứng dụng cho Android TV.

### 8. [Wear OS by Google](https://developer.android.com/wear)

Thành phần giúp phát triển ứng dụng cho Wear.


## IV. Behavior

Các thành phần ở nhóm này sẽ giúp ứng dụng của chúng ta có thể kết nối dễ dàng đến các dịch vụ của hệ thống. Bao gồm `Download Manager`, `Media & Playback`, `CameraX`, `Notifications`, `Permissions`, `Preferences`, `Sharing`, `Slices`, ….

### [Download manager](https://developer.android.com/reference/android/app/DownloadManager)

Đặt lịch & quản lý các tác vụ tải xuống

### 1. [Media and playback](https://developer.android.com/guide/topics/media/legacy)

Hỗ trợ tương thích ngược cho việc phát media và routing (bao gồm cả Google Cast)

### 2. [Notifications](https://developer.android.com/develop/ui/views/notifications)

Cung cấp các API tương thích ngược cho việc hiển thị thông báo, hỗ trợ cả Wear và Auto

### 3. [Permissions](https://developer.android.com/guide/topics/permissions/overview)

Cung cấp các API cho việc kiểm tra và yêu cầu các quyền trong android

### 4. [Sharing](https://developer.android.com/training/sharing)

Cung cấp các hành động chia sẻ phù hợp với action bar của ứng dụng

### 5. [Slices](https://developer.android.com/guide/slices)

Tạo các UI linh hoạt có thể hiển thị dữ liệu ứng dụng bên ngoài ứng dụng.

Để hoàn thiện bộ các tính năng mới ra mắt của Android Jetpack thì không thể không nhắc đến Slices component.

“Slice” là cách để hiển thị UI của ứng dụng bên trong Google Assistant.

-----

## Jetpack Compose

[Jetpack Compose](https://developer.android.com/jetpack/compose) là bộ công cụ hiện đại được Android khuyên dùng để xây dựng giao diện người dùng gốc. Nó đủ trưởng thành và cho phép bạn xây dựng giao diện người dùng dễ dàng hơn, nhanh hơn và ít mã hơn. Hơn nữa, bố cục XML dựa trên Soạn thảo và Chế độ xem có thể được kết hợp. Bạn có thể thêm giao diện người dùng Compose vào một ứng dụng hiện có sử dụng thiết kế dựa trên Chế độ xem hoặc bao gồm hệ phân cấp Chế độ xem Android trong giao diện người dùng Compose. Cách tiếp cận này đặc biệt hữu ích nếu bạn muốn sử dụng các thành phần giao diện người dùng chưa có trong Compose, như AdView hoặc MediaPlayer. Khi bạn bắt đầu một dự án mới, không có lý do gì để sử dụng bố cục XML nữa.

- [MDC for Android](https://m3.material.io/develop/android/mdc-android)
- [25 Videos - Jetpack Compose](https://www.youtube.com/playlist?list=PLHRvASjG6y05T7jdDC4YTwhTAT28rbYI1)
- [35 Videos - Jetpack Compose](https://www.youtube.com/playlist?list=PLQkwcJG4YTCSpJ2NLhDTHhi6XBNfk9WiC)
- [93 Videos - Jetpack Compose](https://www.youtube.com/playlist?list=PLSrm9z4zp4mEWwyiuYgVMWcDFdsebhM-r)
- [Android - Jetpack Compose](https://viblo.asia/p/android-jetpack-compose-L4x5x4qr5BM)
- [Cơ bản về Jetpack Compose](https://viblo.asia/p/co-ban-ve-jetpack-compose-Qbq5QQB35D8)
- [Jetpack Compose - UI Framework mới của Android ](https://viblo.asia/p/jetpack-compose-ui-framework-moi-cua-android-oOVlYoJoK8W)
- [Sử dụng Jetpack Compose để dựng UI trong Android](https://viblo.asia/p/su-dung-jetpack-compose-de-dung-ui-trong-android-m68Z07MMKkG)
- [Sử dụng Jetpack Compose cho project Android với mô hình MVVM](https://viblo.asia/p/su-dung-jetpack-compose-cho-project-android-voi-mo-hinh-mvvm-OeVKBJg0KkW)
- [Jetpack Compose cho người mới bắt đầu](https://viblo.asia/p/jetpack-compose-cho-nguoi-moi-bat-dau-phan-1-RnB5ppp75PG)
- [Jetpack Compose Tutorial - Step by Step Guide](https://viblo.asia/p/jetpack-compose-tutorial-step-by-step-guide-phan-1-924lJmraZPM)
- [Tản mạn về Jetpack Compose - Phần I](https://viblo.asia/p/tan-man-ve-jetpack-compose-maGK76qD5j2)
- [Tản mạn về Jetpack Compose - Phần II](https://viblo.asia/p/tan-man-ve-jetpack-compose-RnB5pp6d5PG)
- [Material theme trong jetpack compose](https://viblo.asia/p/material-theme-trong-jetpack-compose-jvEla9Nmlkw)

- [Codelabs - Navigate between screens with Compose](https://developer.android.com/codelabs/basic-android-kotlin-compose-navigation)
- [Effortless Navigation with Compose](https://blog.stackademic.com/effortless-navigation-with-compose-30d37ddf5625)
- [Navigation Basics in Jetpack Compose](https://youtu.be/glyqjzkc4fk)
- [Full Guide to Nested Navigation Graphs in Jetpack Compose](https://youtu.be/FIEnIBq7Ups)
- [Migrate Jetpack Navigation to Navigation Compose](https://developer.android.com/jetpack/compose/migrate/migration-scenarios/navigation)


# Kotlin Coroutines

Lập trình không đồng bộ hoặc không chặn là một phần quan trọng trong quá trình phát triển Android. Bạn phải xử lý những vấn đề không đồng bộ mỗi khi bạn muốn thực hiện các thao tác I/O hoặc các phép tính mở rộng. Kotlin giải quyết vấn đề này một cách linh hoạt bằng cách cung cấp [hỗ trợ coroutine](https://kotlinlang.org/docs/coroutines-overview.html) ở cấp độ ngôn ngữ và ủy quyền hầu hết chức năng cho các thư viện. Không cần phải tự mình triển khai logic luồng hoặc khởi động AsyncTask nữa. Nếu bạn tìm thấy một hướng dẫn sử dụng những thứ như vậy, hãy chắc chắn rằng nó rất cũ.

# Asynchronous Flow

Luồng không đồng bộ không có gì mới. Bạn có thể quen thuộc với các thư viện như RxJava/RxAndroid triển khai lập trình không đồng bộ với các luồng có thể quan sát được. Tuy nhiên, API này quá phức tạp đối với hầu hết các trường hợp sử dụng và quá trình học tập rất khó khăn. Tôi đã trải nghiệm các dự án trong đó các luồng Rx được liên kết theo cách phức tạp đến mức việc thực hiện các thay đổi đơn giản chỉ mất vài ngày thay vì vài phút. May mắn thay, chúng tôi đã có [Kotlin Flow](https://kotlinlang.org/docs/flow.html), một thư viện luồng không đồng bộ mới của JetBrains, công ty phát triển ngôn ngữ Kotlin. Có nhiều điểm tương đồng với luồng Rx, Kotlin Flow được xây dựng dựa trên Kotlin Coroutines. Nó triển khai nhiều toán tử nổi tiếng mà bạn có thể biết từ thế giới Rx và đơn giản hóa việc làm việc với các luồng không đồng bộ. Hãy ngừng sử dụng RxJava và yêu thích Flow!

# App Architecture

Thiết kế kiến trúc ứng dụng là một yếu tố quan trọng cần cân nhắc để đảm bảo rằng ứng dụng của bạn mạnh mẽ, có thể kiểm thử và bảo trì. Google không phải lúc nào cũng quan tâm nhiều đến Kiến trúc ứng dụng. May mắn thay, điều này đã thay đổi và hiện chúng tôi đã có hướng dẫn chính thức về [cấu trúc ứng dụng](https://developer.android.com/topic/architecture). Hướng dẫn thảo luận về các khái niệm như phân tách mối quan tâm, các lớp ứng dụng khác nhau, mô-đun hóa hoặc chèn phần phụ thuộc. Đọc toàn bộ hướng dẫn trước khi viết một dòng mã!

# Material Design

Mã của bạn phải rõ ràng nhưng đối với Giao diện người dùng thì điều đó đúng gấp đôi vì nó hiển thị cho người dùng. Không dễ để thiết kế một ứng dụng vừa đẹp vừa có chức năng. May mắn thay, chúng tôi có [Material Design](https://m3.material.io), một hệ thống thiết kế được xây dựng và hỗ trợ bởi các nhà thiết kế và nhà phát triển của Google. Material Design cung cấp rất nhiều thành phần, bố cục, hoạt ảnh và biểu tượng sẵn sàng để sử dụng hoặc tùy chỉnh theo nhu cầu của bạn. Người dùng đã quen thuộc với các thành phần như Nút hành động nổi hoặc Ngăn điều hướng, không có lý do gì để phát minh ra những cách khác nhau để thực hiện những việc tương tự. Ngoài ra, đừng quên nói với nhóm thiết kế của bạn rằng Ứng dụng Android không nên trông giống bản sao pixel hoàn hảo của ứng dụng iOS!

- [Material Design 3 in Compose](https://developer.android.com/jetpack/compose/designsystems/material3)

# User Experience

Thiết bị di động có một số hạn chế cụ thể như không gian màn hình nhỏ, hiệu suất hạn chế, dung lượng pin hoặc kết nối internet không ổn định. Dựa trên những hạn chế này, tôi có thể cung cấp cho bạn một vài gợi ý về những điều cần ghi nhớ. Ví dụ:

- Ứng dụng phải có thể thực hiện tất cả hoặc một phần quan trọng của chức năng cốt lõi mà không cần truy cập Internet.
- Ứng dụng phải duy trì trạng thái và thông tin đầu vào của người dùng. Hệ thống Android có thể tắt ứng dụng của bạn bất cứ lúc nào. Người dùng thường không muốn viết tin nhắn trò chuyện dài hai lần vì họ xoay màn hình hoặc chuyển đổi giữa các ứng dụng.
- Ứng dụng sẽ hiển thị rõ ràng trạng thái của nó. Người dùng sẽ biết khi nào nút được nhấn, tệp vẫn đang tải lên hay có xảy ra lỗi nào đó không.
- Màn hình di động nhỏ, loại bỏ sự phân tâm, tập trung vào một việc một lúc và làm tốt việc đó. Chia các quy trình nhiều bước thành nhiều màn hình hơn.

Nguyên tắc chung là cố gắng không làm người dùng thất vọng. Nếu bạn làm đúng mọi thứ, ứng dụng có UX chất lượng cao sẽ là kết quả công việc của bạn.

# Example App

Tôi đang làm việc trong một dự án nguồn mở nhỏ nơi tôi sẽ triển khai các phương pháp hay nhất đã đề cập.

Bạn có thể tìm thấy nó ở đây: [https://github.com/jurajkusnier/stock-browser](https://github.com/jurajkusnier/stock-browser)

Bản thân ứng dụng này rất đơn giản. Nó tải dữ liệu thị trường từ nhiều API của bên thứ 3 và lưu trữ chúng trong cơ sở dữ liệu cục bộ. Sau đó nó cho phép người dùng tìm kiếm, duyệt và đánh dấu các mục yêu thích.

Ứng dụng sử dụng mẫu kiến trúc MVI (Model View Intent), được triển khai bằng thư viện Orbit-MVI. Mỗi màn hình có ViewModel và ScreenState phù hợp. ViewModel đại diện cho nguồn gốc của màn hình. Nó xử lý tất cả thông tin đầu vào của người dùng và trả về trạng thái giao diện người dùng tương ứng được hiển thị trên màn hình. Ngoài trạng thái, ViewModel còn có thể tạo ra các tác dụng phụ được sử dụng chủ yếu để điều hướng giữa các màn hình. ViewModel gọi các trường hợp sử dụng khác nhau để hiển thị dữ liệu cho người dùng. Logic để tải và lưu dữ liệu từ các tài nguyên khác nhau được thực hiện bởi các kho lưu trữ và nguồn dữ liệu.

![Android](https://boxxv.github.io/img/2023/1_dugW9WtoXYPw5zfYlZZ5Nw.webp "Android")

# Free Resources

Tôi thực sự khuyên bạn nên xem [khóa học miễn phí](https://www.udacity.com/course/developing-android-apps-with-kotlin--ud9012) này của Google về Phát triển ứng dụng Android bằng Kotlin. Bạn cũng có thể bắt đầu với [khóa học miễn phí](https://developer.android.com/courses/android-basics-kotlin/course) này trên trang dành cho nhà phát triển Android, nơi các khái niệm được giảng dạy với sự trợ giúp của các phòng thí nghiệm mã, dự án và câu đố, đồng thời bạn cũng kiếm được huy hiệu khi biết các khái niệm đó xuất hiện trên hồ sơ nhà phát triển Google của mình. Ngoài ra, đây là một số tài nguyên để tìm hiểu thêm về các chủ đề được liệt kê ở trên.

- [Udacity - Phát triển ứng dụng Android với Kotlin](https://www.udacity.com/course/developing-android-apps-with-kotlin--ud9012)
- [Kiến thức cơ bản về Android trong Kotlin](https://developer.android.com/courses/android-basics-kotlin/course)
- [Hướng dẫn dành cho nhà phát triển Android](https://developer.android.com/guide)
- [Kodeco](https://www.kodeco.com)
- [How to Build an Android App in 2023](https://www.spaceotechnologies.com/blog/how-to-build-an-android-app/)

Training courses
- [Android Training courses](https://developer.android.com/courses)

For beginners
- [Android Basics with Compose](https://developer.android.com/courses/android-basics-compose/course)
  + Unit 1: Your first Android app
  + Unit 2: Building app UI
  + Unit 3: Display lists and use Material Design
  + Unit 4: Navigation and app architecture
  + Unit 5: Connect to the internet
  + Unit 6: Data persistence
  + Unit 7: WorkManager
  + Unit 8: Views and Compose


- [Android Basics in Kotlin](https://developer.android.com/courses/android-basics-kotlin/course)

For experienced Android developers
- [Jetpack Compose for Android developers](https://developer.android.com/courses/jetpack-compose/course)
- [Modern Android app architecture](https://developer.android.com/courses/pathways/android-architecture)
- [Make your Android app more accessible](https://developer.android.com/courses/pathways/make-your-android-app-accessible)
- [Use coroutines in common Android use cases](https://developer.android.com/courses/pathways/android-coroutines)

Kotlin language training
- [Kotlin Bootcamp for Programmers](https://developer.android.com/courses/kotlin-bootcamp/overview)
- [Kotlin for Java developers](https://developer.android.com/courses/pathways/kotlin-for-java)

For Android Java developers
- [Android Room with a View - Java](https://developer.android.com/codelabs/android-room-with-a-view)
- [Background Work with WorkManager - Java](https://developer.android.com/codelabs/android-workmanager-java)

Certification and degree programs
- [Associate Android Developer](https://developers.google.com/certification/associate-android-developer)
- [Google Play Store Listing Certificate](https://playacademy.withgoogle.com/intl/vi/certificate/)
- [Android Kotlin Developer](https://www.udacity.com/course/android-kotlin-developer-nanodegree--nd940)

# Tổng kết

Cảm ơn bạn đã đọc. Nếu bạn thích bài viết này, hãy thích, để lại phản hồi và chia sẻ nó với bạn bè của bạn. Happy coding - Lập trình vui vẻ!

-----
Tham khảo
- [Developing Android App in 2023](https://medium.com/@jurajkunier/developing-android-app-in-2023-60504dd76e38)
- [Introduction to Android Jetpack](https://www.geeksforgeeks.org/introduction-to-android-jetpack/)
  + [Foundation Components of Android Jetpack](https://www.geeksforgeeks.org/foundation-components-of-android-jetpack/)
  + [Jetpack Architecture Components in Android](https://www.geeksforgeeks.org/jetpack-architecture-components-in-android/)
  + [Behaviour Components of Android Jetpack](https://www.geeksforgeeks.org/jetpack-architecture-components-in-android/)
  + [UI Components of Android Jetpack](https://www.geeksforgeeks.org/ui-components-of-android-jetpack/)
- [Android Jetpack Compose – Interoperability Using Compose in XML Layouts](https://www.geeksforgeeks.org/android-jetpack-compose-interoperability-using-compose-in-xml-layouts/)
- [Architecture Components in Android Jetpack](https://www.scaler.com/topics/architecture-components-in-android-jetpack/)

- [Android Jetpack là gì? Tại sao bạn nên biết](https://vntalking.com/android-jetpack-la-gi.html)
- [Thông Thạo Jetpack – Phần 1 – Jetpack Là Gì?](https://yellowcodebooks.com/2021/04/07/thong_thao_jetpack_phan_1_jetpack_la_gi/)
- [Thông Thạo Jetpack – Phần 2 – Android KTX](https://yellowcodebooks.com/2021/04/14/thong_thao_jetpack_phan_2_android_ktx/)
- [Thông Thạo Jetpack – Phần 3 – Navigation](https://yellowcodebooks.com/2021/05/26/thong-thao-jetpack-phan-3-navigation/)
- [Thông Thạo Jetpack – Phần 4 – Navigation (Tập 2)](https://yellowcodebooks.com/2021/06/09/thong-thao-jetpack-phan-4-navigation-tap-2/)
- [Thông Thạo Jetpack – Phần 5 – Navigation (Tập 3)](https://yellowcodebooks.com/2021/06/24/thong-thao-jetpack-phan-5-navigation-tap-3/)
- [Thông Thạo Jetpack – Phần 6 – Navigation (Tập Cuối)](https://yellowcodebooks.com/2021/08/31/thong-thao-jetpack-phan-6-navigation-tap-cuoi/)
- [Android Architecture Component](https://yellowcodebooks.com/category/lap-trinh-android/android-nang-cao/android-nang-cao-android-architecture-component/)

- [Modern Android Architectures – MVC/MVP/MVVM – Phần 1: Giới Thiệu Các Mô Hình Kiến Trúc](https://yellowcodebooks.com/2020/04/22/modern-android-architectures-mvc-mvp-mvvm-phan-1-gioi-thieu-cac-mo-hinh-kien-truc/)
- [Modern Android Architectures – MVC/MVP/MVVM – Phần 2: Kiến Trúc MVC](https://yellowcodebooks.com/2020/05/27/modern-android-architectures-mvc-mvp-mvvm-phan-2-kien-truc-mvc/)
- [Modern Android Architectures – MVC/MVP/MVVM – Phần 3: Kiến Trúc MVP](https://yellowcodebooks.com/2022/03/06/modern-android-architectures-mvc-mvp-mvvm-phan-3-kien-truc-mvp/)
- [Cơ Bản – Bài Học Theo Chương Trình (36B)](https://yellowcodebooks.com/category/lap-trinh-android/android-co-ban-bai-hoc-theo-chuong-trinh/)

-----
- [Phát triển ứng dụng Android - 34 điều tôi đã rút ra được kinh nghiệm](https://viblo.asia/p/phat-trien-ung-dung-android-34-dieu-toi-da-rut-ra-duoc-kinh-nghiem-OeVKBxX0lkW)
- [Android Adaptive Launcher Icon – Tất Cả Thông Tin Bạn Cần Biết](https://yellowcodebooks.com/2023/05/23/android-adaptive-launcher-icon-tat-ca-thong-tin-ban-can-biet/)