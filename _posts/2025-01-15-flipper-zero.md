---
layout: post
title: Flipper Zero - một công cụ hacking thật tuyệt vời
subtitle: Multi-tool Device for Geeks
date: 2025-01-15 11:00:00
tags:
- Flipper Zero
- hacking
- Multi-tool
---

- [1. Giới thiệu về Flipper Zero​](#1-giới-thiệu-về-flipper-zero)
- [2. Tính năng của Flipper Zero​](#2-tính-năng-của-flipper-zero)
  - [2.1. Tính năng phần cứng​](#21-tính-năng-phần-cứng)
  - [2.2. Tính năng phần mềm​](#22-tính-năng-phần-mềm)
- [3. Hướng dẫn sử dụng Flipper Zero​](#3-hướng-dẫn-sử-dụng-flipper-zero)
  - [3.1. Cài đặt môi trường phát triển​](#31-cài-đặt-môi-trường-phát-triển)
  - [3.2. Lập trình với Flipper Zero​](#32-lập-trình-với-flipper-zero)
  - [3.3. Sử dụng tính năng của Flipper Zero​](#33-sử-dụng-tính-năng-của-flipper-zero)
- [4. Các kịch bản mình đã thử được​](#4-các-kịch-bản-mình-đã-thử-được)
  - [SpamBluetooth​](#spambluetooth)
  - [NFC và RFID​](#nfc-và-rfid)
  - [SUBGHZ](#subghz)
  - [Bad KB​](#bad-kb)
  - [Hồng ngoại​](#hồng-ngoại)
  - [WIFI Hacking​](#wifi-hacking)
  - [Các tính năng khác​](#các-tính-năng-khác)
- [Tổng kết](#tổng-kết)



Trong những ngày vừa qua sau khi được người bạn cho mượn chiếc Flipper Zero để sử dụng mình thấy khá hay và thú vị muốn chia sẻ nhanh cho mọi người.

- Silicone Case for Flipper Zero `$15.00`
- Screen Protectors for Flipper Zero `$7.50`
- WiFi Devboard for Flipper Zero `$29.00`
- Video Game Module for Flipper Zero `$49.00`
- Prototyping Boards for Flipper Zero `$10.00`

## 1. Giới thiệu về Flipper Zero​

![Flipper Zero​](https://boxxv.github.io/img/2025/OIP.jpg "Flipper Zero​")

Flipper Zero là một thiết bị đa chức năng nhỏ gọn và có thể lập trình, được thiết kế để có thể thực hiện nhiều công việc khác nhau trong lĩnh vực an ninh mạng và hacking. Thiết bị này có các tính năng đáng chú ý với nhiều module giao tiếp và khả năng tương tác linh hoạt với nhiều loại thiết bị.

Tuy nhiên thiết bị này đã bị cấm bán trên Amazon và một số nước như Brazil,...Hiện tại ở Việt Nam chưa có nhiều thông tin về việc cấm bán thiết bị này nhưng tính năng quét tần số lại vi phạm dải tần dân sự được sử dụng.


## 2. Tính năng của Flipper Zero​

Một thiết bị nhỏ gọn có thể tùy biến theo cá nhân sử dụng

### 2.1. Tính năng phần cứng​

- Màn hình OLED: Flipper Zero được trang bị một màn hình cảm ứng OLED 128x64 pixels, cho phép hiển thị thông tin và tương tác người dùng trực tiếp trên thiết bị.
- Module giao tiếp đa dạng: Thiết bị có các module giao tiếp như NFC, IR, BLE, và các loại máy quét thẻ, mở ra nhiều cơ hội tương tác với các thiết bị khác.
- Bàn phím và nút bấm: Flipper Zero có bàn phím 6 nút, hỗ trợ thao tác và điều khiển trực tiếp trên thiết bị.
- Kết nối USB-C: Sử dụng cổng USB-C cho việc sạc pin và truyền dữ liệu.

### 2.2. Tính năng phần mềm​

Hỗ trợ lập trình đa ngôn ngữ: Flipper Zero có thể được lập trình bằng C/C++, Python, JavaScript, mở rộng khả năng sử dụng và tùy chỉnh của thiết bị.

Cộng đồng phát triển mở rộng: Có sự hỗ trợ từ cộng đồng phát triển mở rộng các ứng dụng và tính năng mới cho Flipper Zero.


## 3. Hướng dẫn sử dụng Flipper Zero​

### 3.1. Cài đặt môi trường phát triển​

Có nhiều cách để cài đặt môi trường sau khi cầm thiết bị này về tay, bởi lẽ nếu không update firmware thì hoàn toàn không thể sử dụng các tính năng nào cả.

**Cách 1:** Cài đặt trực tiếp từ nhà phát hành Fipper-zero, có trên github hoặc thông qua app qFlipp để sử dụng.

Sau khi trải nghiệm thử ở phiên bản này với người mới vọc vạch thì nó khá đơn giản, hỗ trợ khá ít tính năng, chưa thấy rõ được các chức năng hacking. Có thể do mình chưa tìm hiểu để cài các bản mở rộng khác để hỗ trợ. Tuy nhiên với phong cách mỳ ăn liền mình cũng mày mò đọc các bài bình luận xem có firmware nào khác dành cho nó không, và kết quả cuối cùng cũng có.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 232750.png "Flipper Zero​")

**Cách 2:** Cài đặt trực tiếp thông qua WEB xtremeFlipper

Nhìn chung sau khi cài bản này mình thấy khá phù hợp với người mới được cầm Flipper ở nhiều điểm:

- Giao diện đẹp, có nhiều mode để tùy biến.
- Các tính năng hacking cơ bản cũng có sẵn như Fuzzing NFC, RTFC, Spam Bluetooth,....
- Việc cài đặt không cần tải thêm ứng dụng thứ 3 mà hoàn toàn có thể cài trực tiếp trên WEB
- Không thể sử dụng để có thể điều khiển trên máy tính cá nhân được

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233030.png "Flipper Zero​")

### 3.2. Lập trình với Flipper Zero​

Thông qua việc lập trình, phát triển mã nguồn, các kịch bản tấn công phát tán qua Flipper sẽ làm cho thiết bị như một "con dao".

Tạo dự án mới: Sử dụng SDK để tạo một dự án mới.

Viết mã: Viết mã ứng dụng của bạn trong C/C++ hoặc Python và tương tác với các tính năng của Flipper Zero như module giao tiếp, màn hình OLED, và các nút bấm.

Biên dịch và tải lên thiết bị: Biên dịch mã nguồn và tải chương trình đã biên dịch lên Flipper Zero sử dụng công cụ có sẵn.

### 3.3. Sử dụng tính năng của Flipper Zero​

Kiểm tra bảo mật thiết bị: Sử dụng các module giao tiếp và chức năng của Flipper Zero để kiểm tra bảo mật các thiết bị điện tử.

Quản lý mật khẩu: Sử dụng Flipper Zero để lưu trữ và quản lý mật khẩu an toàn.

Thực hiện các thao tác hacking cơ bản: Sử dụng Flipper Zero để thực hiện các thao tác hacking như thu thập thông tin từ các thiết bị khác.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 232834.png "Flipper Zero​")


## 4. Các kịch bản mình đã thử được​

Do không có GPIO cho nên mình chỉ thử được một phần các chức năng cơ bản. Các module được cài bằng firmware xtreme.

### SpamBluetooth​

Tích hợp cùng với thiết bị cho phép spam các thiết bị bluetooth quanh Flipper, nhưng có vẻ như không có bộ phát cho nên phải để gần thì mới có thể spam được. Các thiết bị có thể bị spam: Iphone, windows, thiết bị samsung,....

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233718.png "Flipper Zero​")

=> Sau khi chạy thử thì với thiết bị iphone12prm của mình đã bị sập nguồn và phải mất khoảng 10p mới có thể trở về hoạt động như bình thường.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233954.png "Flipper Zero​")

### NFC và RFID​

Nhìn chung flipper như một cái máy đọc mã, nó có thể đọc và sao chép, ghi đè, upgrade thẻ của các bạn. Tuy nhiên không phải thẻ nào cũng có thể đọc được ví dụ mình đã thất bại ở 1 số thẻ ngân hàng và nó làm cho thiết bị tự động reboot lại -> có thể đây là 1 cơ chế chống đọc hoặc sao chép.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233239.png "Flipper Zero​")

Không dừng lại ở đó với phôi thẻ mua trên sọp pi đã tích hợp thông tin sau khi đọc thành công, mình có thử upgrade thông tin trên thẻ kết quả trả về là login fail (cơ chế này mình cũng chưa biết tại sao lại thế, các bạn có thể giải thích thêm cho mình).

Ngoài ra có thể fuzzing các thiết bị đọc, điều này hoàn toàn có thể bằng việc thử các địa chỉ lần lượt.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 234711.png "Flipper Zero​")

Nếu bạn hay di chuyển trong các chung cư phải dùng thẻ thì NFC Fuzzer hay RFID Fuzzer cũng khá hay để có thể tự do di chuyển ở các tầng.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233802.png "Flipper Zero​")

### SUBGHZ

Các thiết bị mình có không đảm bảo có thể ghi lại được các tần số hoặc phá sóng các thiết bị như bộ đàm nên cũng chưa chứng thực được.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233736.png "Flipper Zero​")

Nhưng bằng sự tò mò mình đã mượn 1 chiếc smartkey và test cơ chế remote tìm xe vẫn có thể ghi lại được tần số, và thử kích hoạt lại thì ghi nhận như chiếc smartkey thật nhưng chỉ ở chế độ tìm xe và cũng như Bluetooth không có bộ khuếch đại phải đứng gần.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 234444.png "Flipper Zero​")

### Bad KB​

Ở bản firmware xtremeflipper chỉ cung cấp các kịch bản demo và khi cắm cần kích hoạt thông qua thiết bị, đây cũng là sự khác biệt giữ 2 firmware như đề cập ở trên, ở bản qflipper do nhà phát triển tung ra có nhiều kịch bản khở chạy js hơn và hỗ trợ thực thi trên các thiết bị khác:iphone, android, macOs…

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233606.png "Flipper Zero​")

### Hồng ngoại​

Điều khiển các thiết bị hồng ngoại hẳn không còn xa lạ gì nếu bạn sử dụng các thiết bị của xiaomi, thời còn đi học mình hay dùng để điều chỉnh điều hòa hay tắt máy chiếu ở flipper điều này hoàn toàn dễ dàng. Khác với thiết bị điện thoại ở chỗ không cần phải nhập đúng hãng thiết bị mà chỉ cần kích hoạt đợi cho tới khi nó kích hoạt thành công.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 235213.png "Flipper Zero​")

Cái hay của Flipper cho phép bạn có thể tự sao chép tần số hồng ngoại của thiết bị vào flipper để có thể sử dụng nhanh chóng hơn trong các lần sau.

### WIFI Hacking​

Đã đề cập ở ban đầu do không có các broad mở rộng cho nên không sử dụng được, nếu các bạn muốn thử có thể mua trên mạng về để thử, và mình nghĩ đây cũng chính là điểm mạnh của Flipper trong việc fake hoặc sử dụng Flipper để tấn công.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233838.png "Flipper Zero​")

### Các tính năng khác​

Có thể xử dụng Flipper với nhiều các tính năng khác thay vì hacking.

Chơi game trên Flipper tuy nhiên màn hình nhỏ, phím di chuyển khác khó nên trải nghiệm dừng mức độ chơi để biết.

Sử dụng để tạo các loại mã bằng âm thanh.

![Flipper Zero​](https://boxxv.github.io/img/2025/Screenshot 2024-05-15 233819.png "Flipper Zero​")

Ngoài ra cũng nhiều tính năng khi bạn cài qua Github để đi troll bạn bè cũng khá thú vị :))) hãy thử xem nhé.


## Tổng kết

Flipper Zero là một thiết bị độc đáo và mạnh mẽ với nhiều tính năng đa dạng và khả năng tương tác linh hoạt theo như kết quả của các lần sử dụng mình thấy rằng các module hacking hiện tại chủ yếu sử dụng cơ chế bruteforce và chưa có điều đặc biệt gì trong quá trình sử dụng hiện tại có thể khoe với các bạn. Khuyến nghị các bạn sử dụng đúng mục đích thay vì để troll hoặc gây khó chịu cho những người xung quanh.

Việc hướng dẫn sử dụng thiết bị này có thể giúp người dùng tận dụng tối đa các tính năng của nó để kiểm tra bảo mật và thực hiện các thao tác hacking cơ bản. Để biết thêm thông tin chi tiết và hướng dẫn cụ thể, vui lòng truy cập trang web chính thức của Flipper Zero và tham khảo tài liệu hướng dẫn của nhà sản xuất.


-----
Tham khảo:
- [Flipper ZeroMulti-tool Device for Geeks](https://flipperzero.one/)
- [Flipper Zero - một công cụ hacking thật tuyệt vời](https://whitehat.vn/threads/flipper-zero-mot-cong-cu-hacking-that-tuyet-voi.17956/)
- [Cảnh báo sử dụng trái phép Flipper Zero | VTV24](https://youtu.be/X6TxYUGlKtU)
- []()