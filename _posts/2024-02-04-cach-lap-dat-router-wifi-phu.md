---
layout: post
title: 03 cách lắp đặt Router wifi phụ chi tiết từ A đến Z
subtitle: Dịch ngược mã nguồn
image: "img/2024/router-2048px-7062-2x1-1.webp"
tags:
- Reverse Engineering
---
# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
- [1. Cách lắp đặt Router wifi phụ cùng lớp mạng với Router wifi gốc](#1-cách-lắp-đặt-router-wifi-phụ-cùng-lớp-mạng-với-router-wifi-gốc)
	- [Bước 1: Đặt một địa chỉ IP cho Router wifi phụ](#bước-1-đặt-một-địa-chỉ-ip-cho-router-wifi-phụ)
	- [Bước 2: Lựa chọn chế độ hoạt động cho Router wifi phụ](#bước-2-lựa-chọn-chế-độ-hoạt-động-cho-router-wifi-phụ)
	- [Bước 3: Cài đặt thông tin chi tiết](#bước-3-cài-đặt-thông-tin-chi-tiết)
	- [Bước 4: Kết nối 2 Router với nhau](#bước-4-kết-nối-2-router-với-nhau)
- [2. Cách lắp đặt Router wifi phụ khác lớp mạng với Router wifi chính](#2-cách-lắp-đặt-router-wifi-phụ-khác-lớp-mạng-với-router-wifi-chính)
	- [Bước 1: Cài đặt thông tin của Router phụ](#bước-1-cài-đặt-thông-tin-của-router-phụ)
	- [Bước 2: Kết nối hai Router wifi với nhau](#bước-2-kết-nối-hai-router-wifi-với-nhau)
- [3. Cách lắp đặt 2 Router wifi không dây](#3-cách-lắp-đặt-2-router-wifi-không-dây)
	- [Bước 1: Thiết lập mạng wifi cho Router wifi chính](#bước-1-thiết-lập-mạng-wifi-cho-router-wifi-chính)
	- [Bước 2: Thiết lập IP cố định cho Router phụ](#bước-2-thiết-lập-ip-cố-định-cho-router-phụ)
	- [Bước 3: Thiết lập mạng wifi cho Router phụ](#bước-3-thiết-lập-mạng-wifi-cho-router-phụ)
	- [Bước 4: Kích hoạt tính năng WDS trên Router phụ](#bước-4-kích-hoạt-tính-năng-wds-trên-router-phụ)
	- [Bước 5: Kết nối hai Router với nhau](#bước-5-kết-nối-hai-router-với-nhau)
	- [Bước 6: Kích hoạt tính năng WDS trên Router chính](#bước-6-kích-hoạt-tính-năng-wds-trên-router-chính)
	- [Bước 7: Vô hiệu hóa DHCP Server trên Router phụ](#bước-7-vô-hiệu-hóa-dhcp-server-trên-router-phụ)
- [Tổng kết](#tổng-kết)


# Giới thiệu

Bạn có nhu cầu mở rộng vùng phủ sóng wifi nhưng chưa biết cách lắp đặt thêm Router wifi phụ hay lắp thêm modem wifi phụ? Cách lắp đặt sẽ phụ thuộc vào nhu cầu sử dụng mạng của người dùng mà cân nhắc lắp đặt hai Router theo những mô hình khác nhau.

# 1. Cách lắp đặt Router wifi phụ cùng lớp mạng với Router wifi gốc

Hai Router cùng lớp mạng là mạng lưới kết nối giữa hai thiết bị đó và thông thường sẽ là mạng LAN. Router wifi chính đóng vai trò cấp phát `DHCP` và Router wifi còn lại là điểm phát sóng trung gian giữa Router chính và các thiết bị sử dụng mạng. Hai Router này sẽ được kết nối với nhau bằng dây cáp LAN.

Để lắp đặt thêm Router wifi phụ, mạng lưới nhà bạn cần có sẵn một Router wifi hoặc Modem wifi đã kết nối Internet. Với mô hình này, người dùng có thể dễ dàng quản lý tất cả các thiết bị truy cập mạng mà không phải vào từng web quản trị của từng Router.

Hãy làm theo các bước hướng dẫn sau đây để lắp đặt hai Router wifi cùng lớp mạng:

## Bước 1: Đặt một địa chỉ IP cho Router wifi phụ

Truy cập vào web quản trị mà nhà sản xuất cung cấp, thông thường sẽ là 192.168.1.1 hay 192.168.0.1. Sau đó, vào phần thiết lập LAN, gán cho Router phụ một địa chỉ IP tùy thích. Tuy nhiên địa chỉ IP đó cần phải nằm trong dãy địa chỉ IP mà Router chính cấp phát.

## Bước 2: Lựa chọn chế độ hoạt động cho Router wifi phụ

Mỗi Router sẽ có các chế độ hoạt động khác nhau phụ thuộc vào cách thiết lập của nhà sản xuất. Vì vậy, bạn cần lựa chọn đúng chế độ hoạt động để cả hệ thống Router luôn hoạt động ổn định. Đối với thiết bị có Operation Mode, bạn chỉ cần tắt DHCP Server tại mục WAN Setting. Còn đối với thiết bị phân chia chế độ hoạt động, hãy truy cập vào thẻ Operation Mode và chọn chế độ Access Point hoặc Bridge.

## Bước 3: Cài đặt thông tin chi tiết

Sau khi cài đặt xong địa chỉ IP và chọn chế độ hoạt động phù hợp, tiến hành cài đặt cấu hình các thông tin mạng cho Router. Bạn chỉ cần vào thẻ Wireless, chọn Wireless Settings và điền đầy đủ thông tin như tên, mật khẩu,… Bạn hoàn toàn có thể tự thiết lập cho cả hai băng tần 2.4GHz và 5GHz.

## Bước 4: Kết nối 2 Router với nhau

Để hệ thống Router wifi có thể hoạt động, hãy kết nối Router chính và Router phụ với nhau. Đây là cách cách lắp wifi phụ khá đơn giản và dễ thực hiện. Nếu Router phụ đang hoạt động ở chế độ router nhưng tắt DHCP server, bạn chỉ cần kết nối dây mạng từ cổng LAN trên Router chính tới cổng LAN trên thiết bị phụ. Trường hợp Router đang hoạt động ở chế độ access point, bạn cũng làm tương tự nhưng với cổng WAN. Lúc này cổng WAN của Router phụ không khác gì các cổng LAN còn lại.

# 2. Cách lắp đặt Router wifi phụ khác lớp mạng với Router wifi chính

Hệ thống này sẽ bao gồm hai Router với hai lớp mạng khác nhau. Thông thường là LAN – WAN và cả hai Router đều có khả năng cấp phát DHCP. Hai Router này sẽ tạo lập thành hai không gian mạng độc lập, không phụ thuộc lẫn nhau. Mô hình này được sử dụng tại nơi có mạng lưới phức tạp, phục vụ nhiều nhu cầu sử dụng.

Việc lắp Router wifi khác lớp mạng giúp đường truyền mạng được chia tải đều hơn. Đồng thời tránh được trường hợp Router chính quá tải, dẫn đến tình trạng treo hoặc hỏng cả hệ thống Router. Để lắp đặt 2 Router khác lớp mạng, bạn làm theo các hướng dẫn sau:

## Bước 1: Cài đặt thông tin của Router phụ

**Lựa chọn chế độ hoạt động**: Vào mục Operation Mode và chọn chế độ hoạt động là Router Mode hoặc Gateway Mode để tương thích với Router chính.

**Thiết lập địa chỉ IP cấp phát**: Kết nối điện thoại với mạng wifi của Router chính trước khi tiến hành thay đổi IP của Router phụ. Từ đó xác định dãy địa chỉ IP mà Router chính đang phát. Sau đó, truy cập DHCP Server để xác định địa chỉ IP mà Router phụ đang cấp. Trường hợp địa chỉ IP của cả hai Router wifi trùng nhau, bạn cần thực hiện chuyển đổi lớp mạng.

**Thiết lập các thông số cho mạng wifi**: Truy cập Wireless, chọn Wireless Setting để tiến hành thiết lập các thông số cần thiết như SSID, mật khẩu, thay đổi chế độ mã kênh truyền…

## Bước 2: Kết nối hai Router wifi với nhau

Để kết nối hai Router wifi với nhau, dây mạng bắt buộc phải được đi từ cổng LAN trên Router chính tới cổng WAN của Router phụ. Nếu nối không đúng, Router phụ sẽ không nhận được Internet được truyền tải.

# 3. Cách lắp đặt 2 Router wifi không dây

Hai Router chính – phụ sẽ được kết nối với cùng một lớp mạng qua kết nối không dây qua việc sử dụng tính năng WDS. Đây là cách lắp đặt tiết kiệm nhất khi bạn không tốn chi phí để đi dây cũng như tốn thời gian lắp đặt. Đồng thời cũng giúp ngôi nhà của bạn trông gọn gàng hơn khi không có sự đi dây mạng lằng nhằng. Quá trình lắp đặt Router wifi phụ được triển khai như sau:

## Bước 1: Thiết lập mạng wifi cho Router wifi chính

Chọn mục Wireless sau đó đổi tên và mật khẩu cho Router chính trong thẻ Basic Setting. Và chọn một kênh truyền cố định cho Router chính.

## Bước 2: Thiết lập IP cố định cho Router phụ

Đặt cho Router wifi phụ một địa chỉ IP cố định. Điều này sẽ giúp bạn quản lý thiết bị dễ dàng hơn sau khi kết nối hai Router với nhau. Địa chỉ IP được cài đặt cho Router phụ phải thuộc danh sách dãy địa chỉ IP mà Router chính cấp phát.

## Bước 3: Thiết lập mạng wifi cho Router phụ

Tiếp tục truy cập Wireless Setting để cài đặt các thông số cần thiết cho mạng như tên, mật khẩu. Sau đó, thiết lập kênh truyền của Router phụ cho đồng nhất với Router chính.

## Bước 4: Kích hoạt tính năng WDS trên Router phụ

Bắt buộc phải kích hoạt WDS để hai Router có thể kết nối với nhau qua đường truyền không dây. Chọn mục Enable WDS trong phần cài đặt để kích hoạt tính năng này.

## Bước 5: Kết nối hai Router với nhau

Trên giao diện của tính năng WDS, hãy scan để tìm kiếm mạng của Router wifi chính. Sau đó thiết lập thêm các thông số như mật khẩu, chế độ mã hóa để bảo vệ mạng lưới. Cuối cùng, chọn Save để hoàn thành quá trình kết nối.

## Bước 6: Kích hoạt tính năng WDS trên Router chính

Lặp lại quá trình kích hoạt tại Bước 4 và Bước 5 trên Router chính.

## Bước 7: Vô hiệu hóa DHCP Server trên Router phụ

Cuối cùng, hãy quay lại trình cài đặt của Router phụ dựa vào địa chỉ IP cố định trước đó. Vào mục DHCP Setting và chọn Disable DHCP để vô hiệu hóa tính năng cấp phát IP của Router phụ.

# Tổng kết

Trên đây là 03 cách cài đặt và sử dụng Router wifi phụ mà Nhà An Toàn đã chia sẻ tới người dùng. Hy vọng các kiến thức trong bài sẽ giúp bạn tự lắp đặt và kết nối được hai Router. Nếu vẫn còn băn khoăn, hãy liên hệ ngay với Nhà An Toàn để được tư vấn và hỗ trợ nhanh nhất. 

Chúc bạn thành công!

-----
Tham khảo:
- [Decoding binary data structure](https://reverseengineering.stackexchange.com/questions/15969/decoding-binary-data-structure)
- [Understanding and Decoding a JPEG Image using Python](https://yasoob.me/posts/understanding-and-writing-jpeg-decoder-in-python/)
- [DCode™ – Timestamp Decoder](https://www.digital-detective.net/dcode/)
- [图片的 Metadata 与网站性能优化](https://github.com/shfshanyue/blog/blob/master/web-performance/image-metadata.md)
