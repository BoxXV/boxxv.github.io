---
layout: post
title: Cấu hình để kết nối với PostgreSQL từ bên ngoài
subtitle: Configure PostgreSQL to allow remote connection

tags:
- Celery
- Queue
- background jobs
- asynchronous task
- Docker
- PostgreSQL
- Redis
- Supervisor
---

Mặc định, sau khi cài đặt PostgreSQL, bạn chỉ có thể kết nối đến database từ localhost (tức là máy chủ hiện đang cài đặt PostgreSQL)

Tất nhiên là để kết nối được (kể cả trong localhost) bạn phải khởi động PostgreSQL lên trước đó đã nhé.

Bài viết này sẽ hướng dẫn bạn cấu hình để có thể kết nối đến PostgreSQL database từ một máy bên ngoài


## Thử kết nối từ bên ngoài bằng công cụ.

Đầu tiên, bạn cần kết nối đến máy chủ cài đặt PostgreSQL bằng 1 công cụ `ssh` nào đó. Tôi thường dùng **mRemoteNG** hoặc **XShell**









Chúc bạn viết mã vui vẻ!

-----
Tham khảo:
- [Configure PostgreSQL to allow remote connection](https://www.bigbinary.com/blog/configure-postgresql-to-allow-remote-connection)
- [Cấu hình để kết nối với PostgreSQL từ bên ngoài](https://dangxuanduy.com/database/cau-hinh-de-ket-noi-voi-postgresql-tu-ben-ngoai/)
- [Khởi động PostgreSQL server](https://dangxuanduy.com/database/khoi-dong-postgresql-server/)
- [Kết nối vào server Linux bằng ssh tool](https://dangxuanduy.com/lap-trinh/bash-shell/ket-noi-vao-server-linux-bang-ssh-tool/)