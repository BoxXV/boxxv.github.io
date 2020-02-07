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

Ghi Log có một phần quan trọng để chạy trong kịch bản mà bạn có thể sử dụng gỡ lỗi tương tác (nghĩa là đính kèm trình gỡ lỗi như Visual Studio). Nó cho phép chúng tôi điều tra lỗi sau khi sự cố đã xảy ra. Trong một số trường hợp, như Gỡ lỗi sản phẩm, Log có thể là thông tin duy nhất bạn có.

Ngay cả khi bạn có thể gỡ lỗi quy trình của riêng mình, Log có thể cung cấp cho bạn thông tin vô giá về các thành phần khác như thư viện của bên thứ 3, có sẵn trong framework .NET và CLR.

Bên cạnh việc ghi Log, một thuật ngữ mới đang trở nên phổ biến: Giám sát. Giám sát có nghĩa là có một công cụ tự động báo cáo thông tin về ứng dụng của bạn. Thông tin đó thường là lỗi (Giám sát lỗi Error, Giám sát sự cố Crash), nhưng cũng là thông tin về các yêu cầu và về hiệu suất (Giám sát hiệu suất). Điều này rất khác với việc ghi Log nơi mã của bạn chủ động viết tin nhắn và ngoại lệ để ghi Log.

Ghi Log cũng có thể được sử dụng để thu thập dữ liệu và số liệu thống kê về người dùng của bạn. Dữ liệu này có thể được sử dụng để nghiên cứu mô hình sử dụng, nhân khẩu học và hành vi. Không cần phải nói, loại dữ liệu này là vô giá trong một số sản phẩm.

### Các nơi có thể ghi Log - Logging Target Types

Khi chúng tôi nói về ghi Log, theo truyền thống, chúng tôi có nghĩa là lưu tin nhắn vào một tệp. Đó thực sự là ghi Log, nhưng còn nhiều các loại ghi Log duy nhất này. Dưới đây là một số mục tiêu ghi Log phổ biến để xem xét:
- Cơ sở dữ liệu: ghi Log vào cơ sở dữ liệu có nhiều lợi thế
  * Bạn có thể truy xuất Log từ bất cứ đâu mà không cần truy cập vào máy sản xuất.
  * Nó dễ dàng tổng hợp các bản ghi Log từ nhiều máy.
  * Không có trường hợp nào các bản ghi Log sẽ bị xóa khỏi một máy cục bộ.
  * Bạn có thể dễ dàng tìm kiếm và trích xuất số liệu thống kê từ Log. Điều này đặc biệt hữu ích nếu bạn sử dụng ghi Log có cấu trúc.
- Có rất nhiều lựa chọn cho cơ sở dữ liệu để lưu trữ nhật ký của bạn. Chúng ta có thể phân loại chúng như sau:
  * **Relational Databases** luôn là một lựa chọn. Họ dễ dàng thiết lập, có thể được truy vấn bằng SQL và hầu hết các kỹ sư đã quen thuộc với họ.
  * Cơ sở dữ liệu **NoQuery** như [CouchDB](https://couchdb.apache.org). Đây là hoàn hảo cho các bản ghi có cấu trúc được lưu trữ ở định dạng JSON.
  * Cơ sở dữ liệu `Time-series` như [InfluxDB](https://www.influxdata.com) được tối ưu hóa để lưu trữ các sự kiện dựa trên thời gian. Điều này có nghĩa là hiệu suất ghi nhật ký của bạn sẽ tốt hơn và nhật ký của bạn sẽ chiếm ít dung lượng lưu trữ hơn. Đây là một lựa chọn tốt cho đăng nhập tải cao cường độ cao.
- Các giải pháp có thể tìm kiếm như Logstash + Tìm kiếm đàn hồi + Kibana ("Ngăn xếp đàn hồi") cung cấp dịch vụ đầy đủ cho nhật ký của bạn. Họ sẽ lưu trữ, lập chỉ mục, thêm khả năng tìm kiếm và thậm chí trực quan hóa dữ liệu nhật ký của bạn. Họ làm việc tốt nhất với đăng nhập có cấu trúc.

Tham khảo:
- [Logging in C# .NET Modern-day Practices: The Complete Guide](https://michaelscodingspot.com/logging-in-dotnet/)
