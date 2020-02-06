---
layout: post
title: Logging trong C#
subtitle: Thực tiễn hiện đại, Hướng dẫn đầy đủ
tags:
- Csharp
- Comment
- Commenting Convention
- Coding Conventions
modified: 2019-05-13
---

Ghi Log là một phần quan trọng của phát triển phần mềm trong nhiều năm nay. Người ta có thể lập luận rằng một cơ chế ghi Log là một phần bắt buộc phải có của bất kỳ ứng dụng hoặc thư viện nào.  

Ghi Log có một phần quan trọng để chơi trong kịch bản mà bạn có thể sử dụng gỡ lỗi tương tác (nghĩa là đính kèm trình gỡ lỗi như Visual Studio). Nó cho phép chúng tôi điều tra lỗi sau khi sự cố đã xảy ra. Trong một số trường hợp, như Gỡ lỗi sản phẩm, Log có thể là thông tin duy nhất bạn có.

Ngay cả khi bạn có thể gỡ lỗi quy trình của riêng mình, nhật ký có thể cung cấp cho bạn thông tin vô giá về các thành phần khác như thư viện của bên thứ 3, có sẵn trong framework .NET và CLR.

Bên cạnh việc ghi Log, một thuật ngữ mới đang trở nên phổ biến: Giám sát. Giám sát có nghĩa là có một công cụ tự động báo cáo thông tin về ứng dụng của bạn. Thông tin đó thường là lỗi (Giám sát lỗi Error, Giám sát sự cố Crash), nhưng cũng là thông tin về các yêu cầu và về hiệu suất (Giám sát hiệu suất). Điều này rất khác với việc ghi nhật ký nơi mã của bạn chủ động viết tin nhắn và ngoại lệ để ghi nhật ký. Chúng tôi sẽ nói về việc ghi Log ngày hôm nay.




Tham khảo:
- [Logging in C# .NET Modern-day Practices: The Complete Guide](https://michaelscodingspot.com/logging-in-dotnet/)
