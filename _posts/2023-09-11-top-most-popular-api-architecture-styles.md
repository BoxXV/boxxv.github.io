---
layout: post
title: API và những kiến trúc API phổ biến
subtitle: Top Architectural Styles for APIs
author: "TAn"
image: "img/techskills.jpg"
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
- [Các kiểu kiến trúc API phổ biến](#các-kiểu-kiến-trúc-api-phổ-biến)
  - [1. RESTful](#1-restful)
  - [2. SOAP](#2-soap)
  - [3. GraphQL](#3-graphql)
  - [4. gRPC](#4-grpc)
  - [5. Websocket](#5-websocket)
  - [6. Webhook](#6-webhook)
- [Tổng kết](#tổng-kết)


![API](https://boxxv.github.io/img/2023/1691972027119.gif "API")

API là một thuật ngữ không còn xa lạ với các lập trình viên. Ngoài những kiến trúc API quen thuộc như RESTful hoặc SOAP thì bạn đã hiểu hết về những đặc điểm của các loại API phổ biến khác chưa? Hãy cùng xem qua bài viết dưới đây để hiểu thêm về API nhé!

# Khái niệm API

Tên đầy đủ của API là Application Programming Interface (giao diện lập trình ứng dụng). Đây là một tập hợp các giao thức, cơ chế, câu lệnh,….dùng để định nghĩa cách mà 2 thành phần của phần mềm có thể tương tác và trao đổi dữ liệu với nhau. Hay nói cách khác, API là một phần mềm giao tiếp giữa chương trình và hệ điều hành.

## Kiến trúc API là gì?

Kiến trúc API là một tập hợp các quy tắc và tiêu chuẩn hướng dẫn thông tin giúp cho các ứng dụng phần mềm có thể chia sẻ dữ liệu với nhau thông qua API. Kiến trúc API thường được giải thích dễ hiểu dưới dạng máy chủ và máy khách, trong đó ứng dụng yêu cầu được gọi là máy khách, ngược lại ứng dụng phản hồi đóng vai trò máy chủ.

# Các kiểu kiến trúc API phổ biến

Tùy theo nhu cầu cầu của mỗi website mà các nhà lập trình lựa chọn kiểu kiến trúc API phù hợp. Mỗi kiểu API đều sẽ có những ưu, nhược điểm và đặc trưng khác nhau. Một số kiểu kiến trúc API phổ biến nhất hiện nay có thể kể đến:

## 1. RESTful

![API](https://boxxv.github.io/img/2023/REST-API.png "API")

Là kiểu API được ưa chuộng nhất cho đến hiện tại, phần lớn các web API được xây dựng dựa trên REST. API này hoạt động dựa trên các nguyên tắc và quy ước của giao thức web chuẩn HTTP và sử dụng các phương thức HTTP để thực hiện các thao tác trên tài nguyên một cách đơn giản và hiệu quả.

Ưu điểm:
- Khả năng mở rộng tốt, dễ dàng thao tác, dễ dàng triển khai và quản lý
- Cho phép tách biệt giữa client và server từ đó giảm độ phụ thuộc giữa 2 bên đồng thời tăng khả năng tái sử dụng của các phần mềm
- Hỗ trợ đa nền tảng và dễ dàng tương thích với nhiều hệ điều hành khác nhau

Nhược điểm:
- Có thể gặp khó khăn trong việc xử lý các hoạt động phức tạp hoặc thao tác nằm ngoài các phương thức HTTP chuẩn.
- Khối lượng dữ kiệu trả về rất lớn dẫn đến tốn kém tài nguyên

## 2. SOAP

![API](https://boxxv.github.io/img/2023/SOAP.webp "API")

[SOAP](https://en.wikipedia.org/wiki/SOAP) dựa trên WSDL (Web Services Description Language), một ngôn ngữ markup có thể mở rộng (XML) để gửi dữ liệu giữa các phần mềm. Được sử dụng để gửi thông điệp giữa các ứng dụng với nhau thông qua HTTP. SOAP thường được triển khai để truyền data nội bộ có yêu cầu bảo mật cao. Một lợi thế nữa của SOAP là nó hoạt động trên mọi giao thức truyền thông (communication protocol) không chỉ trên HTTP như trường hợp của REST.

Ưu điểm:
- SOAP có thể được phát triển bằng bất kỳ ngôn ngữ nào nhờ có tính trung lập của ngôn ngữ
- SOAP được định dạng bằng XML làm cho việc đoc hiểu dễ dàng hơn.

Nhược điểm:
- Vì chỉ định dạng bằng XML nên có tốc độ tải chậm hơn so với tiêu chuẩn phần mềm trung gian khác như CORBA và RPC
- So với các phương thức mới sử dụng đa ngôn ngữ thì SOAP kém linh hoạt hơn khi chỉ được định dạng bằng XML.

## 3. GraphQL

![API](https://boxxv.github.io/img/2023/GraphQL.webp "API")

GraphQL là ngôn ngữ thao tác và truy vấn dữ liệu nguồn mở cho API, cung cấp cho client 1 cách thức dễ dàng để request chính xác những gì họ cần, giúp việc phát triển API dễ dàng hơn theo thời gian.

Ưu điểm:
- GraphQL giúp ứng dụng của bạn có thể phát triển thêm API mà không làm ảnh hưởng lên các truy vấn đã có.
- Không cần yêu cầu một kiến trúc ứng dụng cụ thể mà vẫn hoạt động như một Rest API. Đồng thời bạn có thể làm việc với các công cụ API hiện có
- Hỗ trợ tối đa việc kiểm soát và xử lý data type. Từ đó có thể hạn chế sự sai lệch trong giao tiếp giữa server và client.
- Tài liệu để học về GraphQL có sẵn và rất chi tiết, dễ dàng học, tiếp thu.

Nhược điểm:
- Nhiều extension mã nguồn mở của GraphQL không tương thích và không thể hoạt động với REST API
- Nhiều truy vấn bị GraphQL chuyển lên server. Và điều này khiến server chịu thêm nhiều công việc và trở nên phức tạp hơn.
- Công việc để triển khai GraphQL và server sẽ có thể nhiều hơn việc phát triển một Rest API.

## 4. gRPC

![API](https://boxxv.github.io/img/2023/gRPC.webp "API")

gRPC là viết tắt của Google Remote Procedure Call. gRPC là một khung RPC nguồn mở được sử dụng để tạo các API nhanh và có thể mở rộng. Nó cho phép phát triển các hệ thống nối mạng và giao tiếp mở giữa các ứng dụng máy khách và máy chủ gRPC**.**

Ưu điểm:
- gRPC là giải pháp thay thế RPC hoàn chỉnh nên nó hoạt động dễ dàng trên nhiều loại hệ thống và ngôn ngữ.
- Việc sử dụng HTTP/2 kết nối mã hóa đầu cuối TLS trong gRPC đảm bảo tính bảo mật của API hơn.
- gRPC hỗ trợ phát trực tuyến phía máy khách hoặc máy chủ với tính nặng ngữ nghĩa. Điều này giúp cho việc xây dựng dịch vụ hoặc ứng dụng phát trực tuyến trở nên đơn giản hơn nhiều.

Nhược điểm
- Cách nén thông báo của Protobuf khiến người dùng không thể đọc hiểu nội dung.
- Không có bộ nhớ đệm cạnh: gRPC sử dụng phương thức POST, một mối đe dọa với bảo mật API.
- gRPC sử dụng nhiều HTTP/2 nên không thể vận hành dịch vụ trực tiếp từ trình duyệt web. Bạn cần một lớp proxy và gRPC-web để chuyển đổi giữa HTTP/1.1 và HTTP/2.

## 5. Websocket

![API](https://boxxv.github.io/img/2023/Websocket.webp "API")

WebSoket là công nghệ hỗ trợ giao tiếp hai chiều giữa client và server bằng cách sử dụng một giao thức TCP (Transmission Control Protocol) để tạo một kết nối hiệu quả và ít tốn kém.

Ưu điểm:
- WebSockets cung cấp khả năng giao tiếp hai chiều mạnh mẽ, có độ trễ thấp và dễ xử lý lỗi. Không cần phải có nhiều kết nối như phương pháp Comet long-polling và cũng không có - những nhược điểm như Comet streaming.
- API cũng rất dễ sử dụng trực tiếp mà không cần bất kỳ các tầng bổ sung nào, so với Comet, thường đòi hỏi một thư viện tốt để xử lý kết nối lại, thời gian chờ timeout, các Ajax request (yêu cầu Ajax), các tin báo nhận và các dạng truyền tải tùy chọn khác nhau (Ajax long-polling và jsonp polling).

Nhược điểm:
- Nó là một đặc tả mới của HTML5, nên nó vẫn chưa được tất cả các trình duyệt hỗ trợ.
- Không có phạm vi yêu cầu nào. Do WebSocket là một TCP socket chứ không phải là HTTP request, nên không dễ sử dụng các dịch vụ có phạm vi-yêu cầu, như SessionInViewFilter của Hibernate. Hibernate là một framework kinh điển cung cấp một bộ lọc xung quanh một HTTP request. Khi bắt đầu một request, nó sẽ thiết lập một contest (chứa các transaction và liên kết JDBC) được ràng buộc với luồng request. Khi request đó kết thúc, bộ lọc hủy bỏ contest này.

## 6. Webhook

![Webhook](https://boxxv.github.io/img/2023/Websocket.webp "Webhook")

Webhook, còn được gọi là API đảo ngược, web callback hoặc HTTP push API là một cách để một ứng dụng cung cấp cho các ứng dụng khác thông tin thời gian thực. Nó cung cấp dữ liệu khi một sự kiện xảy ra hoặc gần như ngay lập tức.

Hiện nay, webhook thường được các lập trình viên (IT) sử dụng nhằm phục vụ cho mục đích cập nhật các event theo thời gian thực và cũng để có thể tiết kiệm tài nguyên nhất. Bên cạnh đó, webhook còn là công cụ được sử dụng thông qua API trong trường hợp API của bạn không được tốt hoặc bạn không có API.

Nhờ có Webhook mà bạn sẽ có thể tạo ra được những giải pháp tối ưu giúp cung cấp dữ liệu mà ứng dụng cần. Do đó, quá trình hoạt động sẽ được đảm bảo nhanh chóng và dễ dàng hơn. Mặc dù webhook có nhiều ưu điểm và tính năng nhưng nếu bạn không thường xuyên sử dụng nó để call dữ liệu thì sẽ không lấy được những bản cập nhất mới nhất khi hệ thống ngừng hoạt động

# Tổng kết

Như bạn có thể thấy, có rất nhiều điều cần lưu ý khi sử dụng API, không chỉ riêng REST, mặc dù REST vẫn là kiến trúc dẫn đầu với khoảng cách rất xa so với các kiến trúc khác. Có thể nói rằng khi các giải pháp như microservices, headless và serverless trở nên phổ biến hơn, chúng ta cũng sẽ thấy sự gia tăng về việc sử dụng một số kiến trúc API khác.

Nhìn vào báo cáo thì có thể thấy một vài kiến trúc khác như MQTT, AMQP, Server-Sent Events, EDI/EDA. Tuy nhiên chúng không quá phổ biến và chỉ ứng dụng vào những hệ thống đặc thù nên mình sẽ không nhắc tới ở đây.

Mong rằng, bài viết này có thể giúp bạn hình dung được các kiến trúc API phổ biến khác ngoài kiến trúc REST đã quá quen thuộc, nhờ đó mà có thể đưa ra lựa chọn phù hợp cho hệ thống của bạn trong tương lai 😄

Cảm ơn mọi người đã dành thời gian theo dõi bài viết này 🙇

-----
Tham khảo:
- [API và những kiến trúc API phổ biến](https://zodinet.com/api-va-nhung-kien-truc-api-pho-bien/)
- []()