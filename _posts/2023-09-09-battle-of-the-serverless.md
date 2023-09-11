---
layout: post
title: Serverless - Rust, Go, Kotlin, Scala và F#
subtitle: Rust vs Go vs Kotlin vs F# vs C#
author: "TAn"
image: "img/techskills.jpg"
tags:
- Java
- JavaScript
- C
- C#
- C++
- PHP
- Ruby
- Perl
- Swift
- R
- Python
- Scala
- TypeScript
- Kotlin
- Go
- VisualBasic.NET
- Objective-C
- VBScript
- Google Apps Script
- Haskell
- Groovy
- Delphi
- Dart
- D
- COBOL
- SQL
- FORTRAN
- MATLAB
- Scratch
---

# Mục lục

- [Mục lục](#mục-lục)
  - [Serverless](#serverless)
    - [Ưu điểm của serverless](#ưu-điểm-của-serverless)
    - [Nhược điểm của serverless](#nhược-điểm-của-serverless)
    - [Khi nào nên sử dụng serverless](#khi-nào-nên-sử-dụng-serverless)
  - [1. Rust](#1-rust)
    - [Ưu điểm của Rust:](#ưu-điểm-của-rust)
    - [Nhược điểm của Rust:](#nhược-điểm-của-rust)
    - [Giải pháp:](#giải-pháp)
    - [Công cụ phổ biến:](#công-cụ-phổ-biến)
  - [2. Go](#2-go)
    - [Ưu điểm của Go](#ưu-điểm-của-go)
    - [Nhược điểm của Go](#nhược-điểm-của-go)
    - [Giải pháp](#giải-pháp-1)
    - [Công cụ phổ biến](#công-cụ-phổ-biến-1)
  - [3. Kotlin](#3-kotlin)
  - [4. Scala](#4-scala)
  - [5. F#](#5-f)
- [Tổng kết](#tổng-kết)


![Serverless Architecture](https://boxxv.github.io/img/2023/9a0fb8a5-8c9f-4d03-9114-ed7658f2e4f9.webp "Serverless Architecture")

Serverless là môi trường, nền tảng thực thi ứng dụng và dịch vụ mà không phải quan tâm đến máy chủ. Ứng dụng serverless không cần phải  quan tâm việc phân bổ, quản lý tài nguyên của hệ điều hành, và bỏ qua các vấn đề về nâng cấp và bảo mật. Với khái niệm là chỉ cần tập trung phát triển sản phẩm, việc còn lại về vận hành sẽ để nền tảng này đảm nhiệm.

Điều quan trọng và khác biệt nhất trong serverless là bạn chỉ trả tiền khi và chỉ những phần bạn sử dụng. Giả sử bạn có một máy chủ ảo, thì thường sẽ được tính tiền trọn gói bao gồm thời gian chạy 24/7 trong 1 tháng, CPU và RAM, băng thông, lưu trữ. Bạn vẫn sẽ phải trả tiền hàng tháng đều đặn cho dù cái máy chủ ảo đó không chạy, hoặc chỉ sử dụng 5~10% công suất thì bạn vẫn phải trả trọn gói. Hiểu một cách nôm na, thì serverless như gói cước điện thoại được tính theo block giây, gọi bao nhiêu tính tiền bấy nhiêu, còn máy chủ ảo thường thì phải trả tiền thuê bao hàng tháng dù có phải sử dụng hay không.

## Serverless

### Ưu điểm của serverless

Xây dụng ứng dụng serverless đồng nghĩa với việc bạn chỉ tập trung vào sản phẩm cốt lõi thay vì phải lo lắng về việc quản lý và vận hành nhiều máy chủ hoặc thời gian chạy, dù trên nền tảng đám mây hay tự xây dựng hệ thống máy chủ. Sự cắt giảm công sức tổng thể này sẽ giúp cho các nhà phát triển dành thời gian và năng lượng để tập trung vào việc xây dựng các sản phẩm tuyệt vời có quy mô linh hoạt và ổn định cao.

- Không cần quản lý máy chủ: Bạn sẽ không cần cung cấp hay duy trì bất kỳ máy chủ nào. Sẽ không cần phần mềm hoặc thời gian chạy để cài đặt, nâng cấp hoặc quản trị.
- Thay đổi quy mô một cách linh hoạt: Ứng dụng của bạn sẽ có khả năng thay đổi quy mô tự động hoặc bằng cách điều chỉnh dung lượng thông qua việc chuyển đổi đơn vị sử dụng (ví dụ: thông lượng, bộ nhớ) thay vì với máy chủ độc lập thì sẽ phức tạp hơn.
- Độ sẵn sàng cao: Ứng dụng serverless có độ sẵn sàng tích hợp và dung sai cao. Bạn sẽ không cần tạo kiến trúc cho các khả năng này do các dịch vụ chạy ứng dụng đã cung cấp cho ứng dụng theo mặc định. Ngoài ra, có để chọn trung tâm dữ liệu (một hoặc nhiều nơi) để triển khai sản phẩm một cách dễ dàng.
- Tiết kiệm chi phí: chi phí gần như bằng 0 sau khi triển khai nếu bạn không có request nào (hoặc không có hành động gọi hàm), còn sử dụng bao nhiêu thì tính tiền bấy nhiêu.

### Nhược điểm của serverless

Serverless là một ý tưởng tuyệt vời nhưng không hoàn hảo, serverless có những vấn đề riêng mà bạn cũng phải suy nghĩ trước khi quyết định sử dụng:

- Độ trễ: Hiệu suất có thể là một vấn đề, chính bản thân mô hình này có thể gây ra độ trễ lớn hơn trong quá trình các nguồn tài nguyên điện toán phản ứng lại với lệnh của các ứng dụng. Nếu khách hàng yêu cầu hiệu suất cao thì việc sử dụng các máy chủ ảo được phân bổ sẽ là một lựa chọn ưu việt hơn.
- Gỡ lỗi (Debug): Công việc giám sát và gỡ lỗi của serverless computing cũng khá khó khăn. Việc bạn không sử dụng một nguồn tài nguyên máy chủ thống nhất làm cho cả hai hoạt động này gặp nhiều trở ngại. (Tin tốt là công cụ này sẽ dần được để cải thiện xử lý giám sát và gỡ lỗi tốt hơn trong môi trường không máy chủ.)
- Giới hạn về bộ nhớ, thời gian: các nhà cung cấp đều giới hạn tài nguyên ở các mức cố định về bộ nhớ và thời gian thực thi (timeout). Giả sử timeout tối đa là 5 phút, nếu bạn chạy quá 5 phút, quá trình thực thi sẽ bị ngắt. Về bộ nhớ, thì sẽ thiết lập mỗi mức khác nhau tuỳ nhà cung cấp, AWS có memory là 3008MB (sẽ được cấp CPU cao tương ứng), nếu ứng dụng yêu cầu bộ nhớ lớn thì sẽ không đáp ứng được. Liên quan đến vấn đề bộ nhớ này, thì cũng cần phải lưu tâm lúc lập trình nên tối ưu tốt, để tiết kiệm chi phí.
- Phụ thuộc nhà cung cấp: bạn không thể muốn chạy phiên bản của phần mềm, nền tảng chính xác như bạn muốn. Ví dụ Nodejs bạn cần 10.x nhưng nhà cung cấp chỉ hỗ trợ đến 8.x, thì bạn sẽ không sử dụng được nền tảng này. Như vậy, trước khi sử dụng, bạn cần cân nhắc các nền tảng được hỗ trợ.
- Chi phí ngầm: tuỳ nhà cung cấp có tính hay không, nhưng cơ bản là sẽ phát sinh chi phí lưu trữ mã nguồn, băng thông, và chi phí về lưu trữ dữ liệu (tuỳ ứng dụng có sử dụng hay không, ví dụ DynamoDB, RDMS … thì sẽ được tính riêng). Mặc dù, tuy không nhiều nhưng nếu không tối ưu, các phần chi phí ngầm sẽ còn cao hơn cả chi phí cho serverless.
- Thời gian để nghiên cứu: trước đây bạn phải học cách sử dụng, quản lý máy chủ thì giờ đây bạn cũng cần thời gian để học để quản lý các tài nguyên trong serverless, mặc dù ko phải quá khó như quản lý máy chủ, nhưng không thể không tính. Ví dụ bạn sẽ mất thời gian để hiểu về cách sử dụng CloudFormation, IAM policies, quản lý cấu hình về stage, region, memory của Functions…

### Khi nào nên sử dụng serverless

Có rất nhiều trường hợp có thể ứng dụng được serverless, điểm chung là tất cả những ứng dụng không dính dáng đến điểm yếu của serverless 😀

- Websites và APIs: hoàn toàn có thể xây dựng 1 website hoặc API, website có thể là động hoặc là bán tĩnh (bán tĩnh nghĩa là nguồn gốc file là tĩnh, nhưng dùng route động). Thường thì người ta hay xây dựng Restful API với serverless, nhưng mình thích áp dụng cho Graphql hơn, vì Restful có thể trả về dữ liệu không dùng tới nhưng mình phải trả tiền băng thông 😀 (Xem thêm [Graphql là gì](https://fullstackstation.com/graphql-la-gi-ap-dung-nhu-the-nao/)).
- Xử lý đa phương tiện: các thao tác xử lý hình ảnh, video với yêu cầu không quá cao như cắt, nén, định dạng kích thước ảnh, tạo ảnh thumbnail, hoặc chuyển đổi bộ mã của video để phù hợp với thiết bị tương ứng.
- Xử lý sự kiện: có thể đóng vai trò như 1 công tắc cầu giao để thực hiện một loạt các hành động khác khi được kích hoạt tuỳ theo sự kiện.
- Xử lý dữ liệu: tuỳ theo ngữ cảnh mà có thể ứng dụng như chatbot, IoT,… lý do mà serverless thích hợp với mảng này vì với chatbot hay IoT chúng ta không biết khi nào dữ liệu sẽ tới, khi nào sẽ cần xử lý dữ liệu nên chúng ta không cần phải xây dựng máy chủ luôn luôn chạy và lãng phí ở thời gian chờ.

## 1. Rust

[Rust](https://www.rust-lang.org) là một ngôn ngữ lập trình mới được phát triển bởi Mozilla Research vào năm 2010. Nó chủ yếu tập trung vào việc xây dựng các hệ thống hiệu suất cao, an toàn và đáng tin cậy. Với cú pháp dễ đọc và mô hình sở hữu, Rust đảm bảo an toàn thông qua việc kiểm tra lỗi biên dịch và loại bỏ sự cố xảy ra trong thời gian chạy.

### Ưu điểm của Rust:
- Hiệu suất cao: Rust được tối ưu hóa để chạy nhanh và sử dụng tài nguyên hiệu quả.
- An toàn: Rust loại bỏ các lỗi thông thường như trỏ hoang (null pointer) và đa luồng không an toàn.
- Bảo mật: Rust bảo vệ chương trình khỏi các lỗ hổng bảo mật thông thường như tràn bộ nhớ (buffer overflow).
- Dễ học: Với cú pháp gần gũi, Rust dễ tiếp cận cho người mới học.

### Nhược điểm của Rust:
- Tốn thời gian học tập: Với mô hình sở hữu và kiểm tra lỗi biên dịch khắt khe, Rust có thể tốn thời gian cho người mới học.
- Khó sử dụng cho dự án lớn: Rust có hạn chế trong việc phát triển các dự án lớn và phức tạp do phong cách viết mã và hạn chế của hệ thống ghi nhớ mượt mà.

### Giải pháp:
- Rust đang tiếp tục phát triển và cộng đồng đang hoạt động tích cực để cải thiện tài liệu và cung cấp các tài nguyên học tập tốt hơn cho người mới. Sử dụng các tài liệu và tài nguyên từ cộng đồng có thể giúp hạn chế khó khăn khi học Rust.
- Đối với các dự án lớn, việc sử dụng các công cụ và framework hỗ trợ, cũng như phân chia dự án thành các module có thể giúp quản lý mã nguồn hiệu quả hơn.

### Công cụ phổ biến:
- `rustc`: Đây là trình biên dịch chính của Rust. Nó có các cờ tùy chỉnh để cấu hình mã nguồn và hiệu suất.
- `Cargo`: Cargo là trình quản lý gói và công cụ xây dựng dựa trên Rust. Nó giúp bạn tự động hóa quy trình biên dịch và tối ưu hóa mã nguồn.

Ví dụ minh họa: Chúng ta sẽ viết một chương trình tính tổng của một dãy số từ 1 đến N.

{% highlight js %}
fn main() {
    let n = 10;
    let sum: i32 = (1..=n).sum();
    println("Tổng từ 1 đến {}: {}", n, sum);
}
{% endhighlight %}

## 2. Go

[Go](https://go.dev), thường được gọi là Golang, là một ngôn ngữ lập trình mã nguồn mở do Google phát triển từ năm 2007 và ra mắt chính thức vào năm 2012. Go được thiết kế để đơn giản hóa quy trình lập trình và cải thiện hiệu suất của các ứng dụng phần mềm. Nó được sử dụng rộng rãi trong phát triển web, các ứng dụng phân tán, và dịch vụ cloud.

### Ưu điểm của Go

- Hiệu suất cao: Go chạy rất nhanh và sử dụng tài nguyên hiệu quả.
- Đơn giản: Go có cú pháp đơn giản và dễ đọc, giúp lập trình viên tập trung vào việc viết mã chất lượng cao.
- Đáng tin cậy: Go được thiết kế để hạn chế các lỗi phổ biến và hỗ trợ xử lý đồng thời (concurrency) an toàn.
- Xử lý đồng thời mạnh mẽ: Go hỗ trợ xử lý hàng ngàn luồng (goroutines) một cách hiệu quả.

### Nhược điểm của Go

- Không hỗ trợ kỹ thuật lập trình hướng đối tượng đầy đủ: Go hạn chế việc kế thừa và không có tính chất đa hình đầy đủ, điều này có thể làm giảm sự sáng tạo trong thiết kế kiến trúc phần mềm phức tạp.
- Có một số hạn chế trong việc xử lý đồng thời: Mặc dù Go hỗ trợ xử lý đồng thời thông qua goroutines, nhưng thiếu một số tính năng quan trọng như coroutine hay async/await giống như trong các ngôn ngữ khác.

### Giải pháp

- Đối với việc hỗ trợ hướng đối tượng, Go khuyến khích sử dụng kiểu dữ liệu cấu trúc (struct) và giao diện (interface) để đạt được các mục tiêu thiết kế phần mềm tương tự.
- Để xử lý đồng thời hiệu quả, lập trình viên có thể sử dụng các cơ chế quản lý goroutines và channels của Go. Đồng thời, cộng đồng cũng đang phát triển các thư viện và framework hỗ trợ xử lý đồng thời phức tạp hơn cho Go.

### Công cụ phổ biến

- `go build`: Trình biên dịch chính của Go có thể được sử dụng để biên dịch chương trình và tối ưu hóa mã nguồn.
- `go fmt`: Công cụ này định dạng mã nguồn Go theo quy tắc định sẵn, giúp mã trở nên dễ đọc và nhất quán.

Ví dụ minh họa:


## 3. Kotlin

Loại ngôn ngữ này coi chương trình là một nhóm đối tượng bao gồm dữ liệu và các phần tử chương trình, được gọi là thuộc tính và phương thức. Các đối tượng có thể được tái sử dụng trong một chương trình hoặc trong các chương trình khác. Điều này làm cho nó trở thành loại ngôn ngữ phổ biến cho các chương trình phức tạp, vì mã dễ sử dụng lại và mở rộng quy mô hơn. Một số ngôn ngữ lập trình hướng đối tượng (OOP) phổ biến bao gồm:

## 4. Scala

Các lập trình viên sử dụng ngôn ngữ kịch bản để tự động hóa các tác vụ lặp đi lặp lại, quản lý nội dung web động hoặc hỗ trợ các quy trình trong các ứng dụng lớn hơn. Một số ngôn ngữ kịch bản phổ biến bao gồm:

## 5. F#

Thay vì ra lệnh cho máy tính phải làm gì, ngôn ngữ lập trình logic thể hiện một loạt các sự kiện và quy tắc để hướng dẫn máy tính cách đưa ra quyết định. Một số ví dụ về ngôn ngữ logic bao gồm:

# Tổng kết

-----
Tham khảo:
- [Khám phá những ngôn ngữ lập trình: Rust, Go, Kotlin, Scala và F#](https://viblo.asia/p/kham-pha-nhung-ngon-ngu-lap-trinh-rust-go-kotlin-scala-va-f-38X4EPlzVN2)
- [Serverless là gì? Hãy sẵn sàng với serverless!](https://fullstackstation.com/serverless-la-gi/)
- [5 Types of Programming Languages](https://www.coursera.org/articles/types-programming-language)
- [Programming Languages to Avoid and Learn in 2022.](https://zriyansh.medium.com/programming-languages-to-avoid-and-learn-in-2022-c8e2a1cdf427)