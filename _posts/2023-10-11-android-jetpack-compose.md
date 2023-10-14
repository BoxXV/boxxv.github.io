---
layout: post
title: Jetpack Compose
subtitle: Phát triển ứng dụng Android năm 2023
description: Sử dụng Jetpack Compose để dựng UI trong Android
author: AndroidDev
image: "img/2023/1_tDFPLaEDlaW5dtsfv4sd0A.webp"
tags:
- Android
- Kotlin
- Jetpack
- Compose
- Material Design
---

# Mục lục

- [Mục lục](#mục-lục)
- [Tổng quan](#tổng-quan)
  - [Giải quyết vấn đề với Jetpack Compose](#giải-quyết-vấn-đề-với-jetpack-compose)
  - [Đặc điểm cơ bản của Jetpack Compose](#đặc-điểm-cơ-bản-của-jetpack-compose)
  - [Jetpack Compose’s tech stack](#jetpack-composes-tech-stack)
- [Các thành phần của Jetpack Compose](#các-thành-phần-của-jetpack-compose)
  - [1. Surface](#1-surface)
  - [2. Scaffold](#2-scaffold)
  - [3. TopAppBar](#3-topappbar)
  - [4. FloatingActionButton](#4-floatingactionbutton)
  - [5. Card](#5-card)
  - [6. Box](#6-box)
  - [7. Row](#7-row)
  - [8. Column](#8-column)
  - [9. Spacer](#9-spacer)
  - [10. Text](#10-text)
  - [11. TextButton](#11-textbutton)
  - [12. TextField](#12-textfield)
  - [13. Button](#13-button)
  - [14. Image](#14-image)
  - [15. Icon](#15-icon)
  - [16. LazyColumn](#16-lazycolumn)
  - [17. LazyRow](#17-lazyrow)
  - [18. LazyVerticalGrid](#18-lazyverticalgrid)
  - [19. AlertDialog](#19-alertdialog)
  - [20. CircularProgressIndicator](#20-circularprogressindicator)
  - [21. LinearProgressIndicator](#21-linearprogressindicator)
  - [22. CheckBox](#22-checkbox)
  - [23. RadioButton](#23-radiobutton)
  - [24. Slider](#24-slider)
  - [25. Switch](#25-switch)
  - [26. SnackBar](#26-snackbar)
  - [27. Divider](#27-divider)
  - [28. DropDownMenu](#28-dropdownmenu)
  - [1. Modifiers](#1-modifiers)
  - [2. remember](#2-remember)
  - [3. rememberSaveable](#3-remembersaveable)
  - [4. animateContentSize](#4-animatecontentsize)
  - [5. Shape](#5-shape)
  - [Live Preview](#live-preview)
- [Example App](#example-app)
- [Free Resources](#free-resources)
- [Ứng dụng được xây dựng bằng Compose](#ứng-dụng-được-xây-dựng-bằng-compose)
- [Tổng kết](#tổng-kết)



![Compose](https://boxxv.github.io/img/2023/android-tips-for-working-with-preview-in-jetpack-compose.png "Compose")

# Tổng quan

Tại Google I/O 2019, Google đã giới thiệu Jetpack Compose. Cùng với đó, Android Studio 4.0 (phiên bản thử nghiệm) cũng đã hỗ trợ phát triển ứng dụng sử dụng Jetpack Compose.

[`Jetpack Compose`](https://developer.android.com/jetpack/compose?hl=vi) là một bộ công cụ hiện đại, được khuyên dùng cho Android để xây dựng giao diện người dùng gốc (native). Công cụ này đơn giản hoá và đẩy nhanh quá trình phát triển giao diện người dùng trên Android. Nhanh chóng đưa ứng dụng vào hoạt động với mã ngắn gọn hơn, các công cụ mạnh mẽ và API Kotlin trực quan. Đối với ai từng lập trình Flutter hoặc React Native thì sẽ dễ dàng hơn rất nhiều vì ý tưởng của compose cũng dựa trên việc thiết kế UI theo dạng cây.

- [Thiết lập môi trường](https://developer.android.com/jetpack/compose/setup?hl=vi) phát triển và dùng Compose.

![Java đã chết, Kotlin trường tồn](https://boxxv.github.io/img/2023/5b84c1f10041d41f8d50.jpg "Java đã chết, Kotlin trường tồn")

## Giải quyết vấn đề với Jetpack Compose

Compose có cơ chế khá giống với các khung UI framework hiện có như React, Litho hoặc Flutter.

UI framework hiện tại của Android đã có từ năm 2008 và theo thời gian, nó đã trở nên phức tạp hơn rất nhiều. Jetpack Compose ra đời nhằm mục đích bắt đầu sự mới mẻ trong việc thiết kế giao diện dựa trên các component. Framework này được viết với các mục tiêu chính:

- **Tách biệt khỏi các bản platform release**: Điều này cho phép việc sửa lỗi và release sản phẩm nhanh chóng hơn vì nó độc lập với các bản phát hành Android mới.
- **Ít các thành phần giao diện hơn**: Không bắt buộc bạn phải sử dụng View hay Fragment khi tạo giao diện người dùng của mình. Tất cả mọi thứ là một component và có thể được kết hợp tự do với nhau.
- **Làm rõ quyền sở hữu trạng thái (state) và xử lý sự kiện**: Một trong những điều quan trọng và phức tạp nhất để có trong các ứng dụng lớn là việc xử lý luồng dữ liệu và trạng thái trong giao diện người dùng của bạn. Compose cho ta biết rõ cái gì đang chịu trách nhiệm về trạng thái và cách xử lý các sự kiện, tương tự như cách React xử lý việc này.
- **Viết ít mã hơn**: Viết UI trong Android thường yêu cầu RẤT NHIỀU mã, đặc biệt là khi tạo bố cục phức tạp hơn (ví dụ với RecyclerView chẳng hạn). Compose đơn giản hóa đáng kể cách bạn xây dựng giao diện người dùng của mình.

Điều này giúp ta dễ dàng tạo các thành phần biệt lập và có thể tái sử dụng, khiến việc tạo một màn hình mới với các thành phần hiện có trở nên dễ dàng hơn. Giúp bạn có nhiều thời gian hơn tập trung vào việc tạo trải nghiệm người dùng tuyệt vời thay vì cố gắng giữ giữ View hierarchy thật phẳng.

## Đặc điểm cơ bản của Jetpack Compose

- `@Composable` là annotation dùng để đánh dấu một function là compose function.
- `@Model` là annotation được dùng để đánh dấu một class sẽ làm cho ui tương ứng với class đó được cập nhật khi giá trị của model thay đổi.
- Luồng của dữ liệu luôn luôn là từ trên xuống dưới. Do đó, trong mô hình MVVM dữ liệu sẽ đi từ Repository -> ViewModel -> Activity và từ Activity thì stateModel được update, từ đó UI được update.
- Để có thể xử lý các sự kiện từ UI như là click button, chúng ta sẽ sử dụng biểu thức lambda để cập nhật Activity mà sự kiện này xảy ra. Từ Activity, luồng sự kiện sẽ là Activity -> ViewModel -> Repository và từ Repository dữ liệu sẽ được gửi trở về bằng luồng đã được nhắc tới ở trên.
- Ứng dụng này chỉ sử dụng cho mục đích demo là chủ yếu, do đó mình sẽ cố gắng sử dụng ít code nhất có thể. Cùng với đó, mình sẽ không sử dụng Repository Pattern mà thay vào đó là dữ liệu tĩnh được khởi tạo trục tiếp từ trong ViewModel.

## Jetpack Compose’s tech stack

![Compose](https://boxxv.github.io/img/2023/6c4427aa-b4a2-4ed9-8b11-f63d839b84f0.webp "Compose")

# Các thành phần của Jetpack Compose

Jetpack Compose có nhiều thành phần khác nhau và linh hoạt để soạn giao diện người dùng của bạn trên màn hình và trên blog này chúng tôi sẽ khám phá từng thành phần một, vì vậy, không chần chừ gì nữa, hãy chuyển sang phần tiếp theo và bắt đầu khám phá !!!

> Lưu ý: Giống như mọi thứ trong Flutter đều là Widget, hầu hết mọi thứ trong Compose đều có thể kết hợp hoặc nằm trong một hàm được chú thích bằng `@Composable`. Giống như ví dụ dưới đây:

```kotlin
@Composable
fun YourComposable() {
    //Your implementation on composable or UI components placed together in it.
}
```

## 1. Surface

> A Surface is anything on which you can place any other components or apply some property on it to give some shape or look.

Surface là bất cứ thứ gì mà bạn có thể đặt bất kỳ thành phần nào khác lên đó hoặc áp dụng một số thuộc tính lên nó để tạo ra một số hình dạng hoặc diện mạo.

```kotlin
```

## 2. Scaffold

> Scaffold is kind of a basic structure that any app can have in general. For example, Toolbar or TopAppBar, Side Drawer, Bottom Navigation Menu, FloatingActionButton, Main Content, etc.

```kotlin
```

## 3. TopAppBar

> TopAppBar as the name suggests stays at the top of your screen and acts a Toolbar in Android from where you can handle back navigation(s), options menu and things like that.

```kotlin
```

## 4. FloatingActionButton

> A FloatingActionButton or FAB acts as the floating button in your screen which you can keep to allow user to perform some quick action or jump into next screen.

```kotlin
```

## 5. Card

> A Card is a that layout which we can use to display a particular part of our screen little bit elevated or with rounded corners mostly we use this to design our list’s single row item.

```kotlin
```

## 6. Box

> A Box in Compose is a layout which renders its child components stack over each other and provides various properties to align its children according to the requirement. It is similar to Stack in Flutter and FrameLayout in Android XML.

```kotlin
```

## 7. Row

> A Row places its child components in horizontal manner as the name suggests and similar to LinearLayout with “horizontal” orientation in Android XML.

```kotlin
```

![Row](https://boxxv.github.io/img/2023/51c199c8a23bd6a8_856.png "Row")

## 8. Column

> A Column places its child components in vertical manner as the name suggests and similar to LinearLayout with “vertical” orientation in Android XML.

```kotlin
```

## 9. Spacer

> A Spacer is that component which we can use it for providing space between different components. It is similar to View in Android XML.

```kotlin
```

## 10. Text

> A Text is a simple label or text you want to display on screen to portray or convey something.

```kotlin
```

## 11. TextButton

> A TextButton is a mix of Text and Button component means it will look like a Text but it can be clickable as well.

```kotlin
```

## 12. TextField

> A TextField in Compose is similar to EditText in Android and it allows user to input some value in it.

```kotlin
```

## 13. Button

> A Button in Compose is a way to show an actionable component which can be clicked and can perform some given action.

```kotlin
```

## 14. Image

> An Image in Compose is used to display image or picture from remote URL, drawable, or, app assets. You can use Coil Compose library to display remote image URL in your Image component.

```kotlin
```

## 15. Icon

> An Icon is used to display various different icons to provide some added information about that field or label. You can also wrap Icon under IconButton component to upgrade that icon to make it clickable as well.

```kotlin
```

## 16. LazyColumn

> A LazyColumn represents a list of data displayed in vertical manner and it is similar to RecyclerView with a vertical LinearLayout orientation.

```kotlin
@Composable
fun ShowLazyColumnSample() {
    val list = (1..50).map { it.toString() }
    Column(Modifier.padding(20.dp)) {
        LazyColumn {
            items(list) { item ->
                SampleLazyColumnItem(item)
            }
        }
    }
}

@Composable
fun SampleLazyColumnItem(item: String) {
    Card(
        elevation = 5.dp, modifier = Modifier
            .padding(5.dp)
            .fillMaxWidth()
    ) {
        Text("List Item #$item", modifier = Modifier.padding(10.dp))
    }
}
```

## 17. LazyRow

> A LazyRow represents a list of data displayed in horizontal manner and it is similar to RecyclerView with a horizontal LinearLayout orientation.

```kotlin

@Composable
fun ShowLazyRowSample() {
    val list = (1..50).map { it.toString() }
    Column(Modifier.padding(20.dp)) {
        LazyRow {
            items(list) { item ->
                SampleLazyRowItem(item)
            }
        }
    }
}

@Composable
fun SampleLazyRowItem(item: String) {
    Card(
        elevation = 5.dp, modifier = Modifier
            .padding(5.dp)
            .wrapContentWidth()
            .wrapContentHeight()
    ) {
        Text("List Item #$item", modifier = Modifier.padding(10.dp), maxLines = 1)
    }
}
```

## 18. LazyVerticalGrid

> A LazyVerticalGrid represents a grid of data displayed in vertical manner and it is similar to RecyclerView with a vertical GridLayoutManager.

```kotlin
@OptIn(ExperimentalFoundationApi::class)
@Composable
fun ShowLazyVerticalGridSample() {
    val list = (1..50).map { it.toString() }
    Column(Modifier.padding(20.dp)) {
        LazyVerticalGrid(cells = GridCells.Fixed(3), content = {
            items(list) { item ->
                ShowLazyVerticalGridSample(item)
            }
        })
    }
}

@Composable
fun ShowLazyVerticalGridSample() {
    val list = (1..50).map { it.toString() }
    Column(Modifier.padding(20.dp)) {
        LazyRow {
            items(list) { item ->
                SampleLazyRowItem(item)
            }
        }
    }
}
```

## 19. AlertDialog

> An AlertDialog in Compose serves the similar purpose as in other languages of showing a dialog or popup to the user on performing some action on the app components.

```kotlin
```

## 20. CircularProgressIndicator

> A CircularProgressIndicator is a component used to show any kind of progress in circular or circle shaped indicator. It can be determinate and indeterminate.

```kotlin
```

## 21. LinearProgressIndicator

> A LinearProgressIndicator is a component used to show any kind of progress in linear or horizontally placed indicator. It can also be determinate and indeterminate.

```kotlin
```

## 22. CheckBox

> A Checkbox component in Compose provides functionality of choosing multiple items from given list of items for example selection of hobbies.

```kotlin
```

## 23. RadioButton

> A RadioButton component in Compose provides functionality of choosing single item from given list of items for example selection of gender.

```kotlin
```

## 24. Slider

> A Slider component in Compose provides functionality of choosing some value by sliding through one horizontal slider for example choosing price from low to high.

```kotlin
```

## 25. Switch

> A Switch component in Compose provides functionality of choosing from two possible options for example enable push notifications or not.

```kotlin
```

## 26. SnackBar

> A SnackBar component in Compose provides functionality of showing a minimal popup kind of layout for temporary basis to convey some information to the user like showing — Your post is updated !!!

```kotlin
```

## 27. Divider

> A Divider component in Compose provides functionality of showing a horizontal or vertical line in between some components in your screen to convey some partition or difference.

```kotlin
```

## 28. DropDownMenu

> A DropDownMenu component in Compose provides functionality of choosing single item from list of related items like choosing profession from dropdown menu.

```kotlin
```

-----

## 1. Modifiers

> Modifiers in Compose provides us the functionalities or properties through which we can change the layout of our composables or set some intrinsic values like height, width, size, or, padding apart from any composable’s default properties.

Friendly Note: The ordering of properties in modifier matters, it can change the whole complexion of the composable. Try to experiment and explore it yourself.

## 2. remember

> remember in Compose is mainly used to perform local state management means to preserve values in the screen while user is interacting with those values. It can used to perform operations like tracking textfield while user types in it, or showing alert dialog on some button click, etc.

## 3. rememberSaveable

> rememberSaveable in Compose is almost similar to remember we learnt but if you observe properly your values will not be retained after screen rotation or any configuration changed when using remember and that is why we have rememberSaveable which will retain the values every time whatever the scenario.

Friendly Note: Try to rotate the screen and observe revenue variable is retaining the current revenue and not vanishing to 0 again on configuration change.

## 4. animateContentSize

> Animations are the fun part and of course Compose provides it too. But one of my favorite animation provided by Compose is animateContentSize and the beauty of this animation is how smoothly it gives the transition when size changes in any composable.
> And fun fact is it comes as a simple property in our beloved Modifiers. You just have to append this in your modifier property and provide some animation values. Thats it.

## 5. Shape

> We all love to shape our components in our UIs. Thus Compose also gives us the handy shapes to work out and upgrade our boring existing composables into rectangle, circle, rounded rectangle, or, cut corner shapes.

Friendly Note: You can’t just provide shapes to your composables using clip property in modifier but you have to just check whether any component provide “shape” property in their methods or not and if you found “shape” in it you can directly give any shape like we gave in clip property.

-----


## Live Preview

Live Preview là một tính năng của ANdorid Studio cho phép bạn kiểm tra và so sánh các composable functions thông qua orientation, kích thước font và theme mà không cần phải deploy lại ứng dụng.

Để tạo một live preview, tạo mới một composable function không có tham số bao gồm annotation `@Preview` ở bên trên annotation `@Composable``:

- [Android - Jetpack Compose](https://viblo.asia/p/android-jetpack-compose-L4x5x4qr5BM)

[Jetpack Compose](https://developer.android.com/jetpack/compose) là bộ công cụ hiện đại được Android khuyên dùng để xây dựng giao diện người dùng gốc. Nó đủ trưởng thành và cho phép bạn xây dựng giao diện người dùng dễ dàng hơn, nhanh hơn và ít mã hơn. Hơn nữa, bố cục XML dựa trên Soạn thảo và Chế độ xem có thể được kết hợp. Bạn có thể thêm giao diện người dùng Compose vào một ứng dụng hiện có sử dụng thiết kế dựa trên Chế độ xem hoặc bao gồm hệ phân cấp Chế độ xem Android trong giao diện người dùng Compose. Cách tiếp cận này đặc biệt hữu ích nếu bạn muốn sử dụng các thành phần giao diện người dùng chưa có trong Compose, như AdView hoặc MediaPlayer. Khi bạn bắt đầu một dự án mới, không có lý do gì để sử dụng bố cục XML nữa.

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
- [Android Basics in Kotlin](https://developer.android.com/courses/android-basics-kotlin/course)

For experienced Android developers
- [Jetpack Compose for Android developers](https://developer.android.com/courses/jetpack-compose/course)
- [Modern Android app architecture](https://developer.android.com/courses/pathways/android-architecture)
- [Make your Android app more accessible](https://developer.android.com/courses/pathways/make-your-android-app-accessible)
- [Use coroutines in common Android use cases](https://developer.android.com/courses/pathways/android-coroutines)

Kotlin language training
- [Kotlin Bootcamp for Programmers](https://developer.android.com/courses/kotlin-bootcamp/overview)
- [Kotlin for Java developers](https://developer.android.com/courses/pathways/kotlin-for-java)

#  Ứng dụng được xây dựng bằng Compose

![Compose](https://boxxv.github.io/img/2023/d825a7a669eebeb0e7ff.jpg "Compose")

# Tổng kết

Jetpack Compose là tương lai mà các lập trình viên Android cần thiết để xây dựng UI cho ứng dụng của mình một cách nhanh chóng và trực quan hơn. Không những thế nó còn loại bỏ được những khó khăn trong việc kiến trúc một ứng dụng Android.

-----
Tham khảo
- [Complete Jetpack Compose Tutorial For Beginners](https://appdevnotes.com/complete-jetpack-compose-tutorial-for-beginners/)
- [The Journey of Jetpack 🚀 — Compose](https://proandroiddev.com/the-journey-of-jetpack-compose-i-eef660bc546b)
- [Tips for working with Preview in Jetpack Compose](https://nimblehq.co/blog/tips-for-working-with-preview-in-jetpack-compose)
- [Jetpack Compose 1.4 Essentials: Developing Android Apps with Jetpack Compose 1.4, Android Studio, and Kotlin](https://www.amazon.com/Jetpack-Compose-1-4-Essentials-Developing-ebook/dp/B0CHMSDJDY/)
- [Jetpack Compose by Tutorials (Second Edition): Building Beautiful UI With Jetpack Compose](https://www.amazon.com/Jetpack-Compose-Tutorials-Second-Beautiful/dp/1950325830/)
- [Cheat sheet for Jetpack Compose](https://proandroiddev.com/cheat-sheet-for-jetpack-compose-7a197909fa42)
- [The Ultimate Jetpack Compose Cheat Sheet](https://hackernoon.com/the-ultimate-jetpack-compose-cheat-sheet)
- [Jetpack Compose Cheat Sheet: Part One](https://medium.com/jetpack-composers/jetpack-compose-cheat-sheet-part-one-263e0a26a844)
- [Jetpack Compose Cheat Sheet: Part Two](https://medium.com/jetpack-composers/jetpack-compose-cheat-sheet-part-two-6321f8c5d980)
- [Jetpack Compose Cheat Sheet: Part Three](https://medium.com/jetpack-composers/jetpack-compose-cheat-sheet-part-three-299cd6e21872)
- [Jetpack Compose Cheat Sheet: Part Four](https://dharmeshbasapati.medium.com/jetpack-compose-cheat-sheet-part-four-10b713e7790a)
- [Animation cheat sheet](https://developer.android.com/jetpack/compose/animation/resources)
- [Testing cheatsheet](https://developer.android.com/jetpack/compose/testing-cheatsheet)

-----
- [JetpackComposeVersion.com](https://www.jetpackcomposeversion.com/)
- [MDC for Android](https://m3.material.io/develop/android/mdc-android)
- [25 Videos - Jetpack Compose](https://www.youtube.com/playlist?list=PLHRvASjG6y05T7jdDC4YTwhTAT28rbYI1)
- [35 Videos - Jetpack Compose](https://www.youtube.com/playlist?list=PLQkwcJG4YTCSpJ2NLhDTHhi6XBNfk9WiC)
- [93 Videos - Jetpack Compose](https://www.youtube.com/playlist?list=PLSrm9z4zp4mEWwyiuYgVMWcDFdsebhM-r)
- [Android - Jetpack Compose](https://viblo.asia/p/android-jetpack-compose-L4x5x4qr5BM)
- [Cơ bản về Jetpack Compose](https://viblo.asia/p/co-ban-ve-jetpack-compose-Qbq5QQB35D8)
- [Jetpack Compose - UI Framework mới của Android ](https://viblo.asia/p/jetpack-compose-ui-framework-moi-cua-android-oOVlYoJoK8W)
- [Sử dụng Jetpack Compose để dựng UI trong Android](https://viblo.asia/p/su-dung-jetpack-compose-de-dung-ui-trong-android-m68Z07MMKkG)
- [Sử dụng Jetpack Compose cho project Android với mô hình MVVM](https://viblo.asia/p/su-dung-jetpack-compose-cho-project-android-voi-mo-hinh-mvvm-OeVKBJg0KkW)
- [Jetpack Compose With MVVM](https://medium.com/@kushaldave2011/jetpack-compose-with-mvvm-5c8b0ad00e50)
- [Jetpack Compose cho người mới bắt đầu](https://viblo.asia/p/jetpack-compose-cho-nguoi-moi-bat-dau-phan-1-RnB5ppp75PG)
- [Jetpack Compose Tutorial - Step by Step Guide](https://viblo.asia/p/jetpack-compose-tutorial-step-by-step-guide-phan-1-924lJmraZPM)
- [Jetpack Compose Tutorial - Step by Step Guide](https://blog.mindorks.com/jetpack-compose-tutorial/)
- [https://github.com/MindorksOpenSource/Jetpack-Compose-Android-Examples](https://github.com/MindorksOpenSource/Jetpack-Compose-Android-Examples)
- [Tản mạn về Jetpack Compose - Phần I](https://viblo.asia/p/tan-man-ve-jetpack-compose-maGK76qD5j2)
- [Tản mạn về Jetpack Compose - Phần II](https://viblo.asia/p/tan-man-ve-jetpack-compose-RnB5pp6d5PG)
- [Material theme trong jetpack compose](https://viblo.asia/p/material-theme-trong-jetpack-compose-jvEla9Nmlkw)

-----
- [Navigation in Jetpack Compose](https://developer.android.com/courses/pathways/android-basics-compose-unit-4-pathway-2)
- [Codelabs - Navigate between screens with Compose](https://developer.android.com/codelabs/basic-android-kotlin-compose-navigation)
- [Effortless Navigation with Compose](https://blog.stackademic.com/effortless-navigation-with-compose-30d37ddf5625)
- [Navigation Basics in Jetpack Compose](https://youtu.be/glyqjzkc4fk)
- [Full Guide to Nested Navigation Graphs in Jetpack Compose](https://youtu.be/FIEnIBq7Ups)
- [Modular Navigation with Jetpack Compose](https://medium.com/google-developer-experts/modular-navigation-with-jetpack-compose-fda9f6b2bef7)
- [Nested Navigation Graph in Jetpack Compose with Bottom Navigation](https://medium.com/@mathroda/nested-navigation-graph-in-jetpack-compose-with-bottom-navigation-d983c2d4119f)
- [Migrate Jetpack Navigation to Navigation Compose](https://developer.android.com/jetpack/compose/migrate/migration-scenarios/navigation)

-----
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
- [Android Architecture Component](https://yellowcodebooks.com/category/lap-trinh-android/android-nang-cao/android-nang-cao-android-architecture-component/)
- [Modern Android Architectures – MVC/MVP/MVVM – Phần 1: Giới Thiệu Các Mô Hình Kiến Trúc](https://yellowcodebooks.com/2020/04/22/modern-android-architectures-mvc-mvp-mvvm-phan-1-gioi-thieu-cac-mo-hinh-kien-truc/)
- [Modern Android Architectures – MVC/MVP/MVVM – Phần 2: Kiến Trúc MVC](https://yellowcodebooks.com/2020/05/27/modern-android-architectures-mvc-mvp-mvvm-phan-2-kien-truc-mvc/)
- [Modern Android Architectures – MVC/MVP/MVVM – Phần 3: Kiến Trúc MVP](https://yellowcodebooks.com/2022/03/06/modern-android-architectures-mvc-mvp-mvvm-phan-3-kien-truc-mvp/)
- [Cơ Bản – Bài Học Theo Chương Trình (36B)](https://yellowcodebooks.com/category/lap-trinh-android/android-co-ban-bai-hoc-theo-chuong-trinh/)
- [Phát triển ứng dụng Android - 34 điều tôi đã rút ra được kinh nghiệm](https://viblo.asia/p/phat-trien-ung-dung-android-34-dieu-toi-da-rut-ra-duoc-kinh-nghiem-OeVKBxX0lkW)
- [Android Adaptive Launcher Icon – Tất Cả Thông Tin Bạn Cần Biết](https://yellowcodebooks.com/2023/05/23/android-adaptive-launcher-icon-tat-ca-thong-tin-ban-can-biet/)