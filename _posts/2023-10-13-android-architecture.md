---
layout: post
title: Android Architecture
subtitle: Xây dựng một ứng dụng có thể mở rộng, được mô-đun hóa và có thể thử nghiệm ngay từ đầu
description: Building a scalable, modularized, testable app from scratch
author: "Google Developers Training team"
image: "img/2023/android-tips-for-working-with-preview-in-jetpack-compose.png"
tags:
- Android
- Kotlin
- Jetpack
- Architecture
- Compose
- Material Design
- Navigation
---

# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
  - [Model View View Model - MVVM](#model-view-view-model---mvvm)
  - [Tách biệt các mối lo ngại](#tách-biệt-các-mối-lo-ngại)
  - [Một nguồn dữ liệu đáng tin cậy duy nhất](#một-nguồn-dữ-liệu-đáng-tin-cậy-duy-nhất)
  - [Luồng dữ liệu một chiều](#luồng-dữ-liệu-một-chiều)
- [Cấu trúc ứng dụng được đề xuất](#cấu-trúc-ứng-dụng-được-đề-xuất)
- [Sử dụng Hilt trong Ứng dụng Android](#sử-dụng-hilt-trong-ứng-dụng-android)
  - [Chèn phần phụ thuộc](#chèn-phần-phụ-thuộc)
  - [Triển khai Hilt trong Retrofit](#triển-khai-hilt-trong-retrofit)
- [Tổng kết](#tổng-kết)

![Architecture](https://boxxv.github.io/img/2023/001.png "Architecture")

# Giới thiệu

Mã nguồn cơ bản cho Android hiện đại đang hướng tới reactive. Với các khái niệm và mô hình như MVI, Redux, hay Unidirectional Data Flow, rất nhiều components của hệ thống được mô hình hóa như các streams.

Các sự kiện UI cũng có thể được mô hình hóa thành các streams là các inputs từ hệ thống.

## Model View View Model - MVVM

Đầu tiên tôi xin nhắc lại Coinserve sử dụng mô hình MVVM. MVVM phân tách UI với business logic, tăng cường khả năng đọc hiểu và tổ chức. Tuy nhiên, vì một ứng dụng phát triển với MVVM nên nó sẽ trở thành một hồ dữ liệu. Thông tin các luồng in/out và xoay quanh tại rất nhiều điểm thông qua các activities và fragments với Data Binding, ViewModels, và Repositories. Điều này làm tăng độ phức tạp, rắc rối cho quá trình theo dõi logic, debugging, testing và đòi hỏi phải giả lập rất nhiều các components.

## Tách biệt các mối lo ngại

Nguyên tắc quan trọng nhất cần tuân thủ là [tách biệt các mối lo ngại](https://en.wikipedia.org/wiki/Separation_of_concerns). Có một lỗi thường gặp là viết tất cả mã trong Activity hoặc Fragment. Các lớp dựa trên giao diện người dùng này chỉ nên chứa logic xử lý các tương tác với giao diện người dùng và hệ điều hành. Bằng cách giữ các lớp này tinh gọn nhất có thể, bạn có thể tránh nhiều vấn đề liên quan đến vòng đời của thành phần và cải thiện khả năng kiểm thử của các lớp này.

## Một nguồn dữ liệu đáng tin cậy duy nhất

Khi xác định một loại dữ liệu mới trong ứng dụng, bạn nên chỉ định một Nguồn chính xác duy nhất (SSOT) cho nó. SSOT là chủ sở hữu của dữ liệu đó, và chỉ SSOT mới có thể sửa đổi hoặc thay đổi dữ liệu đó. Để đạt được điều này, SSOT hiển thị dữ liệu bằng cách sử dụng một kiểu bất biến, và để có thể sửa đổi dữ liệu, SSOT sẽ hiển thị các hàm hoặc nhận các sự kiện mà loại khác có thể gọi.

## Luồng dữ liệu một chiều

`Nguyên tắc về nguồn đáng tin duy nhất` thường dùng trong hướng dẫn của chúng tôi với mẫu `Luồng dữ liệu một chiều` (**UDF**). Trong `UDF`, trạng thái chỉ chạy theo một hướng. Các sự kiện sửa đổi luồng dữ liệu theo hướng ngược lại.

Mô hình UDF còn gọi là Unidirectional Data or State Flow ban đầu được phổ biến trong phát triển ứng dụng web của Facebook như quản lý trạng thái React và Readux, và các thư viện Flux UI.

# Cấu trúc ứng dụng được đề xuất

Hãy xem xét các nguyên tắc cấu trúc phổ biến đã đề cập trong phần trước, mỗi ứng dụng phải có ít nhất hai lớp:

- Lớp giao diện người dùng hiển thị dữ liệu ứng dụng trên màn hình.
- Lớp dữ liệu chứa logic nghiệp vụ của ứng dụng và hiển thị dữ liệu ứng dụng.

![Architecture](https://boxxv.github.io/img/2023/mad-arch-overview.png "Architecture")

**UI layer - Lớp giao diện người dùng**

Vai trò của lớp giao diện người dùng (hoặc lớp bản trình bày) là hiển thị dữ liệu ứng dụng trên màn hình. Bất cứ khi nào dữ liệu thay đổi, do sự tương tác của người dùng (chẳng hạn như nhấn một nút) hoặc đầu vào bên ngoài (chẳng hạn như phản hồi mạng), giao diện người dùng sẽ cập nhật để phản ánh các thay đổi đó.

- `UI elements`: Các thành phần trên giao diện người dùng hiển thị dữ liệu trên màn hình. Bạn tạo các phần tử này bằng cách sử dụng các hàm View (Thành phần hiển thị) hoặc Jetpack Compose.
- `State holders`: (chẳng hạn như các lớp `ViewModel`) chứa dữ liệu, hiển thị thông tin đó tới giao diện người dùng và xử lý logic.

> [UI layer page](https://developer.android.com/jetpack/guide/ui-layer?hl=vi)

**Data layer - Lớp dữ liệu**

Lớp dữ liệu của ứng dụng chứa _logic nghiệp vụ_ (business logic). Logic nghiệp vụ là yếu tố tạo ra giá trị cho ứng dụng — logic này được tạo ra từ các quy tắc xác định cách ứng dụng tạo, lưu trữ và thay đổi dữ liệu.

Các lớp trong lớp dữ liệu thường hiển thị các hàm để thực hiện lệnh gọi một lần: Tạo, Đọc, Cập nhật và Xóa (`CRUD`) hoặc để được thông báo về sự thay đổi dữ liệu theo thời gian. Lớp dữ liệu phải hiển thị những nội dung sau cho từng trường hợp sau:

- **Thao tác một lần**: Lớp dữ liệu cần hiển thị các hàm tạm ngưng trong Kotlin; và đối với ngôn ngữ lập trình Java, lớp dữ liệu cần hiển thị các hàm cung cấp lệnh gọi lại để thông báo kết quả của thao tác hoặc các loại RxJava `Single`, `Maybe` hoặc `Completable`.
- **Để nhận thông báo về các thay đổi của dữ liệu theo thời gian**: Lớp dữ liệu cần hiển thị [các luồng](https://developer.android.com/kotlin/flow?hl=vi) trong Kotlin; và đối với ngôn ngữ lập trình Java, lớp dữ liệu cần hiển thị một lệnh gọi lại phát ra dữ liệu mới hoặc loại RxJava `Observable` hoặc `Flowable`.

**Quy ước đặt tên trong hướng dẫn này**

Trong hướng dẫn này, các lớp kho lưu trữ được đặt tên theo dữ liệu mà chúng chịu trách nhiệm. Quy ước như sau:

> type of data + Repository.

Ví dụ: `NewsRepository`, `MoviesRepository` hoặc `PaymentsRepository`.

Các lớp nguồn dữ liệu được đặt tên theo dữ liệu mà các lớp này chịu trách nhiệm và nguồn mà chúng sử dụng. Quy ước như sau:

> type of data + type of source + DataSource.

Đối với loại dữ liệu, hãy sử dụng Điều khiển từ xa hoặc Địa phương chung hơn vì cách triển khai có thể thay đổi. Ví dụ: `NewsRemoteDataSource` hoặc `NewsLocalDataSource`. Để cụ thể hơn trong trường hợp nguồn là quan trọng, hãy sử dụng loại nguồn. Ví dụ: `NewsNetworkDataSource` hoặc `NewsDiskDataSource`.

Không đặt tên nguồn dữ liệu dựa trên thông tin triển khai—ví dụ: `UserSharedPreferencesDataSource` — vì các kho lưu trữ mà sử dụng nguồn dữ liệu đó sẽ không biết cách lưu dữ liệu. Nếu tuân theo quy tắc này, bạn có thể thay đổi cách triển khai nguồn dữ liệu (ví dụ: di chuyển từ SharedPreferences tới DataStore ) mà không ảnh hưởng đến lớp gọi nguồn đó.

**Nhiều cấp độ của các kho lưu trữ**

Trong một số trường hợp liên quan đến các yêu cầu kinh doanh phức tạp hơn, một kho lưu trữ có thể cần phải phụ thuộc vào những kho lưu trữ khác. Điều này có thể là do dữ liệu liên quan là tổng hợp từ nhiều nguồn dữ liệu hoặc do trách nhiệm cần được đóng gói trong một lớp kho lưu trữ khác.

Ví dụ: một kho lưu trữ xử lý dữ liệu xác thực người dùng, `UserRepository`, có thể phụ thuộc vào các kho lưu trữ khác như `LoginRepository` và `RegistrationRepository` để đáp ứng các yêu cầu của kho lưu trữ đó.

![Architecture](https://boxxv.github.io/img/2023/mad-arch-data-multiple-repos.png "Architecture")

> [Data layer page](https://developer.android.com/jetpack/guide/data-layer?hl=vi)

**Quản lý các phần phụ thuộc giữa các thành phần**

Các lớp trong ứng dụng phụ thuộc vào các lớp khác để có thể hoạt động đúng cách. Bạn có thể sử dụng một trong các mẫu thiết kế sau để thu thập các phần phụ thuộc của một lớp cụ thể:

- [Chèn phần phụ thuộc (DI)](https://developer.android.com/training/dependency-injection?hl=vi): Chèn phần phụ thuộc cho phép các lớp xác định các phần phụ thuộc mà không cần tạo chúng Trong thời gian chạy, một lớp khác chịu trách nhiệm cung cấp các phần phụ thuộc này.
- [Công cụ định vị dịch vụ](https://en.wikipedia.org/wiki/Service_locator_pattern): Mẫu bộ định vị dịch vụ cung cấp một sổ đăng ký mà các lớp có thể lấy phần phụ thuộc thay vì tạo các phần phụ thuộc đó.

Các mẫu này cho phép bạn mở rộng mã vì chúng cung cấp các mẫu rõ ràng để quản lý các phần phụ thuộc mà không cần sao chép mã hoặc thêm độ phức tạp. Hơn nữa, các mẫu này cho phép bạn nhanh chóng chuyển đổi giữa triển khai bản chính thức và kiểm thử.

**Bạn nên làm theo các mẫu chèn phụ thuộc và sử dụng [thư viện Hilt](https://developer.android.com/training/dependency-injection/hilt-android?hl=vi) trong các ứng dụng Android.**

Hilt tự động tạo các đối tượng thông qua cây phần phụ thuộc, đưa ra sự đảm bảo về thời gian biên dịch các phần phụ thuộc và tạo vùng chứa phần phụ thuộc cho các lớp thuộc khung Android.


# Sử dụng Hilt trong Ứng dụng Android

[Hilt](https://developer.android.com/training/dependency-injection/hilt-android?hl=vi) là thư viện đề xuất của Jetpack dùng để chèn phần phụ thuộc trong Android. Hilt xác định một phương pháp chuẩn để thực hiện DI trong ứng dụng của bạn, bằng cách cung cấp các vùng chứa cho mọi lớp Android trong dự án, đồng thời tự động quản lý vòng đời của các vùng chứa đó cho bạn.

Hilt được xây dựng dựa trên thư viện DI phổ biến là [Dagger](https://developer.android.com/training/dependency-injection/dagger-basics?hl=vi) để hưởng lợi từ độ chính xác của thời gian biên dịch, hiệu suất trong thời gian chạy, khả năng có thể mở rộng và Hỗ trợ Android Studio mà Dagger cung cấp.

## Chèn phần phụ thuộc

Cấu trúc ứng dụng đề xuất của Android khuyến khích việc chia mã thành các lớp để hưởng lợi từ việc tách biệt các vấn đề, một nguyên tắc mà mỗi lớp trong hệ phân cấp chỉ có một trách nhiệm xác định. Điều này dẫn đến việc nhiều lớp nhỏ hơn cần được kết nối với nhau để thực hiện các phần phụ thuộc của nhau.

![Architecture](https://boxxv.github.io/img/2023/final-architecture.png "Architecture")

## Triển khai Hilt trong Retrofit

**Project Structure**

![Architecture](https://boxxv.github.io/img/2023/1bzauaaaepvkr9hk5w3c.png "Architecture")

**Bản tóm tắt về chú thích Hilt và Dagger**

![Architecture](https://boxxv.github.io/img/2023/hilt-cheatsheet.png "Architecture")


# Tổng kết

Đến đây là xong rồi đó bạn có thể thấy rằng nó thực sự đơn giản. Hãy thử và để lại bình luận nhé.

Chúc bạn thành công!

-----
Tham khảo
- [Hướng dẫn về cấu trúc ứng dụng](https://developer.android.com/topic/architecture?hl=vi)
- [UI layer - Lớp giao diện người dùng](https://developer.android.com/jetpack/guide/ui-layer?hl=vi)
- [Chèn phần phụ thuộc trong Android](https://developer.android.com/training/dependency-injection?hl=vi)
- [Chèn phần phụ thuộc bằng Hilt](https://developer.android.com/training/dependency-injection/hilt-android?hl=vi)
- [Implementation of Hilt in Retrofit](https://dev.to/krisrajkumar/implementation-of-hilt-in-retrofit-154f)

- [Tổng quan về Hilt trong loạt bài kỹ năng Modern Android Development (MAD)](https://viblo.asia/p/tong-quan-ve-hilt-trong-loat-bai-ky-nang-modern-android-development-mad-Do754zeQZM6)
- [What's new in Jetpack?](https://viblo.asia/p/whats-new-in-jetpack-maGK76yL5j2)
- [What’s new in Jetpack](https://viblo.asia/p/whats-new-in-jetpack-Ljy5VqXblra)

- [Android Unidirectional Data Flow with LiveData](https://viblo.asia/p/android-unidirectional-data-flow-with-livedata-vyDZO767Zwj)
- [Binding Android UI with Kotlin Flow](https://viblo.asia/p/binding-android-ui-with-kotlin-flow-eW65GWyY5DO)
- [25 thư viện và project sample Android hay nhất năm 2020](https://viblo.asia/p/25-thu-vien-va-project-sample-android-hay-nhat-nam-2020-1Je5Ey015nL)

