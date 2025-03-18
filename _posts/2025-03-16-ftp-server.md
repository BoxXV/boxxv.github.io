---
layout: post
title: FileZilla - The free FTP solution
subtitle: Cài đặt mô phỏng FTP server với phần mềm FileZilla Server
date: 2025-03-17 01:00:00
tags:
- FTP
- Server
- internet
- protocol
---

![FTP](https://boxxv.github.io/img/2025/FileZilla-Server-on-Windows.webp "FTP Server")

- [Giới thiệu về FileZilla](#giới-thiệu-về-filezilla)
- [Cài đặt FileZilla Server](#cài-đặt-filezilla-server)
- [Thiết lập cấu hình cho FTP Server](#thiết-lập-cấu-hình-cho-ftp-server)
  - [Bước 1: Tạo FPT Users](#bước-1-tạo-fpt-users)
  - [Bước 2: Tạo đặt chia sẻ thư mục](#bước-2-tạo-đặt-chia-sẻ-thư-mục)
  - [Bước 3: Bảo mật Server của bạn.](#bước-3-bảo-mật-server-của-bạn)
- [Truy cập FileZilla Server và shared folders từ máy khách](#truy-cập-filezilla-server-và-shared-folders-từ-máy-khách)
- [Kết luận](#kết-luận)

# Giới thiệu về FileZilla

FileZilla Server là ứng dụng máy chủ FTP mạnh mẽ và thân thiện với người dùng được thiết kế cho hệ điều hành Windows. Ứng dụng này giúp người dùng dễ dàng chia sẻ tệp và thư mục qua mạng cục bộ hoặc internet. Với bộ tính năng phong phú và giao diện thân thiện với người dùng, FileZilla Server cung cấp một cách an toàn và hiệu quả để quản lý việc truyền tệp. Ứng dụng hỗ trợ các giao thức truyền tệp, bao gồm FTP, FTPS (FTP qua SSL/TLS), SFTP (Giao thức truyền tệp SSH) và HTTP/HTTPS. Ứng dụng này cũng cung cấp các tùy chọn bảo mật mạnh mẽ, chẳng hạn như lọc IP, mã hóa SSL/TLS và kiểm soát quyền truy cập của người dùng, đảm bảo dữ liệu của bạn luôn được bảo vệ. Cho dù bạn là cá nhân hay doanh nghiệp, FileZilla Server là lựa chọn tuyệt vời để thiết lập giải pháp chia sẻ tệp đáng tin cậy và thân thiện với người dùng trên hệ thống Windows của bạn.

Trong bài viết trước mình đã giới thiệu cho các bạn tổng quan về giao thức truyền file FTP và nguyên lý hoạt động của giao thức này. Trong bài viết này mình sẽ hướng dẫn các bạn cài đặt FTP server với phần mềm FileZilla server và cách sử dụng phần mềm FTP client để upload file lên máy chủ.

# Cài đặt FileZilla Server

Bước 1: Tải phần mềm [FileZilla Server](https://filezilla-project.org/download.php?type=server) cho Windows (64bit x86).

Bước 2: Khi tải hoàn tất, kích đúp chuột vào “FileZilla_Server_1.9.4_win64-setup.exe” để bắt đầu cài đặt.

Bước 3: Rồi theo sự chỉ dẫn trên màn hình để cài đặt FileZilla Server. Khi bạn đến màn hình bên dưới, chọn cách để khởi động FileZilla Server: Start the Filezilla Server with Windows hoặc là Start Filezilla Server manually rồi.

![FTP Img1](https://boxxv.github.io/img/2025/43bd8a2bd49a65c43c8b.jpg "FTP Server")
![FTP Img2](https://boxxv.github.io/img/2025/0d6ced35b28403da5a95.jpg "FTP Server")
![FTP Img3](https://boxxv.github.io/img/2025/b5aec2cd9a7c2b22726d.jpg "FTP Server")
![FTP Img4](https://boxxv.github.io/img/2025/8d17e6f2be430f1d5652.jpg "FTP Server")
![FTP Img5](https://boxxv.github.io/img/2025/b133b023ea925bcc0283.jpg "FTP Server")
![FTP Img6](https://boxxv.github.io/img/2025/db013ba16110d04e8901.jpg "FTP Server")
![FTP Img7](https://boxxv.github.io/img/2025/ee0a227c79cdc89391dc.jpg "FTP Server")
![FTP Img8](https://boxxv.github.io/img/2025/aa319bfeae4f1f11465e.jpg "FTP Server")
![FTP Img9](https://boxxv.github.io/img/2025/fd17b580b631076f5e20.jpg "FTP Server")
![FTP Img10](https://boxxv.github.io/img/2025/6426b54abbfb0aa553ea.jpg "FTP Server")
![FTP Img11](https://boxxv.github.io/img/2025/76a86c5963e8d2b68bf9.jpg "FTP Server")
![FTP Img12](https://boxxv.github.io/img/2025/1a6eb70fbfbe0ee057af.jpg "FTP Server")
![FTP Img13](https://boxxv.github.io/img/2025/3b9783829533246d7d22.jpg "FTP Server")
![FTP Img14](https://boxxv.github.io/img/2025/50a4817097c1269f7fd0.jpg "FTP Server")

Khi cài đặt kết thúc, chạy ứng dụng FileZilla đã cài đặt , nhấn Connect để bắt đầu thiết lập cấu hình cho FPT Server mới của bạn.

# Thiết lập cấu hình cho FTP Server

## Bước 1: Tạo FPT Users

1. Ở Menu chính, chọn Edit -> Users, nếu bạn muốn tạo 1 loạt các users để truy cập vào FPT Server của bạn, với cùng 1 sự cho phép thì chọn Edit -> Group.
2. Ở hộp thoại User, chọn General, nhấn Add để thêm người dung truy cập vào Server của bạn.
3. Nhập tên User mới để thêm vào, VD: “User21” và nhấn OK.
4. Tích vào ô Password và nhập mật khẩu cho User đó với mục đích bảo mật.

## Bước 2: Tạo đặt chia sẻ thư mục

1. Khi bạn hoàn thành việc thêm Users mới , chọn Shared Folders ở bên trái, nhấn vào Add dưới hộp thoại Shared folders để để chọn xem thư mục nào trong máy tính của bạn sẽ được chia sẻ thông qua FTP.
2. Chọn thư mục sẽ được sử dụng để truy cập và nhấn OK
3. Cuối cùng đặt quyền truy cập người dung cho thư mục đó: ( Đọc, Viết, Xóa , …) rồi nhấn OK

Đến đây bạn đã hoàn thành xong việc cài đặt cấu hình cơ bản cho FTP Server.

## Bước 3: Bảo mật Server của bạn.

Chọn Edit -> Setting.

1. Ở hộp thoại, chọn General Setting: chỉ định 1 cổng khác thay vì cổng 21, ví dụ 54557
2. Ở IP Filter: chỉ định xem địa chỉ IPs nào sẽ được phép truy cập và ko được phép truy cập vào FTP Server. VD: Ở đây IP 192.168.1.121 k được phép truy cập tới Server
3. Cuối cùng bạn có thể làm cho Server bảo mật hơn bằng việc tích Enable the FTP over TLS support và sử dụng private key đặt để mã hóa thông tin.


# Truy cập FileZilla Server và shared folders từ máy khách

Sau khi cài đặt xong FTP Server bạn có thể truy cập và chia sẻ file từ bất kể máy tính trong mạng cục bộ và mạng ngoài bằng việc thực hiện các cách sau.

Nếu muốn truy cập từ 1 máy ngoài, thực hiện các bước sau:

1. Chuyển kết nối FTP tới địa chỉ IP FTP Server's Internal của bạn (and cổng) trên Firewall/Router của bạn
2. Cho phép kết nối FTP trên 1 cổng đã được chỉ định trên Firewall/Router của bạn.
3. Để kết nối tới FTP server qua Internet, bạn phải biết địa chỉ IP Public của mình (http://www.whatismyip.com/). At this case and to make your life easier, it is better to đăng kí 1 tên miền to your Dynamic (Public) IP Address by using a DDNS service (e.g. http://www.noip.com/)

**Truy cập Server từ trình duyệt Internet của bạn**

Mở trình duyệt Internet của bạn, trên thanh bar địa chỉ, nhập Hostname của FTP Server và số hiệu của cổng FTP ( nếu như lúc trước bạn đã thay đổi số hiệu từ 21 sang 1 sô nào đó )

VD: ftp://10.10.56.36:54557

Rồi điền giấy ủy nhiệm theo yêu cầu để đăng nhập vào FTP Server


# Kết luận

Hope it useful for you. Thanks!!!

Chúc bạn thành công!

-----
Tham khảo:
- [Cài đặt mô phỏng FTP server với phần mềm filezila server](https://viblo.asia/p/cai-dat-mo-phong-ftp-server-voi-phan-mem-filezila-server-yMnKMAArK7P)
- [Cách download & đọc file csv từ một FTP, SFTP server](https://viblo.asia/p/cach-download-doc-file-csv-tu-mot-ftp-sftp-server-yMnKMBvjZ7P)
- [FileZilla Server on Windows](https://www.educba.com/filezilla-server-on-windows/)
- []()