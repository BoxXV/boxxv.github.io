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
	- [Jetpack Compose](#jetpack-compose)
- [Example App](#example-app)
- [Free Resources](#free-resources)
- [Tổng kết](#tổng-kết)



![Android](https://boxxv.github.io/img/2023/android-14-h.jpeg "Android")

Trong bài viết ngắn này, tôi tóm tắt một số đề xuất cũng như thực tiễn tốt nhất và phổ biến mới dành cho nhà phát triển ứng dụng Android. Hãy thoải mái sử dụng chúng khi bạn xây dựng một dự án greenfield mới hoặc khi bạn muốn loại bỏ giao diện cũ khỏi các ứng dụng hiện có của mình.

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

For beginners
- [Android Training courses](https://developer.android.com/courses)

For beginners
- [Android Basics with Compose](https://developer.android.com/courses/android-basics-compose/course)
- [Android Basics in Kotlin](https://developer.android.com/courses/android-basics-kotlin/course)

For experienced Android developers
- [Jetpack Compose for Android developers](https://developer.android.com/courses/jetpack-compose/course)
- [Modern Android app architecture](https://developer.android.com/courses/pathways/android-architecture)
- []()
- []()

Kotlin language training
- []()
- []()

For Android Java developers
- []()
- []()

Certification and degree programs
- []()
- []()
- []()

# Tổng kết

Cảm ơn bạn đã đọc. Nếu bạn thích bài viết này, hãy thích, để lại phản hồi và chia sẻ nó với bạn bè của bạn. Happy coding - Lập trình vui vẻ!

-----
Tham khảo
- [Developing Android App in 2023](https://medium.com/@jurajkunier/developing-android-app-in-2023-60504dd76e38)
- [Introduction to Android Jetpack](https://www.geeksforgeeks.org/introduction-to-android-jetpack/)
  + [Foundation Components of Android Jetpack](https://www.geeksforgeeks.org/foundation-components-of-android-jetpack/)
  + [Jetpack Architecture Components in Android](https://www.geeksforgeeks.org/jetpack-architecture-components-in-android/)
  + [Behaviour Components of Android Jetpack](https://www.geeksforgeeks.org/jetpack-architecture-components-in-android/)
  + [Behaviour Components of Android Jetpack](https://www.geeksforgeeks.org/ui-components-of-android-jetpack/)
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
- []()

-----
- [Phát triển ứng dụng Android - 34 điều tôi đã rút ra được kinh nghiệm](https://viblo.asia/p/phat-trien-ung-dung-android-34-dieu-toi-da-rut-ra-duoc-kinh-nghiem-OeVKBxX0lkW)
- [Android Adaptive Launcher Icon – Tất Cả Thông Tin Bạn Cần Biết](https://yellowcodebooks.com/2023/05/23/android-adaptive-launcher-icon-tat-ca-thong-tin-ban-can-biet/)
- []()