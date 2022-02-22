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

Bạn chuyển sang user posgres bằng lệnh

```bat
su - postgres
```

Sau đó kết nối vào PostgreSQL trên localhost bằng lệnh

```bat
psql
psql (13.2)
Type "help" for help.

postgres=#
```

Như vậy là bạn đã kết nối vào PostgreSQL. Tuy nhiên, chỉ có đứng trên localhost bạn mới thực hiện được thôi, còn từ bên ngoài mạng vẫn chưa kết nối được.

Bằng chứng là bạn sử dụng một công cụ để quản lý PostgreSQL như [DBeaver](https://dbeaver.io) để kết nối vào bằng laptop của các bạn thì vẫn không được.

Giờ chúng ta sẽ cần làm theo các bước sau để có thể kết nối được:

## 1. Cấu hình file `postgresql.conf`

Đây là file chứa các tham số cấu hình của PostgreSQL, để tìm được đường dẫn đến file này, các bạn có thể kết nối vào PostgreSQL trên localhost và gõ lệnh `show config_file;`

```bat
postgres=# show config_file;
```

```bat
              config_file               
----------------------------------------
 /var/lib/pgsql/13/data/postgresql.conf
(1 row)
```

Chúng ta sẽ tìm thấy đường dẫn đến file `postgresql.conf`. Mở file đó ra bằng câu lệnh:

```bat
vi /var/lib/pgsql/13/data/postgresql.conf

hoặc

sudo nano /var/lib/pgsql/13/data/postgresql.conf
```

Và tìm đến dòng:
```txt
listen_addresses = 'localhost'
```
và sửa lại thành
```txt
listen_addresses = '*'
```











Chúc bạn viết mã vui vẻ!

-----
Tham khảo:
- [Configure PostgreSQL to allow remote connection](https://www.bigbinary.com/blog/configure-postgresql-to-allow-remote-connection)
- [Cấu hình để kết nối với PostgreSQL từ bên ngoài](https://dangxuanduy.com/database/cau-hinh-de-ket-noi-voi-postgresql-tu-ben-ngoai/)
- [Khởi động PostgreSQL server](https://dangxuanduy.com/database/khoi-dong-postgresql-server/)
- [Kết nối vào server Linux bằng ssh tool](https://dangxuanduy.com/lap-trinh/bash-shell/ket-noi-vao-server-linux-bang-ssh-tool/)
- [Review công cụ quản trị PostgreSQL – DBeaver](https://dangxuanduy.com/database/review-cong-cu-quan-tri-postgresql-dbeaver/)
- [Kho tài liệu kiến thức Database](https://www.facebook.com/groups/khotailieukienthucdatabase)