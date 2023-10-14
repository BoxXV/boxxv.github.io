---
layout: post
title: Điều hướng dễ dàng với Jetpack Compose
subtitle: Full Guide to Navigation in Jetpack Compose
description: Hướng dẫn từng bước để có trải nghiệm người dùng mượt mà
author: "Google Developers Training team"
image: "img/2023/android-tips-for-working-with-preview-in-jetpack-compose.png"
tags:
- Android
- Kotlin
- Jetpack
- Compose
- Material Design
- Navigation
---

# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
  - [Techical Stack](#techical-stack)
- [Hướng dẫn từng bước](#hướng-dẫn-từng-bước)
  - [Xác định các tuyến (routes) và tạo NavHostController](#xác-định-các-tuyến-routes-và-tạo-navhostcontroller)
- [Tổng kết](#tổng-kết)

![Compose](https://boxxv.github.io/img/2023/1_7v6mG_QL5vriYBdwkTLRww.webp "Compose")

# Giới thiệu

Trong quá trình phát triển Android hiện đại, các ứng dụng nhiều màn hình được tạo bằng thành phần Điều hướng `Jetpack`. Thành phần Điều hướng (`Navigation`) trong `Compose` cho phép bạn dễ dàng xây dựng ứng dụng nhiều màn hình trong Compose bằng phương pháp khai báo, tương tự như việc tạo giao diện người dùng. Lớp học lập trình này giới thiệu thông tin cơ bản của thành phần Điều hướng trong Compose, cách giúp AppBar (Thanh ứng dụng) phản hồi nhanh với thao tác điều hướng và cách gửi dữ liệu từ ứng dụng của bạn đến một ứng dụng khác bằng ý định (thể hiện các phương pháp hay nhất trong một ứng dụng ngày càng phức tạp).

## Techical Stack

- Android Jetpack Compose
- Android Navigation Component

Android Navigation Component có 3 phần chính:

- `NavController`: Chịu trách nhiệm điều hướng giữa các destination — tức là các màn hình trong ứng dụng của bạn.
- `NavGraph`: Maps composable destinations để điều hướng đến.
- `NavHost`: Hiển thị destination hiện tại của NavGraph.

Trong lớp học lập trình này, bạn sẽ tập trung vào NavController và NavHost. Trong NavHost, bạn sẽ xác định các đích đến cho NavGraph của ứng dụng.

Kiến thức bạn sẽ học được
- Tạo một thành phần kết hợp `NavHost` để xác định các tuyến và màn hình trong ứng dụng.
- Di chuyển giữa các màn hình bằng `NavHostController`.
- Thao tác với ngăn xếp lui để chuyển về các màn hình trước.
- Dùng ý định để chia sẻ dữ liệu với một ứng dụng khác.
- Tuỳ chỉnh AppBar, bao gồm tiêu đề và nút quay lại.

# Hướng dẫn từng bước

![Navigation](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-navigation/img/fde052dfa0a1f56a.png "Navigation")

## Xác định các tuyến (routes) và tạo NavHostController



# Tổng kết

Đến đây là xong rồi đó bạn có thể thấy rằng nó thực sự đơn giản. Hãy thử và để lại bình luận nhé.

Chúc bạn thành công!

-----
Tham khảo
- [Android Jetpack Compose - Navigation Component part 1](https://viblo.asia/p/android-jetpack-compose-navigation-component-part-1-3RlL53m24bB)
- [Navigation in Jetpack Compose](https://developer.android.com/courses/pathways/android-basics-compose-unit-4-pathway-2)
- [Codelabs - Navigate between screens with Compose](https://developer.android.com/codelabs/basic-android-kotlin-compose-navigation)
- [https://github.com/google-developer-training/basic-android-kotlin-compose-training-cupcake](https://github.com/google-developer-training/basic-android-kotlin-compose-training-cupcake)

- [Effortless Navigation with Compose](https://blog.stackademic.com/effortless-navigation-with-compose-30d37ddf5625)
- [Navigation Basics in Jetpack Compose](https://youtu.be/glyqjzkc4fk)
- [Full Guide to Nested Navigation Graphs in Jetpack Compose](https://youtu.be/FIEnIBq7Ups)
- [Migrate Jetpack Navigation to Navigation Compose](https://developer.android.com/jetpack/compose/migrate/migration-scenarios/navigation)
