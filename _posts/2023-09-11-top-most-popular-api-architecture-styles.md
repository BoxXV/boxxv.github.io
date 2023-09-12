---
layout: post
title: API và những kiến trúc API phổ biến
subtitle: Top Architectural Styles for APIs
author: "TAn"
image: "img/lonely.jpg"
tags:
- API
- REST
- GraphQL
- SOAP
- JSON-RPC
- gRPC
- WebSocket
- OData
- Falcor
---

# Mục lục

- [Mục lục](#mục-lục)
- [Khái niệm API](#khái-niệm-api)
  - [Kiến trúc API là gì?](#kiến-trúc-api-là-gì)
  - [API architecture styles](#api-architecture-styles)
- [Các kiểu kiến trúc API phổ biến](#các-kiểu-kiến-trúc-api-phổ-biến)
  - [1. RESTful](#1-restful)
  - [2. Webhook](#2-webhook)
  - [3. GraphQL](#3-graphql)
  - [4. SOAP](#4-soap)
  - [5. gRPC](#5-grpc)
  - [6. Websocket](#6-websocket)
- [Tổng kết](#tổng-kết)


![API](https://boxxv.github.io/img/2023/1691972027119.gif "API")

Trong quá trình làm việc với API, có lẽ do sự phổ biến của REST API mà ta quên đi sự tồn tại của các loại API khác.

API là một thuật ngữ không còn xa lạ với các lập trình viên. Ngoài những kiến trúc API quen thuộc như RESTful hoặc SOAP thì bạn đã hiểu hết về những đặc điểm của các loại API phổ biến khác chưa? Hãy cùng xem qua bài viết dưới đây để hiểu thêm về API nhé!

# Khái niệm API

Tên đầy đủ của API là Application Programming Interface (giao diện lập trình ứng dụng). Đây là một tập hợp các giao thức, cơ chế, câu lệnh,….dùng để định nghĩa cách mà 2 thành phần của phần mềm có thể tương tác và trao đổi dữ liệu với nhau. Hay nói cách khác, API là một phần mềm giao tiếp giữa chương trình và hệ điều hành.

## Kiến trúc API là gì?

Kiến trúc API là một tập hợp các quy tắc và tiêu chuẩn hướng dẫn thông tin giúp cho các ứng dụng phần mềm có thể chia sẻ dữ liệu với nhau thông qua API. Kiến trúc API thường được giải thích dễ hiểu dưới dạng máy chủ và máy khách, trong đó ứng dụng yêu cầu được gọi là máy khách, ngược lại ứng dụng phản hồi đóng vai trò máy chủ.

Với kiến trúc API, các nhà phát triển có thể tạo ra các ứng dụng mà không cần biết chi tiết về các phần khác của hệ thống, chỉ cần tương tác thông qua API. Điều này làm cho việc xây dựng ứng dụng dễ dàng hơn và giảm thiểu sự phụ thuộc giữa các phần của hệ thống.

## API architecture styles

Các kiểu kiến trúc API (API architecture styles) là những kiểu kiến trúc chung được sử dụng để thiết kế các API. Các kiểu kiến trúc này cung cấp một cách tiếp cận chuẩn hóa để thiết kế và triển khai các API, giúp cho các nhà phát triển có thể dễ dàng phát triển, tương tác và quản lý các ứng dụng của họ.

Theo báo cáo [2023 State of the API Report](https://www.postman.com/state-of-api/api-technologies/#api-technologies) của Postman, các kiểu kiến trúc API phổ biến nhất là:

![API](https://boxxv.github.io/img/2023/12af029c4353960dcf42.jpg "API")

Dựa vào kết quả này, ta có thể thấy kết quả cho tới thời điểm hiện tại (tháng 8 năm 2023) không thay đổi quá nhiều. Mình sẽ nêu ra những ưu nhược điểm của vài kiểu kiến trúc API mà mình thấy nó ở vị trí top nhá

# Các kiểu kiến trúc API phổ biến

Tùy theo nhu cầu cầu của mỗi website mà các nhà lập trình lựa chọn kiểu kiến trúc API phù hợp. Mỗi kiểu API đều sẽ có những ưu, nhược điểm và đặc trưng khác nhau. Một số kiểu kiến trúc API phổ biến nhất hiện nay có thể kể đến:

## 1. RESTful

![API](https://boxxv.github.io/img/2023/REST-API.png "API")

Là kiểu API được ưa chuộng nhất cho đến hiện tại, phần lớn các web API được xây dựng dựa trên REST. API này hoạt động dựa trên các nguyên tắc và quy ước của giao thức web chuẩn HTTP và sử dụng các phương thức HTTP để thực hiện các thao tác trên tài nguyên một cách đơn giản và hiệu quả.

**Ưu điểm:**
- RESTful API sử dụng các phương thức HTTP chuẩn, giúp các nhà phát triển dễ dàng tương tác và thao tác trên các nguồn tài nguyên.
- Khả năng mở rộng tốt, dễ dàng thao tác, dễ dàng triển khai và quản lý
- Cho phép tách biệt giữa client và server từ đó giảm độ phụ thuộc giữa 2 bên đồng thời tăng khả năng tái sử dụng của các phần mềm
- Hỗ trợ đa nền tảng và dễ dàng tương thích với nhiều hệ điều hành khác nhau

**Nhược điểm:**
- Có thể gặp khó khăn trong việc xử lý các hoạt động phức tạp hoặc thao tác nằm ngoài các phương thức HTTP chuẩn.
- Khối lượng dữ kiệu trả về rất lớn dẫn đến tốn kém tài nguyên

**Bạn nên sử dụng kiến trúc REST khi nào?**

Kiến trúc RESTful API thường được sử dụng trong các ứng dụng web và di động. Nó là một lựa chọn tốt cho các ứng dụng cần thiết kế để hoạt động trên nhiều nền tảng và thiết bị khác nhau. REST API cũng được sử dụng trong các hệ thống quản lý dữ liệu, các hệ thống phân tán và trong các hệ thống IoT để tương tác với các thiết bị.

## 2. Webhook

![Webhook](https://boxxv.github.io/img/2023/Websocket.webp "Webhook")

Webhook, còn được gọi là API đảo ngược, web callback hoặc HTTP push API là một cách để một ứng dụng cung cấp cho các ứng dụng khác thông tin thời gian thực. Nó cung cấp dữ liệu khi một sự kiện xảy ra hoặc gần như ngay lập tức.

Hiện nay, webhook thường được các lập trình viên (IT) sử dụng nhằm phục vụ cho mục đích cập nhật các event theo thời gian thực và cũng để có thể tiết kiệm tài nguyên nhất. Bên cạnh đó, webhook còn là công cụ được sử dụng thông qua API trong trường hợp API của bạn không được tốt hoặc bạn không có API.

Nhờ có Webhook mà bạn sẽ có thể tạo ra được những giải pháp tối ưu giúp cung cấp dữ liệu mà ứng dụng cần. Do đó, quá trình hoạt động sẽ được đảm bảo nhanh chóng và dễ dàng hơn. Mặc dù webhook có nhiều ưu điểm và tính năng nhưng nếu bạn không thường xuyên sử dụng nó để call dữ liệu thì sẽ không lấy được những bản cập nhất mới nhất khi hệ thống ngừng hoạt động

**Ưu điểm:**
- Thời gian thực: Webhook cho phép truyền dữ liệu trực tiếp mỗi khi sự kiện xảy ra, giúp các ứng dụng web tương tác với nhau theo thời gian thực.
- Tiết kiệm tài nguyên: Vì các cập nhật chỉ được gửi khi cần thiết, Webhook giúp tiết kiệm tài nguyên hơn so với việc liên tục truy vấn API để kiểm tra sự thay đổi dữ liệu.
- Tích hợp dễ dàng: Webhook có tính khả chuyển cao, cho phép tích hợp với các ứng dụng web khác một cách dễ dàng.

**Nhược điểm:**
- Không đa dạng và không linh hoạt như một API hoàn chỉnh.
- Nó chỉ đơn giản là một bộ truyền tải dữ liệu một chiều
- Không có cơ chế đảm bảo tính sẵn sàng của người nhận. Vì vậy bạn sẽ không biết được liệu dữ liệu đang được truyền tải đến đúng địa chỉ hay không

Nên sử dụng kiến trúc Webhook trong các trường hợp cần truyền tải dữ liệu theo thời gian thực và sự kiện xảy ra không định kỳ. Ví dụ: cập nhật trang trạng thái của một đơn hàng, gửi thông báo khi có tin nhắn mới, cập nhật thông tin trạng thái của máy chủ và phần mềm.

## 3. GraphQL

![API](https://boxxv.github.io/img/2023/GraphQL.webp "API")

GraphQL là ngôn ngữ thao tác và truy vấn dữ liệu nguồn mở cho API, cung cấp cho client 1 cách thức dễ dàng để request chính xác những gì họ cần, giúp việc phát triển API dễ dàng hơn theo thời gian.

**Ưu điểm:**
- GraphQL giúp ứng dụng của bạn có thể phát triển thêm API mà không làm ảnh hưởng lên các truy vấn đã có.
- Không cần yêu cầu một kiến trúc ứng dụng cụ thể mà vẫn hoạt động như một Rest API. Đồng thời bạn có thể làm việc với các công cụ API hiện có
- Hỗ trợ tối đa việc kiểm soát và xử lý data type. Từ đó có thể hạn chế sự sai lệch trong giao tiếp giữa server và client.
- Mã hoá tĩnh: Mã hoá tĩnh giúp GraphQL phát hiện các lỗi tại thời điểm compile, giúp giảm thiểu sự cố hệ thống và thời gian giải quyết lỗi.
- Đa ngôn ngữ: GraphQL hỗ trợ nhiều ngôn ngữ, cho phép phát triển ứng dụng đa nền tảng.
- GraphQL không phụ thuộc vào cơ sở dữ liệu, nghĩa là bạn có thể sử dụng nó với hầu hết mọi cơ sở dữ liệu mà bạn có thể nghĩ đến.
- Tài liệu để học về GraphQL có sẵn và rất chi tiết, dễ dàng học, tiếp thu.

**Nhược điểm:**
- Nhiều extension mã nguồn mở của GraphQL không tương thích và không thể hoạt động với REST API
- Nhiều truy vấn bị GraphQL chuyển lên server. Và điều này khiến server chịu thêm nhiều công việc và trở nên phức tạp hơn.
- Công việc để triển khai GraphQL và server sẽ có thể nhiều hơn việc phát triển một Rest API.
- Khó khăn trong quản lý cache: Do khả năng động và linh hoạt của GraphQL trong việc lấy dữ liệu, việc quản lý cache có thể khó khăn hơn so với REST API.
- Khó khăn trong việc định nghĩa schema: GraphQL yêu cầu định nghĩa schema chính xác và chi tiết để tối ưu hóa hoạt động của API.
- GraphQL không phải là lựa chọn tốt nhất cho các truy vấn phức tạp, vì quá nhiều truy vấn lồng nhau có thể gây quá tải và tắt hệ thống.

GraphQL thường được sử dụng trong các ứng dụng có yêu cầu phải lấy dữ liệu phức tạp và đa dạng, hoặc ứng dụng có nhu cầu tương tác dữ liệu phân tán từ nhiều nguồn. Nó cũng được sử dụng trong các ứng dụng đòi hỏi tốc độ truy vấn nhanh và giảm thiểu lượng truy vấn tới server.

## 4. SOAP

![API](https://boxxv.github.io/img/2023/SOAP.webp "API")

[SOAP](https://en.wikipedia.org/wiki/SOAP) dựa trên WSDL (Web Services Description Language), một ngôn ngữ markup có thể mở rộng (XML) để gửi dữ liệu giữa các phần mềm. Được sử dụng để gửi thông điệp giữa các ứng dụng với nhau thông qua HTTP. SOAP thường được triển khai để truyền data nội bộ có yêu cầu bảo mật cao. Một lợi thế nữa của SOAP là nó hoạt động trên mọi giao thức truyền thông (communication protocol) không chỉ trên HTTP như trường hợp của REST.

**Ưu điểm:**
- SOAP có thể được phát triển bằng bất kỳ ngôn ngữ nào nhờ có tính trung lập của ngôn ngữ
- SOAP được định dạng bằng XML làm cho việc đoc hiểu dễ dàng hơn.
- Hỗ trợ tất cả các giao thức internet phổ biến, bao gồm HTTP, SMTP, TCP, và FTP.
- Hỗ trợ rất nhiều ngôn ngữ lập trình, bao gồm C++, Java, .NET, và Python.
- Đảm bảo tính toàn vẹn và độ tin cậy cao trong việc truyền tải dữ liệu qua mạng.

**Nhược điểm:**
- Vì chỉ định dạng bằng XML nên có tốc độ tải chậm hơn so với tiêu chuẩn phần mềm trung gian khác như CORBA và RPC
- So với các phương thức mới sử dụng đa ngôn ngữ thì SOAP kém linh hoạt hơn khi chỉ được định dạng bằng XML.

Kiến trúc SOAP nên được sử dụng trong các trường hợp cần đảm bảo tính bảo mật, tính toàn vẹn và độ tin cậy cao, ví dụ như trong các ứng dụng quản lý tài khoản ngân hàng hoặc các ứng dụng y tế. Tuy nhiên, nếu bạn đang phát triển các ứng dụng có tính tương tác cao, đòi hỏi tốc độ truyền tải nhanh và cấu trúc dữ liệu đơn giản, thì kiến trúc SOAP có thể không phù hợp.

## 5. gRPC

![API](https://boxxv.github.io/img/2023/gRPC.webp "API")

gRPC là viết tắt của Google Remote Procedure Call. gRPC là một khung RPC nguồn mở được sử dụng để tạo các API nhanh và có thể mở rộng. Nó cho phép phát triển các hệ thống nối mạng và giao tiếp mở giữa các ứng dụng máy khách và máy chủ gRPC**.**

**Ưu điểm:**
- gRPC là giải pháp thay thế RPC hoàn chỉnh nên nó hoạt động dễ dàng trên nhiều loại hệ thống và ngôn ngữ.
- Việc sử dụng HTTP/2 kết nối mã hóa đầu cuối TLS trong gRPC đảm bảo tính bảo mật của API hơn.
- gRPC hỗ trợ phát trực tuyến phía máy khách hoặc máy chủ với tính nặng ngữ nghĩa. Điều này giúp cho việc xây dựng dịch vụ hoặc ứng dụng phát trực tuyến trở nên đơn giản hơn nhiều.
- Tốc độ nhanh hơn: gRPC được xây dựng trên HTTP/2, với đó là hỗ trợ cho multiplexing, nén header, và stream data. Điều này cho phép tốc độ truyền tải dữ liệu nhanh hơn và giảm thiểu lưu lượng mạng.
- Giảm thiểu độ trễ (latency): Vì gRPC sử dụng HTTP/2 để truyền tải dữ liệu, điều này giúp giảm thiểu độ trễ trong việc truyền tải dữ liệu giữa các service, giúp cho hệ thống hoạt động mượt mà hơn.
- Tính khả chuyển: Giao thức gRPC được hỗ trợ bởi nhiều ngôn ngữ lập trình, cho phép phát triển đa nền tảng và tích hợp dễ dàng.
- Hỗ trợ cho stream data: gRPC cho phép truyền tải dữ liệu theo kiểu streaming, cho phép tạo ra các ứng dụng đa kênh.
- Tính năng mã hóa dữ liệu: gRPC sử dụng Protobuf để mã hóa dữ liệu, đây là một định dạng dữ liệu nhị phân hiệu quả hơn so với JSON hoặc XML. Protobuf cho phép compress dữ liệu và giảm thiểu kích thước gói tin truyền tải, giúp giảm tải băng thông mạng.

**Nhược điểm:**
- Cách nén thông báo của Protobuf khiến người dùng không thể đọc hiểu nội dung.
- Không có bộ nhớ đệm cạnh: gRPC sử dụng phương thức POST, một mối đe dọa với bảo mật API.
- gRPC sử dụng nhiều HTTP/2 nên không thể vận hành dịch vụ trực tiếp từ trình duyệt web. Bạn cần một lớp proxy và gRPC-web để chuyển đổi giữa HTTP/1.1 và HTTP/2.
- Yêu cầu kiến thức chuyên sâu về mạng và lập trình để triển khai gRPC.
- Cần phải có một môi trường hoạt động đúng để tận dụng được các ưu điểm của gRPC.

Nên sử dụng kiến trúc gRPC khi bạn đang xây dựng các ứng dụng cần tốc độ truyền tải dữ liệu cao, hoặc các ứng dụng real-time cần truyền tải dữ liệu liên tục. gRPC rất được ưa chuộng khi phát triển ứng dụng có kiến trúc microservices. Tuy nhiên, nếu bạn mới bắt đầu hoặc không có nhiều kinh nghiệm về mạng và lập trình, có thể gRPC sẽ không phù hợp với bạn.

## 6. Websocket

![API](https://boxxv.github.io/img/2023/Websocket.webp "API")

WebSoket là công nghệ hỗ trợ giao tiếp hai chiều (full-duplex) giữa client và server bằng cách sử dụng một giao thức TCP (Transmission Control Protocol) để tạo một kết nối hiệu quả và ít tốn kém. Nó cho phép các ứng dụng web thiết lập kết nối liên tục và truyền tải dữ liệu trong thời gian thực, đồng thời giảm thiểu tải cho máy chủ và tăng trải nghiệm người dùng. Kết nối WebSocket cũng nhanh hơn nhiều so với HTTP, do đó chúng là sự lựa chọn tuyệt vời nếu bạn đang tìm kiếm kết nối nhanh nhất có thể.

**Ưu điểm:**
- WebSockets cung cấp khả năng giao tiếp hai chiều mạnh mẽ, có độ trễ thấp và dễ xử lý lỗi. Không cần phải có nhiều kết nối như phương pháp Comet long-polling và cũng không có - những nhược điểm như Comet streaming.
- API cũng rất dễ sử dụng trực tiếp mà không cần bất kỳ các tầng bổ sung nào, so với Comet, thường đòi hỏi một thư viện tốt để xử lý kết nối lại, thời gian chờ timeout, các Ajax request (yêu cầu Ajax), các tin báo nhận và các dạng truyền tải tùy chọn khác nhau (Ajax long-polling và jsonp polling).
- Truyền tải dữ liệu nhanh và hiệu quả, giảm thiểu tải cho máy chủ so với các phương pháp truyền tải dữ liệu khác như polling.
- Thiết lập kết nối liên tục, giúp ứng dụng web có thể truyền tải dữ liệu trong thời gian thực và phản hồi nhanh chóng.
- Được hỗ trợ bởi hầu hết các trình duyệt web hiện đại và các thư viện lập trình, dễ dàng để triển khai.

**Nhược điểm:**
- Nó là một đặc tả mới của HTML5, nên nó vẫn chưa được tất cả các trình duyệt hỗ trợ.
- Không có phạm vi yêu cầu nào. Do WebSocket là một TCP socket chứ không phải là HTTP request, nên không dễ sử dụng các dịch vụ có phạm vi-yêu cầu, như SessionInViewFilter của Hibernate. Hibernate là một framework kinh điển cung cấp một bộ lọc xung quanh một HTTP request. Khi bắt đầu một request, nó sẽ thiết lập một contest (chứa các transaction và liên kết JDBC) được ràng buộc với luồng request. Khi request đó kết thúc, bộ lọc hủy bỏ contest này.
- Có thể gây ra vấn đề bảo mật khi kết nối trực tiếp với máy chủ, vì vậy cần có các biện pháp bảo mật để bảo vệ dữ liệu.
- Khó để xử lý lỗi và quản lý kết nối, đặc biệt khi số lượng kết nối lớn.
- Nếu một WebSocket bị ngắt kết nối, không có cân bằng tải hoặc cơ chế để kết nối lại
- Không thể sử dụng được trên một số mạng chặt chẽ, ví dụ như các mạng công ty hay trường học.
- Không hỗ trợ bộ nhớ cache

Kiến trúc WebSockets thường được sử dụng trong các ứng dụng cần truyền thông tin thời gian thực (real-time) với tốc độ kết nối cao như trò chuyện trực tuyến, trò chơi trực tuyến, các ứng dụng video và âm nhạc trực tuyến, hệ thống đánh giá thời gian thực và các ứng dụng khác cần truyền thông tin nhanh và chính xác.

# Tổng kết

Như bạn có thể thấy, có rất nhiều điều cần lưu ý khi sử dụng API, không chỉ riêng REST, mặc dù REST vẫn là kiến trúc dẫn đầu với khoảng cách rất xa so với các kiến trúc khác. Có thể nói rằng khi các giải pháp như microservices, headless và serverless trở nên phổ biến hơn, chúng ta cũng sẽ thấy sự gia tăng về việc sử dụng một số kiến trúc API khác.

Nhìn vào báo cáo thì có thể thấy một vài kiến trúc khác như MQTT, AMQP, Server-Sent Events, EDI/EDA. Tuy nhiên chúng không quá phổ biến và chỉ ứng dụng vào những hệ thống đặc thù nên mình sẽ không nhắc tới ở đây.

Mong rằng, bài viết này có thể giúp bạn hình dung được các kiến trúc API phổ biến khác ngoài kiến trúc REST đã quá quen thuộc, nhờ đó mà có thể đưa ra lựa chọn phù hợp cho hệ thống của bạn trong tương lai 😄

Cảm ơn mọi người đã dành thời gian theo dõi bài viết này 🙇

-----
Tham khảo:
- [API và những kiến trúc API phổ biến](https://zodinet.com/api-va-nhung-kien-truc-api-pho-bien/)
- [Các loại kiến trúc API phổ biến mà bạn nên biết](https://viblo.asia/p/cac-loai-kien-truc-api-pho-bien-ma-ban-nen-biet-m2vJPx9oJeK)
- []()
- [Webhooks vs API - Sự khác biệt là gì?](https://viblo.asia/p/webhooks-vs-api-su-khac-biet-la-gi-Qbq5QQkG5D8)
- []()