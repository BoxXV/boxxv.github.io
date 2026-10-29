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
- [Tham khảo](#tham-khảo)
  - [Lỗi `ERR_CERT_COMMON_NAME_INVALID` và SAN](#lỗi-err_cert_common_name_invalid-và-san)
  - [Tự tạo CA nội bộ và cert bằng openssl](#tự-tạo-ca-nội-bộ-và-cert-bằng-openssl)
  - [Let's Encrypt và chứng chỉ cho IP](#lets-encrypt-và-chứng-chỉ-cho-ip)
  - [Cài Root CA lên máy Client](#cài-root-ca-lên-máy-client)
  - [Firewall Windows](#firewall-windows)
  - [Node.js, Express và HTTP header bảo mật](#nodejs-express-và-http-header-bảo-mật)
- [Kết luận](#kết-luận)


# Tổng quan

Việc bật `HTTPS` cho localhost trong môi trường phát triển Node.js của bạn bao gồm việc tạo chứng chỉ `SSL` và cấu hình máy chủ Node.js để sử dụng chúng. HTTPS, viết tắt của **Hypertext Transfer Protocol Secure**, bổ sung một lớp bảo mật cho việc giao tiếp qua Internet. Bằng cách chạy máy chủ HTTPS trên máy tính cục bộ, bạn có thể tái tạo môi trường được bảo vệ. Giao thức SSL (Secure Socket Layer) hoặc TLS (Transport Layer Security) cung cấp một phương thức giao tiếp an toàn qua internet.

Trong bài viết này, tôi sẽ hướng dẫn bạn cách cấu hình HTTPS cho việc phát triển cục bộ bằng Node.js cho giao diện người dùng. Phương pháp này cũng áp dụng cho React và Express.

![TLS vs SSL](/img/2026/TLS_-Transport-Layer-Security-and-Its-Importance-in-Web-Security.png "TLS vs SSL")


# Cấu hình HTTPS cho Localhost

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


# Tham khảo

## Lỗi `ERR_CERT_COMMON_NAME_INVALID` và SAN
- [Chrome Deprecates Subject CN Matching](https://textslashplain.com/2017/03/10/chrome-deprecates-subject-cn-matching/), Eric Lawrence, 03/2017: từ Chrome 58, tên máy chủ chỉ được so với trường SAN, trường CN bị bỏ qua. Bài giải thích vì sao lỗi `COMMON_NAME_INVALID` gây hiểu nhầm.
- [Remove: Support for commonName matching in certificates](https://groups.google.com/a/chromium.org/g/security-dev/c/IGT2fLJrAeo), Chrome không còn hỗ trợ commonName matching trong certificates, cụ thể là nó còn đòi thêm 1 subjectAltName từ tháng 1 2017.
- [x509v3_config](https://docs.openssl.org/3.2/man5/x509v3_config/), tài liệu OpenSSL: cú pháp `subjectAltName = IP:192.168.7.1` hoặc `DNS:...`, hỗ trợ IPv4 và IPv6.

## Tự tạo CA nội bộ và cert bằng openssl
- [Generate a self-signed server and client certificates with OpenSSL](https://docs.devolutions.net/rdm/kb/general-knowledge/secure-self-signed-certificates/), Devolutions: tạo Root CA, ký cert, cài CA lên server và client. Bài này chỉ đặt CN, không có SAN hay IP, nên cần kết hợp với tài liệu OpenSSL ở trên.
- [LAN SSL Certificates](https://kb.unixservertech.com/software/openssl/internalca/lan), unixservertech: quy trình dùng CA riêng cho dịch vụ trong mạng LAN. Bài này cũng không đề cập IP hay SAN.
- [mkcert](https://github.com/FiloSottile/mkcert): công cụ tạo cert tin cậy cục bộ, hỗ trợ IP (ví dụ `127.0.0.1`). README cảnh báo `rootCA-key.pem` cho toàn quyền chặn lưu lượng HTTPS, cùng nguyên tắc với `ca.key` của dự án. Chỉ nên dùng cho máy Dev.

## Let's Encrypt và chứng chỉ cho IP
- [We've Issued Our First IP Address Certificate](https://letsencrypt.org/2025/07/01/issuing-our-first-ip-address-certificate), 07/2025, cập nhật 15/01/2026: chứng chỉ cho IP đã phát hành chính thức. Chỉ xác thực bằng `http-01` hoặc `tls-alpn-01`, hạn khoảng 6 ngày, không dùng được DNS challenge.

## Cài Root CA lên máy Client
- [Distribute certificates to Windows devices using Group Policy](https://learn.microsoft.com/nl-nl/windows-server/identity/ad-cs/distribute-certificates-group-policy/), Microsoft Learn: các bước import vào Trusted Root Certification Authorities bằng GPO.
- [certutil](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/certutil): cú pháp `-addstore` và `-hashfile`.
- [Set up Certificate Authorities (CAs) in Firefox](https://support.mozilla.org/en-US/kb/setting-certificate-authorities-firefox): bật `security.enterprise_roots.enabled`, hoặc dùng policy `ImportEnterpriseRoots`.
- [About upcoming limits on trusted certificates](https://support.apple.com/en-qa/102028), Apple: giới hạn 398 ngày không áp dụng cho cert cấp từ Root CA do người dùng hoặc quản trị viên thêm. Cert nội bộ 730 ngày của dự án vì vậy không bị ảnh hưởng.

## Firewall Windows
- [New-NetFirewallRule](https://learn.microsoft.com/en-us/powershell/module/netsecurity/new-netfirewallrule): tham số `-RemoteAddress` nhận IP, subnet (`/16`), dải hoặc từ khóa; `-Profile` nhận `Domain`, `Private`, `Public`. Đây là các tham số `setup-firewall.ps1` đang dùng.

## Node.js, Express và HTTP header bảo mật
- [Node.js: TLS](https://nodejs.org/api/tls.html): có `server.setSecureContext(options)` để nạp lại cert mà không ngắt kết nối đang có (từ v11.0.0). Tính năng "Nạp lại chứng chỉ" của dự án dựa trên hàm này.
- [Node.js: Crypto, class X509Certificate](https://nodejs.org/api/crypto.html#class-x509certificate): các hàm `checkIP`, `checkHost`, `checkPrivateKey` dùng trong `ssl.js` và `check-cert.js`. Trang quá dài nên tôi chưa đọc phần mô tả chi tiết; tôi đã chạy thử các hàm này trên file thật.
- [Production Best Practices: Security](https://www.expressjs.com/en/advanced/best-practice-security.html), Express: khuyến nghị dùng TLS và Helmet.
- [Strict-Transport-Security header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Strict-Transport-Security), MDN: "an IP address cannot be an HSTS host", nên HSTS chỉ có tác dụng khi truy cập bằng hostname.
- [Transport Layer Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html), OWASP: phiên bản giao thức, khóa mạnh, HSTS và chọn CA phù hợp.
- [Security/Server Side TLS](https://wiki.mozilla.org/Security/Server%20Side%20TLS), Mozilla: cấu hình TLS khuyến nghị, tôi chỉ xác nhận tiêu đề từ kết quả tìm kiếm, chưa mở xem nội dung.

Không tìm được bài tiếng Việt đủ tin cậy về đúng chủ đề này (CA nội bộ, cert có SAN cho IP), nên không đưa vào để tránh dẫn nguồn sai.


# Kết luận

Việc sử dụng mkcert giúp đơn giản hóa quá trình kích hoạt HTTPS trên localhost bằng cách tạo ra một Certificate Authority (CA) cục bộ và tạo các chứng chỉ SSL tự ký. Phương pháp này đảm bảo môi trường phát triển cục bộ an toàn, cho phép bạn thử nghiệm các ứng dụng Node.js qua giao thức HTTPS với quy trình thiết lập tối giản.


-----
Tham khảo:
- [How to Enable HTTPS for Localhost?](https://www.geeksforgeeks.org/node-js/how-to-enable-https-for-localhost/)
- [Hướng dẫn cài đặt OpenSSL trên Windows 10](https://topdev.vn/blog/huong-dan-cai-dat-openssl-tren-windows-10/)
- [Cách làm HTTPS hoạt động trên local trong 5 phút](https://topdev.vn/blog/cach-lam-https-hoat-dong-tren-local-trong-5-phut/)
- [https://github.com/FiloSottile/mkcert](https://github.com/FiloSottile/mkcert)