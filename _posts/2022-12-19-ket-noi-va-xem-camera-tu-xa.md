---
layout: post
title: Kết nối và xem camera từ xa
subtitle: Giải pháp kết nối camera từ xa về đầu ghi qua internet
image: "img/projects-bg.jpg"
tags:
- máy chấm công
- camera
- attendance machine
- timekeeper
---


## I. Tổng quan

### 1. Cách mở port (NAT port) cho modem Viettel F606, F608, F600w

**Bước 1: Truy cập vào trang quản lý của Modem Viettel**

Bạn vào trình duyệt Web gõ địa chỉ: [http://192.168.1.1](http://192.168.1.1) (Lưu ý: một số trường hợp trang quản lý sẽ có địa chỉ khác, nếu bạn đã đổi IP Default Gateway thì trang quản lý chính là IP Default Gateway đó).

Đăng nhập với ID và password là admin/admin. Nếu không được thì xem dưới đáy của Modem.

![NAT port](https://boxxv.github.io/img/timekeeper/login.png "NAT port")


**Bước 2: Tắt Firewall của modem**

Bạn phải thực hiện việc này thì mới mở được port modem. Bạn thực hiện như sau:

Vào `Security` -> `Firewall` -> click chọn `Low` hoặc `Off` -> xong click `Submit`.

![NAT port](https://boxxv.github.io/img/timekeeper/firewall.png "NAT port")


**Bước 3: Mở port modem**

Cách 1: Mở port nhanh modem của Viettel bằng **DMZ**

Mở port nhanh với `DMZ`, cách này sẽ mở tất cả các port cho IP đó

- Vào menu `Application` -> `DMZ Host` -> click `Enable`, chọn `Wan Connection` là `omci_ipv4_pppoe_1`, nhập IP cần mở port vào ô `DMZ Host IP Address`.
- Click `Submit` để hoàn tất.

![NAT port](https://boxxv.github.io/img/timekeeper/huong-dan-mo-port-modem-viettel-h606-h608-h600w-2.jpg "NAT port")


Cách 2: Mở port bằng **Port Forwarding**

Cách này có thể mở port cho nhiều IP cùng lúc, bạn thực hiện như sau:

- Vào menu `Application` -> `Port Forwarding` -> thực hiện như hình dưới
- Xong click `Add` để hoàn tất
- Thực hiện tương tự với các IP và port tiếp theo cần mở.

![NAT port](https://boxxv.github.io/img/timekeeper/huong-dan-mo-port-modem-viettel-h606-h608-h600w-3.jpg "NAT port")


Kiểm tra xem port modem đã được NAT chưa

Bạn truy cập trang [canyouseeme.org](https://canyouseeme.org) hoặc [https://ping.eu/port-chk](https://ping.eu/port-chk) gõ port mà bạn đã thao tác xem port đó đã được mở chưa:

- Truy cập “ping.eu/port-chk/“, nhập IP WAN muốn check port, ở đây mình check IP WAN hiện tại.
- Nhập port cần check.
- Nhập mã Captcha.
- Nhấn Go để check port.

Nếu website báo open tức là port đã được mở thành công, nếu là Closed tức là mở port thất bại, bạn phải làm lại cho đúng nhé.

![NAT port](https://boxxv.github.io/img/timekeeper/check-port-da-open-chua.jpg "NAT port")


Đã thao tác đúng cách nhưng port vẫn chưa mở?

Bạn đã thao tác đúng hướng dẫn NAT port nhưng port vẫn chưa được mở, bởi vì:
- Những thao tác bạn vừa làm ở trên là những bước để mở port ở tại modem nhà bạn.
- Port ở trên nhà mạng Viettel cũng cần phải được mở.
- Thông thường thì nhà mạng họ mở sẵn tất cả các port, nên bạn chỉ cần mở port modem tại nhà là xong.

Điều cần làm bây giờ là: bạn hãy gọi điện thoại lên tổng đài hỗ trợ của Viettel 18008119 và yêu cầu họ mở port giúp mình nhé.


**Bước 4: Sử Dụng Tên Miền Động DDNS**

Trong Mục `Application` => `DDNS` => Nhập thông Tin => `Submit`

- Service Type : Chọn nhà cung cấp dịch vụ của bạn
- Server : Tự động nhận khi chọn Service Type (Đây là địa chỉ máy chủ phân giải tên miền)
- User : Tài khoản chứa tên miền
- Password : Mật khẩu của tài khoản trên
- Host name : Tên miền bạn đang sử dụng

![NAT port](https://boxxv.github.io/img/timekeeper/8a.jpg "NAT port")


-----
Tham khảo:

- [Giải pháp kết nối máy chấm công và xem camera từ xa qua mạng Internet 3G](https://dienmayvanphong.com/giai-phap-ket-noi-may-cham-cong-va-xem-camera-tu-xa-qua-mang-internet-3g/)
- [Kết nối camera IP từ xa về đầu ghi qua internet](https://youtu.be/gmePuIZLsbg)
- [Camera an ninh có đang hack lại chính bạn?](https://viblo.asia/p/camera-an-ninh-co-dang-hack-lai-chinh-ban-YWOZrA7YKQ0)
- [Rủi ro từ lỗ hổng máy chấm công khi lấy dữ liệu từ xa qua public IP wan và NAT Port](https://azza.vn/rui-ro-tu-lo-hong-may-cham-cong-khi-lay-du-lieu-tu-xa-qua-public-ip-wan-va-nat-port/)
- [Việt Nam chịu tấn công mạng qua IoT nhiều thứ hai thế giới](https://viblo.asia/p/viet-nam-chiu-tan-cong-mang-qua-iot-nhieu-thu-hai-the-gioi-3P0lPO84Zox)
- [Shodan - Công cụ tìm kiếm cho kiểm thử bảo mật](https://viblo.asia/p/shodan-cong-cu-tim-kiem-cho-kiem-thu-bao-mat-924lJJD0lPM)
- [8 lỗi thường mắc phải khi mở port camera](https://youtu.be/fzhEj4IVjxY)
- []()
- [ZKTeco TA Push SDK bộ công cụ tích hợp hoàn hảo cho nhà phát triển giải pháp chấm công](https://smartid.com.vn/zkteco-ta-push-sdk-bo-cong-cu-tich-hop-hoan-hao-cho-nha-phat-trien-giai-phap-cham-cong.html)