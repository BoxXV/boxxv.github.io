---
layout: post
title: "Cập nhật bảo mật quan trọng 2026"
subtitle: "Important Security Update 2026"
date: 2026-10-21 10:11:12
tags:
- PHP2Shell
- CVE-2026-109618
- CVE-2026-109619
- Security
---

- [Tổng quan](#tổng-quan)
- [2026-10-21 \> Node.js — Security Releases](#2026-10-21--nodejs--security-releases)
- [2026-10-20 \> PHP2Shell CVEs - CVE-2026-109618 and CVE-2026-109619](#2026-10-20--php2shell-cves---cve-2026-109618-and-cve-2026-109619)
  - [cPanel \& WHM Release Notes - 138 Change Log](#cpanel--whm-release-notes---138-change-log)
    - [138.0.18](#138018)
      - [2026-10-21](#2026-10-21)
  - [EasyApache 4 25.92](#easyapache-4-2592)
- [Kết luận](#kết-luận)


# Tổng quan

Chỉ trong một ngày, hàng loạt sự kiện an ninh mạng nghiêm trọng đã diễn ra dồn dập trên phạm vi toàn cầu, làm chấn động cả internet thế giới.

Ngày 21 tháng Mười (21/10/2026) vừa qua đã trở thành một mốc lịch sử đối với internet thế giới cũng như ngành an ninh mạng toàn cầu. Chỉ trong một ngày, các bảng tin kỹ thuật liên tục nhảy số với những cảnh báo mức nghiêm trọng cao nhất, khiến giới quản trị hệ thống và lập trình viên gần như không kịp thở.

Không hẹn mà gặp, hàng loạt sự kiện chấn động cùng lúc xuất hiện ở gần như mọi tầng của hạ tầng số. Từ hệ thống cấp chứng thư số, ngân hàng, ngôn ngữ lập trình PHP, kho mã nguồn GitLab, môi trường chạy Node.js, thư viện kết nối AI, nền tảng điện toán đám mây cho đến máy chủ phát nội dung, tất cả cùng phát đi tín hiệu báo động trong một khoảng thời gian rất sát nhau.


# 2026-10-21 > Node.js — Security Releases

Đợt phát hành này sửa 10 lỗ hổng bảo mật khác nhau, áp dụng đồng loạt cho các nhánh `22.x`, `24.x` và `26.x`. Trong đó có 4 lỗ hổng mức độ Cao, bao gồm một lỗi có thể dẫn tới thực thi mã từ xa (RCE). Bản vá cũng cập nhật các thư viện lõi đi kèm Node.js như OpenSSL, SQLite, c-ares và Undici.

| Nhánh Node.js | Phiên bản đã cập nhật |
|---|---|
| **26.x** | **v26.12.1** |
| **24.x (LTS)** | **v24.22.1** |
| **22.x (LTS)** | **v22.23.4** |

Nếu bạn tự cài đặt Node.js trên VPS, máy chủ riêng hoặc container, hãy nâng cấp ngay theo các bước sau:
1. Kiểm tra phiên bản hiện tại bằng `node -v`
2. Nâng cấp lên bản vá tương ứng: v22.23.4, v24.22.1 hoặc v26.12.1.
3. Nếu dùng Docker, cập nhật tag image Node.js trong Dockerfile rồi build và triển khai lại.
4. Khởi động lại ứng dụng (PM2, systemd…) để tiến trình chạy trên phiên bản mới.

| Node.js | Codename | First released | Last updated | Status |
|---|---|---|---|---|
| v26 | - | May 05, 2026 | Oct 21, 2026 | 🟢 Current |
| v25 | - | Oct 15, 2025 | Mar 31, 2026 | 🟠 EOL |
| v24 | Krypton | May 06, 2025 | Oct 20, 2026 | 🔵 LTS |
| v23 | - | Oct 16, 2024 | May 14, 2025 | 🟠 EOL |
| v22 | Jod | Apr 24, 2024 | Oct 20, 2026 | 🔵 LTS |
| v21 | - | Oct 17, 2023 | Apr 10, 2024 | 🟠 EOL |
| v20 | Iron | Apr 17, 2023 | Mar 24, 2026 | 🟠 EOL |
| v19 | - | Oct 17, 2022 | Apr 10, 2023 | 🟠 EOL |
| v18 | Hydrogen | Apr 18, 2022 | Mar 27, 2025 | 🟠 EOL |

![Node.js Supported Versions](/img/2026/schedule.svg "Node.js Supported Versions")



# 2026-10-20 > PHP2Shell CVEs - CVE-2026-109618 and CVE-2026-109619

- **Mức nghiêm trọng**: 9,2/10 điểm theo thang CVSS v4.0
- **CVE-2026-109618**: Việc xử lý lỗi thiếu bộ nhớ có thể làm gián đoạn PHP trong khi dữ liệu yêu cầu nội bộ chỉ được khởi tạo một phần. Quá trình dọn dẹp yêu cầu sau đó có thể coi dữ liệu không hợp lệ là hợp lệ.
- **CVE-2026-109619**: Trạng thái nội bộ do yêu cầu sở hữu có thể tồn tại sau khi bộ nhớ hỗ trợ đã được giải phóng. Một yêu cầu sau đó được xử lý bởi cùng một tiến trình có thể sử dụng trạng thái cũ đó trước khi quá trình khởi tạo thông thường đặt lại trạng thái.
- **Các phiên bản bị ảnh hưởng**: Tất cả các phiên bản PHP từ 5.4 đến 8.5.11
- **Bản vá**: PHP `8.5.12`, `8.4.27`, `8.3.36` và `8.2.35`
    - PHP 8.5: Cần nâng cấp lên phiên bản **8.5.12**
    - PHP 8.4: Cần nâng cấp lên phiên bản **8.4.27**
    - PHP 8.3: Cần nâng cấp lên phiên bản **8.3.36**
    - PHP 8.2: Cần nâng cấp lên phiên bản **8.2.35**
- **Chưa được vá lỗi**: Dự án PHP không phát hành bản vá lỗi cho PHP 8.1 trở xuống, những phiên bản đã hết hạn hỗ trợ.

![PHP Supported Versions](/img/2026/php-supported-versions.png "PHP Supported Versions")

| PRODUCT | AFFECTED VERSIONS | PATCHED VERSIONS |
|---|---|---|
| cPanel & WHM | All supported versions | • 11.110.0.153<br>• 11.134.0.66<br>• 11.136.0.50<br>• 11.138.0.18<br>• WP Squared: 11.138.1.17 |
| cPanel EasyApache4 | PHP 5.0 and later | • ea-php74: 7.4.33-19<br>• ea-php80: 8.0.30-12<br>• ea-php81: 8.1.34-5<br>• ea-php82: 8.2.35<br>• ea-php83: 8.3.36<br>• ea-php84: 8.4.27<br>• ea-php85: 8.5.12 |
| CloudLinux EasyApache4 | PHP 5.0 and later | • ea-php52: 5.2.17-27<br>• ea-php53: 5.3.29-29<br>• ea-php54: 5.4.45-82<br>• ea-php55: 5.5.38-64<br>• ea-php56: 5.6.40-25<br>• ea-php70: 7.0.33-29<br>• ea-php71: 7.1.33-20<br>• ea-php72: 7.2.34-12<br>• ea-php73: 7.3.33-15<br>• ea-php74: 7.4.33-18<br>• ea-php80: 8.0.30-11<br>• ea-php81: 8.1.34-4<br>• ea-php82: 8.2.34-2<br>• ea-php83: 8.3.35-2<br>• ea-php84: 8.4.26-2<br>• ea-php85: 8.5.11-2 |

**Phân biệt:**
- **`ea-php`**: Là package của **EasyApache 4** (MultiPHP Manager) - cả cPanel và CloudLinux đều dùng chung hệ thống này
- **`alt-php`**: Là package của **CloudLinux PHP Selector** (Alternative PHP) - một hệ thống khác cho phép người dùng chọn phiên bản PHP riêng cho từng tài khoản

## cPanel & WHM Release Notes - 138 Change Log

### 138.0.18

#### 2026-10-21

- Fixed CPANEL-57977: Update cpanel-php84 to 8.4.27. Fixes: CVE-2026-109618 and CVE-2026-109619.

## EasyApache 4 25.92

*2026 October 21*

- ea-nodejs22
- ea-php74-meta
- ea-php80-meta
- ea-php81-meta
- ea-tomcat101


# Kết luận

Hiếm có ngày nào trong lịch sử internet thế giới lại xuất hiện dồn dập các sự cố bảo mật và an ninh mạng như ngày 21 tháng Mười vừa qua. Điểm chung dễ thấy nhất trong loạt sự cố này là khóa và thông tin xác thực đang trở thành mục tiêu trung tâm của kẻ tấn công. Với internet hiện đại, nơi mọi dịch vụ đều kết nối và phụ thuộc lẫn nhau, mắt xích yếu nhất mới là yếu tố quyết định độ an toàn của toàn bộ chuỗi.


-----
Tham khảo:
- [cPanel & WHM Release Notes](https://docs.cpanel.net/release-notes/release-notes/)
- [cPanel & WHM Change Log](https://docs.cpanel.net/changelogs/releases/)
- [EasyApache Change Log](https://docs.cpanel.net/changelogs/easyapache-4-change-log-25/)
- []()
- [PHP Supported Versions](https://www.php.net/supported-versions.php)
- [PHP 8.5.12](https://www.php.net/downloads.php?version=8.5) · [Changelog](https://www.php.net/ChangeLog-8.php#8.5.12)
- [PHP 8.4.27](https://www.php.net/downloads.php?version=8.4) · [Changelog](https://www.php.net/ChangeLog-8.php#8.4.27)
- [PHP 8.3.36](https://www.php.net/downloads.php?version=8.3) · [Changelog](https://www.php.net/ChangeLog-8.php#8.3.36)
- [PHP 8.2.35](https://www.php.net/downloads.php?version=8.2) · [Changelog](https://www.php.net/ChangeLog-8.php#8.2.35)
- [PHP source code](https://github.com/php/php-src)
- []()
- [Node.js Releases](https://nodejs.org/en/about/previous-releases)
- [Node.js — Wednesday, October 21, 2026 Security Releases](https://nodejs.org/en/blog/vulnerability/october-2026-security-releases)
- [Thông báo cập nhật Node.js ứng phó loạt lỗ hổng bảo mật tháng 10/2026](https://sudo.vn/blog/thong-bao-cap-nhat-nodejs-ung-pho-loat-lo-hong-bao-mat-thang-102026.html)