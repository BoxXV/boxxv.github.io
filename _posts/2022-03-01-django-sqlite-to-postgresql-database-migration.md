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

Trước tiên, bạn cần sao lưu toàn bộ DB bằng lệnh dưới đây

```bat
python manage.py dumpdata > whole.json
```

Trong lệnh này, một số người dùng thường thích sử dụng khóa ngoại tự nhiên và khóa chính nhưng tôi sẽ không đề xuất sử dụng lệnh dưới đây cho đến khi bạn gặp lỗi khi khôi phục dữ liệu (loaddata) vào Postgres

```bat
python manage.py dumpdata — natural-foreign — natural-primary > whole.json
```

Lệnh này sẽ tạo ra `whole.json` trong thư mục gốc của các dự án của bạn, điều này có nghĩa là bạn đã tạo dữ liệu kết xuất từ SQLite ở định dạng cố định JSON.


## 2. Tạo PostgresDB với người dùng và mật khẩu.

Trong bước này, bạn cần cài đặt Postgres trong hệ điều hành của bạn như Ubuntu hoặc mac (google), sau khi cài đặt xong, đăng nhập vào Postgres

```bat
sudo su — postgrespsql

psql
```

Sử dụng lệnh dưới đây để tạo người dùng có mật khẩu và DB và cấp quyền trên DB từ người dùng

```bat
create user hero;
create database my_db;
alter role hero with password ‘my_db@123’;
grant all privileges on database my_db to hero;
alter database my_db owner to hero;
```


## 3. Thay đổi settings.py

```bat
# install this package 
pip install psycopg2
```

`settings.py`

```python
DATABASES = {
	‘default’: {
		‘ENGINE’: ‘django.db.backends.postgresql_psycopg2’,
		‘NAME’: ‘my_db’,
		‘USER’ : ‘hero’,
		‘PASSWORD’ : ‘my_db@123’,
		‘HOST’ : ‘localhost’,
		‘PORT’ : ‘5432’,
	}
}
```

Xóa tất cả các tệp migrations vì chúng tôi không cần tất cả các migrations cũ, thay vào đó, chúng tôi sẽ tạo một tệp migrations cho mỗi ứng dụng. sử dụng lệnh dưới đây để xóa tất cả các tệp di chuyển.

```bat
find . -path “*/migrations/*.py” -not -name “__init__.py” -delete

find . -path “*/migrations/*.pyc” -delete
```

```bat
python manage.py makemigrations
python manage.py migrate
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