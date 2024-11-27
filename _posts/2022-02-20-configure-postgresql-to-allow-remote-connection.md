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
 /etc/postgresql/14/main/postgresql.conf
(1 row)
```

Chúng ta sẽ tìm thấy đường dẫn đến file `postgresql.conf`. Mở file đó ra bằng câu lệnh:

```bat
vi /var/lib/pgsql/13/data/postgresql.conf
vi /etc/postgresql/14/main/postgresql.conf

hoặc

sudo nano /etc/postgresql/14/main/postgresql.conf
```

Và tìm đến dòng:
```txt
listen_addresses = 'localhost'
```
và sửa lại thành
```txt
listen_addresses = '*'
```

Tiếp theo chúng ta sẽ cấu hinh file `pg_hba.conf`

## 2. Cấu hình file `pg_hba.conf`

Đây là file cho phép chúng ta định ra các luật cho phép user, ip được kết nối vào database cụ thể nào. Chúng ta sẽ cấu hình để mọi IP có thể truy cập được vào tất cả database nếu có username và password.

Để tìm được đường dẫn của file `pg_hba.conf`, chúng ta kết nối vào PostgreSQL và chạy lệnh

```bat
postgres=# show hba_file;
```

```bat
              hba_file              
------------------------------------
 /var/lib/pgsql/13/data/pg_hba.conf
 /etc/postgresql/14/main/pg_hba.conf
(1 row)
```

Chúng ta lại mở file pg_hba.conf bằng trình soạn thảo vi

```bat
vi /var/lib/pgsql/13/data/pg_hba.conf

hoặc

sudo nano /etc/postgresql/14/main/pg_hba.conf
```

Và thêm vào dòng sau:
```txt
host    all             all              0.0.0.0/0                       md5
host    all             all              ::/0                            md5

hoặc

host all all 192.168.56.1/24 md5
```


## 3. Khởi động lại PostgreSQL

Bây giờ bạn cần restart lại PostgreSQL để các thay đổi có hiệu lực

```bat
systemctl stop postgresql-14
systemctl start postgresql-14
```


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