---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: Cách thêm và sử dụng Deepseek-r1 trong Visual Studio Code
subtitle: How to Add and Use Deepseek-r1 in Your Visual Studio Code (For Free!)
date: 2025-02-01 11:00:00
tags:
- Deepseek
- Visual Studio Code
---

- [Tại sao lại là Deepseek-r1?](#tại-sao-lại-là-deepseek-r1)
- [Cài đặt Deepseek-r1 trong VS Code?](#cài-đặt-deepseek-r1-trong-vs-code)
  - [Bước 1: Cài đặt Ollama](#bước-1-cài-đặt-ollama)
  - [Bước 2: Tải xuống Deepseek-r1](#bước-2-tải-xuống-deepseek-r1)
  - [Bước 3: Cài đặt tiện ích mở rộng Continue.dev](#bước-3-cài-đặt-tiện-ích-mở-rộng-continuedev)
  - [Bước 4: Cấu hình Deepseek-r1 trong Continue.dev](#bước-4-cấu-hình-deepseek-r1-trong-continuedev)
- [Bạn có thể làm gì với Deepseek-r1?](#bạn-có-thể-làm-gì-với-deepseek-r1)
- [Suy nghĩ cuối cùng](#suy-nghĩ-cuối-cùng)


Cuộc cách mạng AI đang diễn ra và `Deepseek-r1` đang đi đầu. Mô hình ngôn ngữ lớn (LLM) mạnh mẽ này có thể cạnh tranh trực tiếp với các mô hình AI hàng đầu như GPT, vượt trội về khả năng lập luận, mã hóa và giải quyết vấn đề, trong khi vẫn chạy tốt trên chính máy của bạn. Không còn phải phụ thuộc vào các công cụ đám mây đắt tiền nữa. Với Deepseek-r1, bạn sẽ có được một trợ lý mã hóa nhanh chóng, riêng tư và tiết kiệm chi phí, luôn sẵn sàng khi bạn cần.

Sau vô số giờ sử dụng các công cụ như Cursor và các trợ lý AI trả phí khác, tôi quyết định dùng thử Deepseek-r1. Tôi đã khám phá ra một công cụ thay đổi cuộc chơi: tích hợp liền mạch, miễn phí với Visual Studio Code giúp tăng tốc quy trình làm việc của tôi. Bạn đã sẵn sàng để bắt đầu chưa? Hãy để tôi hướng dẫn bạn cách thiết lập từng bước.


## Tại sao lại là Deepseek-r1?

Trước khi đi sâu vào thiết lập, hãy cùng xem lý do tại sao bạn nên cân nhắc sử dụng Deepseek-r1 với tư cách là nhà phát triển:

- Bạn có thể chạy mọi thứ cục bộ trên máy tính của mình mà không cần nhà cung cấp dịch vụ đám mây.
- Nó giúp bạn giải quyết các tác vụ mã hóa phức tạp nhanh hơn và thông minh hơn.
- Nó hoạt động tốt trong việc tạo mã và gỡ lỗi.


## Cài đặt Deepseek-r1 trong VS Code?

Chúng ta hãy tiến hành cài đặt Deepseek-r1 trong môi trường mã hóa Virtual Studio Code của bạn. Để thực hiện, hãy làm theo các bước dưới đây:

### Bước 1: Cài đặt Ollama

Để bắt đầu, bạn sẽ cần `Ollama`, một nền tảng nhẹ cho phép bạn chạy LLM cục bộ. Ollama là xương sống của thiết lập Deepseek-r1 của bạn vì nó sẽ cho phép bạn quản lý và chạy Deepseek-r1 dễ dàng trên máy tính của bạn.

Để cài đặt Ollama, hãy truy cập trang web chính thức của [Ollama](https://ollama.com) và tải xuống phiên bản dành cho hệ điều hành của bạn. Sau đó, hãy xem hướng dẫn cài đặt để bắt đầu và chạy.

![Deepseek](https://boxxv.github.io/img/2025/m7uwvc1hi54fgriqvm64.png "Deepseek")

### Bước 2: Tải xuống Deepseek-r1

Sau khi cài đặt Ollama, đã đến lúc đưa Deepseek-r1 vào môi trường mã hóa của bạn. Mở terminal và chạy lệnh bên dưới:

```bash
ollama pull deepseek-r1
```

> Việc cài đặt này có thể mất một chút thời gian, nhưng bạn phải kiên nhẫn.

Lệnh trên sẽ tải mô hình Deepseek-r1 xuống máy tính cục bộ của bạn.

![Deepseek](https://boxxv.github.io/img/2025/bley3tcc9v1an7z3yahu.png "Deepseek")

Sau khi tải xuống hoàn tất, hãy kiểm tra bằng một truy vấn đơn giản để đảm bảo mọi thứ hoạt động. Chạy deepseek-r1 bằng lệnh:

```bash
ollama run deepseek-r1
```

Và thêm lời nhắc kiểm tra của bạn:

![Deepseek](https://boxxv.github.io/img/2025/6yl8ll5ib58nl9obgsnl.png "Deepseek")

### Bước 3: Cài đặt tiện ích mở rộng Continue.dev

Bây giờ, hãy đưa Deepseek-r1 vào Visual Studio Code. Đối với điều này, chúng ta sẽ sử dụng [Continue.dev](http://continue.dev), một tiện ích mở rộng tuyệt vời kết nối VS Code với các LLM như Deepseek-r1. Tiện ích mở rộng này sẽ hoạt động như một cầu nối giữa VS Code và Ollama, cho phép bạn tương tác trực tiếp với Deepseek-r1 trong môi trường mã hóa của mình. Để cài đặt `Continue.dev` Extension, hãy làm theo các bước sau:

1. Mở VS Code và vào Extensions Marketplace.
2. Tìm Continue.dev và nhấn cài đặt.

![Deepseek](https://boxxv.github.io/img/2025/shplvr9guhqd2b3sjp1s.png "Deepseek")

### Bước 4: Cấu hình Deepseek-r1 trong Continue.dev

Sau khi cài đặt Continue.dev, đã đến lúc kết nối nó với Deepseek-r1. Thực hiện theo các bước để cấu hình nó:

- Mở giao diện Continue.dev bằng cách nhấp vào biểu tượng của giao diện này trên Thanh hoạt động của VS Code.
- Tìm nút chọn người mẫu ở góc dưới bên trái của cửa sổ trò chuyện.
- Nhấp vào nút, chọn Ollama làm nền tảng, sau đó chọn Deepseek-r1 từ danh sách các mẫu có sẵn.

![Deepseek](https://boxxv.github.io/img/2025/tm105obzebk2br2g8bzw.png "Deepseek")

Vậy là xong! Bây giờ bạn đã sẵn sàng khai thác sức mạnh của Deepseek-r1 trong quy trình viết mã của mình.


## Bạn có thể làm gì với Deepseek-r1?

Sau khi mọi thứ đã được thiết lập, khả năng của Deepseek-r1 là vô tận trong môi trường lập trình của bạn:

- Nó cung cấp cho bạn những gợi ý thông minh, phù hợp với ngữ cảnh khi bạn nhập.
- Bạn có thể đánh dấu một khối mã và yêu cầu Deepseek-r1 tối ưu hóa hoặc viết lại khối mã đó.
- nếu bạn gặp lỗi, Deepseek-r1 sẽ giúp bạn khắc phục sự cố.
- Bạn có thể chọn bất kỳ đoạn mã nào và nhận được thông tin chi tiết về cách thức hoạt động của đoạn mã đó.

Sau đây là bản demo nhanh về cách Deepseek-r1 hoạt động trong Virtual Studio Code của bạn.

Phần thú vị nhất là bạn:

- Bạn không cần đăng ký hay phí ẩn, chỉ cần sự hỗ trợ AI mạnh mẽ và miễn phí.
- Mọi thứ đều chạy cục bộ, do đó mã của bạn sẽ nằm trên máy của bạn.
- Bạn có thể tùy chỉnh hành vi của Deepseek-r1 để phù hợp với nhu cầu cụ thể của mình.


## Suy nghĩ cuối cùng

Việc tích hợp Deepseek-r1 vào Visual Studio Code đã thay đổi hoàn toàn năng suất làm việc của tôi. Nó nhanh, đáng tin cậy và cực kỳ linh hoạt mà không cần tôi phải tốn công lặn. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay mới bắt đầu, thì thiết lập này đều đáng để khám phá.

Vậy, bạn còn chờ gì nữa? Hãy thử Deepseek-r1 và trải nghiệm tương lai của lập trình ngay hôm nay.

Chúc bạn viết mã vui vẻ! 🚀

-----
Tham khảo:
- [How to Add and Use Deepseek-r1 in Your Visual Studio Code (For Free!)](https://dev.to/fastapplyai/how-to-add-and-use-deepseek-r1-in-your-visual-studio-code-for-free-6n3)
- []()