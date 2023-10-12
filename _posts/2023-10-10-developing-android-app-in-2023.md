---
layout: post
title: Phát triển ứng dụng Android năm 2023
subtitle: Developing Android App in 2023
description: Các phương pháp hay nhất và đề xuất phổ biến và mới nhất mà mọi nhà phát triển Android nên biết vào năm 2023
author: "Juraj Kušnier"
image: "img/android.jpg"
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
- [Jetpack Compose](#jetpack-compose)
- [Kotlin Coroutines](#kotlin-coroutines)
- [Asynchronous Flow](#asynchronous-flow)
- [App Architecture](#app-architecture)
- [Material Design](#material-design)
- [User Experience](#user-experience)
- [Example App](#example-app)
- [Tổng kết](#tổng-kết)



![Android](https://boxxv.github.io/img/2023/android-14-h.jpeg "Android")

Trong bài viết ngắn này, tôi tóm tắt một số đề xuất cũng như thực tiễn tốt nhất và phổ biến mới dành cho nhà phát triển ứng dụng Android. Hãy thoải mái sử dụng chúng khi bạn xây dựng một dự án greenfield mới hoặc khi bạn muốn loại bỏ giao diện cũ khỏi các ứng dụng hiện có của mình.

# Java đã chết, Kotlin trường tồn

Nếu bạn thực sự không biết thì đã vài năm trôi qua kể từ khi Google [thông báo](https://developer.android.com/kotlin/first) rằng việc phát triển Android sẽ ưu tiên Kotlin lên hàng đầu. Kotlin không chỉ an toàn hơn, được thiết kế tốt hơn và ít dài dòng hơn Java mà không có Kotlin trong cơ sở mã của bạn, bạn sẽ không thể sử dụng các công cụ và thư viện hiện đại như Jetpack Compose hoặc lập trình không đồng bộ bằng Coroutines.

# Jetpack Compose

[Jetpack Compose](https://developer.android.com/jetpack/compose) là bộ công cụ hiện đại được Android khuyên dùng để xây dựng giao diện người dùng gốc. Nó đủ trưởng thành và cho phép bạn xây dựng giao diện người dùng dễ dàng hơn, nhanh hơn và ít mã hơn. Hơn nữa, bố cục XML dựa trên Soạn thảo và Chế độ xem có thể được kết hợp. Bạn có thể thêm giao diện người dùng Compose vào một ứng dụng hiện có sử dụng thiết kế dựa trên Chế độ xem hoặc bao gồm hệ phân cấp Chế độ xem Android trong giao diện người dùng Compose. Cách tiếp cận này đặc biệt hữu ích nếu bạn muốn sử dụng các thành phần giao diện người dùng chưa có trong Compose, như AdView hoặc MediaPlayer. Khi bạn bắt đầu một dự án mới, không có lý do gì để sử dụng bố cục XML nữa.

# Kotlin Coroutines

Lập trình không đồng bộ hoặc không chặn là một phần quan trọng trong quá trình phát triển Android. Bạn phải xử lý những vấn đề không đồng bộ mỗi khi bạn muốn thực hiện các thao tác I/O hoặc các phép tính mở rộng. Kotlin giải quyết vấn đề này một cách linh hoạt bằng cách cung cấp [hỗ trợ coroutine](https://kotlinlang.org/docs/coroutines-overview.html) ở cấp độ ngôn ngữ và ủy quyền hầu hết chức năng cho các thư viện. Không cần phải tự mình triển khai logic luồng hoặc khởi động AsyncTask nữa. Nếu bạn tìm thấy một hướng dẫn sử dụng những thứ như vậy, hãy chắc chắn rằng nó rất cũ.

# Asynchronous Flow

Luồng không đồng bộ không có gì mới. Bạn có thể quen thuộc với các thư viện như RxJava/RxAndroid triển khai lập trình không đồng bộ với các luồng có thể quan sát được. Tuy nhiên, API này quá phức tạp đối với hầu hết các trường hợp sử dụng và quá trình học tập rất khó khăn. Tôi đã trải nghiệm các dự án trong đó các luồng Rx được liên kết theo cách phức tạp đến mức việc thực hiện các thay đổi đơn giản chỉ mất vài ngày thay vì vài phút. May mắn thay, chúng tôi đã có [Kotlin Flow](https://kotlinlang.org/docs/flow.html), một thư viện luồng không đồng bộ mới của JetBrains, công ty phát triển ngôn ngữ Kotlin. Có nhiều điểm tương đồng với luồng Rx, Kotlin Flow được xây dựng dựa trên Kotlin Coroutines. Nó triển khai nhiều toán tử nổi tiếng mà bạn có thể biết từ thế giới Rx và đơn giản hóa việc làm việc với các luồng không đồng bộ. Hãy ngừng sử dụng RxJava và yêu thích Flow!

# App Architecture

Thiết kế kiến trúc ứng dụng là một yếu tố quan trọng cần cân nhắc để đảm bảo rằng ứng dụng của bạn mạnh mẽ, có thể kiểm thử và bảo trì. Google không phải lúc nào cũng quan tâm nhiều đến Kiến trúc ứng dụng. May mắn thay, điều này đã thay đổi và hiện chúng tôi đã có hướng dẫn chính thức về [cấu trúc ứng dụng](https://developer.android.com/topic/architecture). Hướng dẫn thảo luận về các khái niệm như phân tách mối quan tâm, các lớp ứng dụng khác nhau, mô-đun hóa hoặc chèn phần phụ thuộc. Đọc toàn bộ hướng dẫn trước khi viết một dòng mã!

# Material Design

Mã của bạn phải rõ ràng nhưng đối với Giao diện người dùng thì điều đó đúng gấp đôi vì nó hiển thị cho người dùng. Không dễ để thiết kế một ứng dụng vừa đẹp vừa có chức năng. May mắn thay, chúng tôi có [Material Design](https://m3.material.io), một hệ thống thiết kế được xây dựng và hỗ trợ bởi các nhà thiết kế và nhà phát triển của Google. Material Design cung cấp rất nhiều thành phần, bố cục, hoạt ảnh và biểu tượng sẵn sàng để sử dụng hoặc tùy chỉnh theo nhu cầu của bạn. Người dùng đã quen thuộc với các thành phần như Nút hành động nổi hoặc Ngăn điều hướng, không có lý do gì để phát minh ra những cách khác nhau để thực hiện những việc tương tự. Ngoài ra, đừng quên nói với nhóm thiết kế của bạn rằng Ứng dụng Android không nên trông giống bản sao pixel hoàn hảo của ứng dụng iOS!

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

# Tổng kết

Cảm ơn bạn đã đọc. Nếu bạn thích bài viết này, hãy thích, để lại phản hồi và chia sẻ nó với bạn bè của bạn. Happy coding - Lập trình vui vẻ!

-----
Tham khảo
- [Developing Android App in 2023](https://medium.com/@jurajkunier/developing-android-app-in-2023-60504dd76e38)