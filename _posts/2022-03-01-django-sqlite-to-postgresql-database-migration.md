---
layout: post
title: Di chuyển cơ sở dữ liệu Django từ SQLite sang PostgreSQL
subtitle: Django SQLite to PostgreSQL database migration

tags:
- Django
- SQLite
- PostgreSQL
- migration
- database
---

Xin chào tất cả, trong bài viết này, tôi sẽ hướng dẫn các bạn cách di chuyển dữ liệu từ SQLite sang Postgres.

Các bước là:
1. Sao lưu toàn bộ dữ liệu kết xuất dữ liệu SQLite trong DB
2. Tạo Postgres DB với người dùng và mật khẩu
3. Thay đổi settings.py
4. Nhập cố định bằng cách sử dụng dữ liệu tải


## 1. Sao lưu toàn bộ dữ liệu SQLite.



Như vậy là xong rồi đó. Chúc các bạn thành công.

-----
Tham khảo:
- [Configure PostgreSQL to allow remote connection](https://www.bigbinary.com/blog/configure-postgresql-to-allow-remote-connection)
- [Cấu hình để kết nối với PostgreSQL từ bên ngoài](https://dangxuanduy.com/database/cau-hinh-de-ket-noi-voi-postgresql-tu-ben-ngoai/)
- [Khởi động PostgreSQL server](https://dangxuanduy.com/database/khoi-dong-postgresql-server/)
- [Cấu hình kết nối trong PostgreSQL với pg_hba.conf](https://dangxuanduy.com/database/cau-hinh-chinh-sach-ket-noi-trong-postgresql-voi-pg-hba_conf/)
- [Kết nối vào server Linux bằng ssh tool](https://dangxuanduy.com/lap-trinh/bash-shell/ket-noi-vao-server-linux-bang-ssh-tool/)
- [Review công cụ quản trị PostgreSQL – DBeaver](https://dangxuanduy.com/database/review-cong-cu-quan-tri-postgresql-dbeaver/)
- [Kho tài liệu kiến thức Database](https://www.facebook.com/groups/khotailieukienthucdatabase)