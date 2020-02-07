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
- **Database**. Ghi Log vào cơ sở dữ liệu có nhiều lợi thế
  * Bạn có thể truy xuất Log từ bất cứ đâu mà không cần truy cập vào máy sản xuất.
  * Nó dễ dàng tổng hợp các bản ghi Log từ nhiều máy.
  * Không có trường hợp nào các bản ghi Log sẽ bị xóa khỏi một máy cục bộ.
  * Bạn có thể dễ dàng tìm kiếm và trích xuất số liệu thống kê từ Log. Điều này đặc biệt hữu ích nếu bạn sử dụng ghi Log có cấu trúc.
- Có rất nhiều lựa chọn cho cơ sở dữ liệu để lưu trữ Log của bạn. Chúng ta có thể phân loại chúng như sau:
  * Cơ sở dữ liệu **Relational** luôn là một lựa chọn. Họ dễ dàng thiết lập, có thể được truy vấn bằng SQL và hầu hết các kỹ sư đã quen thuộc với họ. Cơ sở dữ liệu quan hệ chứa các bảng và mỗi bảng có Primary Key riêng.
  * Cơ sở dữ liệu **NoSQL** như [CouchDB](https://couchdb.apache.org). Đây là hoàn hảo cho các bản ghi có cấu trúc được lưu trữ ở định dạng JSON.
  * Cơ sở dữ liệu **Time-series** như [InfluxDB](https://www.influxdata.com) được tối ưu hóa để lưu trữ các sự kiện dựa trên thời gian. Điều này có nghĩa là hiệu suất ghi Log của bạn sẽ tốt hơn và Log của bạn sẽ chiếm ít dung lượng lưu trữ hơn. Đây là một lựa chọn tốt cho đăng nhập tải cao cường độ cao.
- **Searchable Solutions** như [Logstash](https://www.elastic.co/logstash) + [Elastic Search](https://www.elastic.co/elasticsearch) + [Kibana](https://www.elastic.co/kibana) (`Elastic Stack`) cung cấp dịch vụ đầy đủ cho Log của bạn. Họ sẽ lưu trữ, lập chỉ mục, thêm khả năng tìm kiếm và thậm chí trực quan hóa dữ liệu Log của bạn. Họ làm việc tốt nhất với đăng nhập có cấu trúc.
- **Error Monitoring** Các công cụ giám sát lỗi cũng có thể hoạt động như các mục tiêu đăng nhập. Điều này rất có lợi vì chúng có thể hiển thị lỗi cùng với các thông điệp tường trình trong cùng một bối cảnh. Ví dụ, bối cảnh có thể là cùng một yêu cầu http. Một vài lựa chọn là Elmah và Azure Application Insights.
- **Logging to File** Đăng nhập vào tập tin vẫn là một mục tiêu đăng nhập tốt. Nó không phải là độc quyền, bạn có thể đăng nhập cả vào tệp và cơ sở dữ liệu chẳng hạn. Đối với các ứng dụng máy tính để bàn, đăng nhập vào tập tin là rất hiệu quả. Khi một vấn đề đã xảy ra, khách hàng có thể dễ dàng tìm và gửi các tệp Log của họ để điều tra.
- **Logging to Standard Output (Console) and Debug Output (Trace)** Ghi Log vào Đầu ra tiêu chuẩn (Bảng điều khiển) và Đầu ra gỡ lỗi (Dấu vết) - Ghi Log vào Bảng điều khiển, còn được gọi là Đầu ra tiêu chuẩn, rất thuận tiện, đặc biệt là trong quá trình phát triển. Windows cũng hỗ trợ một mục tiêu ghi Log tương tự có tên là Debug Output, bạn có thể đăng nhập bằng System.Diagnostics.Trace ("Tin nhắn của tôi"). Điều tuyệt vời của cả hai về ghi Log Console và Trace là bạn cũng có thể đăng nhập tin nhắn từ mã gốc, dễ dàng đạt được một hệ thống ghi Log dùng chung. Bạn có thể xem Đầu ra gỡ lỗi trực tiếp với một chương trình như DebugView. Bạn cũng có thể sử dụng lớp ConsoleTraceListener để hướng thông tin này đến mọi nơi, như đến cơ sở dữ liệu.
- **Logging to Event Viewer** Đăng nhập vào Trình xem sự kiện - Nếu ứng dụng của bạn có trên Windows, bạn có thể sử dụng Nhật ký sự kiện Windows để ghi Log tin nhắn. Nó rất dễ làm và bạn có thể xem tin nhắn bằng chương trình Event Viewer. Như một phần thưởng, tất cả các sự cố được tự động thêm vào như Log sự kiện. Vì vậy, sau bất kỳ sự cố quy trình .NET nào, bạn có thể vào Trình xem sự kiện và xem Ngoại lệ và ngăn xếp cuộc gọi của nó. Điều này khá tốn kém về mặt hiệu suất, do đó, tốt nhất là chỉ sử dụng cho các thông báo quan trọng, như lỗi nghiêm trọng.
- **Log to ETW** Đăng nhập vào ETW - Windows có một hệ thống ghi Log tích hợp cực kỳ nhanh có tên là Truy tìm sự kiện cho Windows (ETW). Bạn có thể sử dụng nó để xem các bản ghi từ .NET framework, hệ điều hành và thậm chí cả kernel. Nhưng bạn cũng có thể sử dụng ETW để đăng nhập chính mình với System.Diagnostics.Tracing.EventSource. Đây là tùy chọn đăng nhập nhanh nhất có sẵn trong .NET. Nếu bạn có một con đường hấp dẫn mà thực hiện 100.000 lần một giây, thì ETW có thể dành cho bạn. .NET Core 3.0 Preview 5+ hiện có một thay thế ETW được gọi là dotnet-track là đa nền tảng.

Tham khảo:
- [Logging in C# .NET Modern-day Practices: The Complete Guide](https://michaelscodingspot.com/logging-in-dotnet/)
