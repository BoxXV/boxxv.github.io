---
layout: post
title: Lý do tôi chọn Serilog thay vì NLog trong dự án .NET Core 8
subtitle: Why I Chose Serilog Over NLog in My Dot Net Core 8 Project
date: 2026-02-10 10:11:12
tags:
- Serilog
- NLog
- Log
- Csharp
---

- [Các nơi có thể ghi Log - Logging Target Types](#các-nơi-có-thể-ghi-log---logging-target-types)
- [Tổng kết](#tổng-kết)


Trong thế giới phát triển .NET Core 8, việc ghi nhật ký không chỉ đơn thuần là cách để theo dõi hoạt động của ứng dụng; nó còn là một thành phần thiết yếu để gỡ lỗi, giám sát hiệu năng và đảm bảo độ tin cậy của ứng dụng. Với sự ra đời của .NET Core 8, các nhà phát triển có vô số framework ghi nhật ký để lựa chọn, nhưng hai cái tên nổi bật hơn cả là Serilog và NLog. Sau khi nghiên cứu và đánh giá kỹ lưỡng, tôi quyết định chọn Serilog thay vì NLog. Sau đây là lý do:


## Hiểu tầm quan trọng của việc ghi nhật ký trong .NET Core 8

.NET Core 8 mang đến những tính năng và cải tiến tiên tiến, khiến việc lựa chọn một framework ghi nhật ký trở nên quan trọng hơn bao giờ hết. Ghi nhật ký trong .NET Core 8 không chỉ đơn thuần là theo dõi lỗi; mà còn là tạo ra một bản tường thuật toàn diện về hoạt động của ứng dụng, điều không thể thiếu đối với việc quản lý vòng đời ứng dụng hiện đại.

## Ghi nhật ký có cấu trúc: Một bước đột phá

Ghi nhật ký có cấu trúc đã cách mạng hóa cách chúng ta nhìn nhận việc ghi nhật ký, chuyển từ nhật ký văn bản không có cấu trúc sang dữ liệu có cấu trúc, có thể truy vấn. Sự thay đổi này rất quan trọng trong các ứng dụng .NET Core 8, nơi độ phức tạp và quy mô của ứng dụng đòi hỏi nhiều hơn từ các framework ghi nhật ký. Serilog, được thiết kế với mục tiêu ghi nhật ký có cấu trúc, cho phép các nhà phát triển ghi nhật ký các loại dữ liệu phức tạp một cách dễ dàng, biến nhật ký không chỉ là thông báo mà còn là dữ liệu phong phú, có thể tìm kiếm. Khả năng tích hợp liền mạch ghi nhật ký có cấu trúc vào các ứng dụng .NET Core 8 của Serilog là một yếu tố then chốt trong quá trình ra quyết định của tôi.

Vì vậy, lý do chính đằng sau quyết định của tôi là khả năng hỗ trợ ghi nhật ký có cấu trúc vượt trội của Serilog. Không giống như ghi nhật ký truyền thống, vốn coi dữ liệu nhật ký là văn bản thuần túy, ghi nhật ký có cấu trúc coi các mục nhật ký là dữ liệu có cấu trúc, thường ở định dạng JSON. Cách tiếp cận này giúp đơn giản hóa đáng kể quá trình truy vấn và phân tích nhật ký, đặc biệt khi xử lý các hệ thống phức tạp hoặc phân tán.

## Phương pháp tiếp cận của Serilog

Serilog xử lý nhật ký như dữ liệu có cấu trúc, cho phép thu thập thông tin chi tiết sâu sắc và tích hợp dễ dàng với các công cụ giám sát hiện đại. Ví dụ, việc ghi nhật ký một đối tượng đơn giản như sau:

```csharp
_logger.Information("Order processed {@Order}", order);
```

Thao tác này ghi lại đối tượng `order` theo định dạng có cấu trúc, bảo toàn các thuộc tính của nó để dễ dàng truy vấn trong các công cụ như Elasticsearch hoặc Seq.


## Phương pháp tiếp cận của NLog

Mặc dù NLog có hỗ trợ ghi nhật ký có cấu trúc ở một mức độ nào đó, nhưng cảm giác như đây chỉ là một tính năng được thêm vào sau chứ không phải là một tính năng tích hợp sẵn. Việc ghi nhật ký truyền thống trong NLog trông như thế này:

```csharp
_logger.Info($"Order processed: {order.Id}, {order.Amount}");
```

Mặc dù có thể cấu trúc nhật ký theo cách thủ công, nhưng quy trình này không liền mạch hoặc trực quan như với Serilog.

## Hiệu năng và Tính linh hoạt

Hiệu năng là một yếu tố quan trọng khác trong quá trình ra quyết định của tôi. Cả Serilog và NLog đều cung cấp hiệu năng ấn tượng, nhưng chúng khác biệt đáng kể trong cách tiếp cận việc ghi nhật ký và cấu hình.

## Thông tin chi tiết về thử nghiệm hiệu năng: Serilog so với NLog

Tôi đã tiến hành các bài kiểm tra hiệu năng để so sánh hiệu năng của chúng, đặc biệt tập trung vào việc ghi nhật ký tệp và console trong .NET Core 8. Mặc dù NLog có lợi thế hơn một chút về tốc độ, nhưng hiệu năng của Serilog trong các ứng dụng .NET Core 8 rất mạnh mẽ và hiệu quả, đáp ứng được nhu cầu ghi nhật ký của tôi mà không ảnh hưởng đến khả năng phản hồi của ứng dụng.

![PSerilog so với NLog2](https://boxxv.github.io/img/2026/1_sw-Xt8OFCf9LHq6lIrBCkA.webp "Serilog so với NLog")


## Tích hợp liền mạch: Tại sao Serilog nổi bật

Khả năng tích hợp đóng vai trò quan trọng trong việc lựa chọn một framework ghi nhật ký cho .NET Core 8. Serilog vượt trội nhờ cấu hình đơn giản, đặc biệt là khi định nghĩa các sink (đầu ra cho nhật ký). API của nó trực quan, giúp dễ dàng thiết lập các kịch bản ghi nhật ký phức tạp. Mặt khác, NLog, mặc dù mạnh mẽ, nhưng lại có đường cong học tập dốc hơn do các tùy chọn cấu hình mở rộng của nó.

## Tích hợp với các công cụ giám sát

Dự án của tôi yêu cầu tích hợp liền mạch với Graylog để quản lý nhật ký tập trung. Hệ sinh thái của Serilog bao gồm một sink chuyên dụng cho Graylog, giúp quá trình tích hợp diễn ra suôn sẻ. Đây là một lợi thế đáng kể vì nhật ký có cấu trúc có thể được Graylog trực tiếp tiếp nhận ở định dạng GELF, nâng cao khả năng giám sát và phân tích của chúng tôi.

## Cộng đồng và tài liệu

Cả Serilog và NLog đều được hỗ trợ bởi các cộng đồng mạnh mẽ và tài liệu toàn diện. Tuy nhiên, tôi thấy tài liệu của Serilog dễ tiếp cận hơn, với nhiều ví dụ cho các tình huống phổ biến. Sự dễ dàng truy cập thông tin này đã chứng tỏ là vô cùng quý giá trong giai đoạn thiết lập ban đầu và khắc phục sự cố.


-----
## Tổng kết

Quyết định chọn Serilog không phải là một quyết định dễ dàng. Đó là kết quả của việc cân nhắc kỹ lưỡng các nhu cầu cụ thể của dự án, kiểm tra hiệu năng toàn diện và yêu cầu tích hợp liền mạch với các công cụ giám sát hiện đại. Khả năng ghi nhật ký có cấu trúc vượt trội, cấu hình dễ dàng và hệ sinh thái mạnh mẽ của Serilog đã biến nó thành lựa chọn lý tưởng cho dự án của chúng tôi. Mặc dù NLog là một lựa chọn đáng gờm với những điểm mạnh riêng, nhưng cách tiếp cận của Serilog phù hợp hơn với mục tiêu quản lý và phân tích nhật ký hiệu quả của chúng tôi.

Hãy kết thúc bằng câu nói không thể thiếu trong những bài đăng trên blog kiểu này:

Hãy nhớ rằng, lựa chọn tốt nhất cuối cùng phụ thuộc vào các yêu cầu và hạn chế cụ thể của dự án của bạn. Tôi đặc biệt khuyên bạn nên đánh giá cả hai lựa chọn trong bối cảnh nhu cầu của riêng mình để đưa ra quyết định sáng suốt.


-----
Tham khảo:
- [Why I Chose Serilog Over NLog in My Dot Net Core 8 Project](https://medium.com/@arttech/why-i-chose-serilog-over-nlog-in-my-dot-net-core-8-project-c0264bceaf49)
- [Logging in C# .NET Modern-day Practices: The Complete Guide](https://michaelscodingspot.com/logging-in-dotnet/)
- [Serilog, log4net and NLog Comparison: Logging Libraries for .NET Applications](https://www.bytehide.com/blog/serilog-log4net-nlog-comparison)
- [Serilog vs NLog](https://dev.to/thomasardal/serilog-vs-nlog-2ojf)
- [Serilog vs NLog](https://blog.elmah.io/serilog-vs-nlog/)
- [A Deep Dive into .NET Logging: Serilog, log4net, and NLog](https://www.c-sharpcorner.com/article/a-deep-dive-into-net-logging-serilog-log4net-and-nlog/)
- [Logging trong C#](https://boxxv.github.io/2020/03/13/c-sharp-logging/)

-----
Serilog:
- [https://github.com/serilog/serilog](https://github.com/serilog/serilog)
- [https://github.com/serilog/serilog-aspnetcore](https://github.com/serilog/serilog-aspnetcore)

-----
NLog:
- [NLog - Tutorial](https://github.com/NLog/NLog/wiki/Tutorial)
- [NLog - Configuration file](https://github.com/NLog/NLog/wiki/Configuration-file)
- [NLog - File target](https://github.com/NLog/NLog/wiki/File-target)
- [NLog - FileTarget Archive Examples](https://github.com/NLog/NLog/wiki/FileTarget-Archive-Examples)
- [Use NLog to log](https://sorceryforce.net/en/tips/asp-net-core-log-n-log)
- [How To Start Logging With NLog](https://betterstack.com/community/guides/logging/how-to-start-logging-with-nlog/)
- [NLog C# (How it Works for Developers)](https://ironpdf.com/blog/net-help/nlog-csharp-guide/)
- [How to log errors in WinForms using NLog](https://grantwinney.com/log-errors-in-winforms-with-nlog/)
- [How to log messages to multiple targets with NLog](https://grantwinney.com/how-to-log-messages-to-multiple-targets-with-nlog/)
- [Basic Understanding Of NLog](https://www.c-sharpcorner.com/article/basic-understanding-of-nlog/)