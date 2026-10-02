---
layout: post
title: "Cấu hình SSL HTTPS cho Localhost trong Node.js"
subtitle: "Config SSL HTTPS Localhost For Node.JS"
date: 2026-10-01 10:11:12
tags:
- SSL
- HTTPS
- Localhost
- Nodejs
---

- [Tổng quan](#tổng-quan)
- [Cấu hình HTTPS cho Localhost](#cấu-hình-https-cho-localhost)
- [Kết luận](#kết-luận)


## Tổng quan

Việc bật `HTTPS` cho localhost trong môi trường phát triển Node.js của bạn bao gồm việc tạo chứng chỉ `SSL` và cấu hình máy chủ Node.js để sử dụng chúng. HTTPS, viết tắt của **Hypertext Transfer Protocol Secure**, bổ sung một lớp bảo mật cho việc giao tiếp qua Internet. Bằng cách chạy máy chủ HTTPS trên máy tính cục bộ, bạn có thể tái tạo môi trường được bảo vệ. Giao thức SSL (Secure Socket Layer) hoặc TLS (Transport Layer Security) cung cấp một phương thức giao tiếp an toàn qua internet.

Trong bài viết này, tôi sẽ hướng dẫn bạn cách cấu hình HTTPS cho việc phát triển cục bộ bằng Node.js cho giao diện người dùng. Phương pháp này cũng áp dụng cho React và Express.

![TLS vs SSL](/img/2026/TLS_-Transport-Layer-Security-and-Its-Importance-in-Web-Security.png "TLS vs SSL")


## Cấu hình HTTPS cho Localhost

Để bật HTTPS trên localhost, hãy tạo chứng chỉ SSL tự ký bằng **OpenSSL**. Cài đặt **mkcert**, tạo Certificate Authority (CA) cục bộ bằng lệnh `mkcert create-ca`, sau đó tạo chứng chỉ SSL tự ký cho localhost bằng lệnh `mkcert create-cert`. Cấu hình máy chủ Node.js của bạn với chứng chỉ và khóa đã tạo cho HTTPS.

**Bước 1:** Cài đặt gói mkcert ở chế độ toàn cục.

mkcert là một gói npm dùng để tạo các chứng chỉ tự ký phục vụ cho quá trình phát triển. Nó có thể được sử dụng để tạo và cài đặt chứng chỉ CA (Certificate Authority) cục bộ cho máy chủ.

```bat
npm install -g mkcert
```


**Bước 2:** Tạo chứng chỉ SSL.

Mở cửa sổ dòng lệnh với quyền quản trị viên. Lần lượt chạy hai lệnh dưới đây trong cửa sổ dòng lệnh.

```bash
mkcert create-ca
mkcert create-cert

mkcert create-ca --validity 36500
mkcert create-cert --validity 36500

mkcert 192.168.20.136

npx mkcert-cli --outDir . --cert server.crt --key server.key --host localhost --host 192.168.20.53
npx mkcert-cli --outDir . --cert server.crt --key server.key --host localhost --host 192.168.20.136
```

![Make Certificate](/img/2026/Make-Certificate.png "Tạo chứng chỉ SSL")


**Bước 3:** Sau khi thực thi thành công hai lệnh trên, bạn sẽ thấy bốn tệp tin được tạo ra trong thư mục nơi các lệnh được thực thi, với mỗi lệnh tạo ra hai tệp tin.

```bash
ca.crt
ca.key
cert.crt
cert.key
```

**Bước 4:** Nhấp đúp vào tệp `ca.cert` và nhấp vào Cài đặt chứng chỉ.

![Certificate Information](/img/2026/Certificate_Information.png "Cài đặt chứng chỉ")

> Lưu ý: Lệnh này tạo nhanh một chứng chỉ có hiệu lực trong **365 ngày**


**Bước 5:** Chọn tùy chọn `Local Machine` rồi nhấn nút **Next**.

![Certificate Information](/img/2026/Certificate_import_wizard_1.png "Cài đặt chứng chỉ")


**Bước 6:** Chọn tùy chọn `Place all certificates in the following store` (Đặt tất cả chứng chỉ vào kho lưu trữ sau), sau đó chọn mục `Trusted Root Certification Authorities`. Cuối cùng, nhấp vào **Next** để tiếp tục.

![Certificate Information](/img/2026/Certificate_import_wizard_2.png "Cài đặt chứng chỉ")


**Bước 7:** Nhấn vào **Finish** và chờ thông báo `Import successful` (Nhập dữ liệu thành công) xuất hiện. Khi thông báo hiện ra, hãy nhấn **OK** để hoàn tất quá trình nhập dữ liệu.

![Certificate Information](/img/2026/Certificate_import_wizard_3.png "Cài đặt chứng chỉ")


**Bước 8:** Xác nhận rằng thông tin chứng chỉ khớp với các chi tiết được cung cấp bên dưới. Sau khi xác minh, hãy nhấp vào **OK** để tiếp tục.


**Bước 9:** Cập nhật lệnh khởi động trong phần `scripts` của tệp `package.json` như sau:

```
"start": "set HTTPS=true&&set SSL_CRT_FILE=C:/Windows/System32/cert.crt&&set SSL_KEY_FILE=C:/Windows/System32/cert.key&&react-scripts start",
```

**Bước 10:** Khởi động ứng dụng React của bạn bằng lệnh này.

```bash
npm start
```


## Kết luận

Việc sử dụng mkcert giúp đơn giản hóa quá trình kích hoạt HTTPS trên localhost bằng cách tạo ra một Certificate Authority (CA) cục bộ và tạo các chứng chỉ SSL tự ký. Phương pháp này đảm bảo môi trường phát triển cục bộ an toàn, cho phép bạn thử nghiệm các ứng dụng Node.js qua giao thức HTTPS với quy trình thiết lập tối giản.


-----
Tham khảo:
- []()
- [How to Enable HTTPS for Localhost?](https://www.geeksforgeeks.org/node-js/how-to-enable-https-for-localhost/)
- [Hướng dẫn cài đặt OpenSSL trên Windows 10](https://topdev.vn/blog/huong-dan-cai-dat-openssl-tren-windows-10/)
- [Cách làm HTTPS hoạt động trên local trong 5 phút](https://topdev.vn/blog/cach-lam-https-hoat-dong-tren-local-trong-5-phut/)
- [https://github.com/FiloSottile/mkcert](https://github.com/FiloSottile/mkcert)
- []()