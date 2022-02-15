---
layout: post
title: Tìm hiểu về Celery
subtitle: Distributed Task Queue

tags:
- Celery
- Queue
- background jobs
- asynchronous task
---

Trong dự án hiện tại của mình khi tới phần scaling hệ thống thì kiến trúc hiện tại theo hướng microservice gặp phải một vấn đề: mọi service trong hệ thống đều tương tác trực tiếp với database nên xảy ra vấn đề càng nhiều service thì càng nhiều kết nối tới database dẫn đến tình trạng xảy ra deadlock, performance cũng rất chậm do các kết nối tới database từ các service phải chờ nhau giải phóng.

Sau khi được gợi ý về việc chuyển sang dùng hàng đợi thay vì để các service thao tác trực tiếp với database, mình có dành thời gian tìm hiểu thêm về kiến trúc Queue. Do dự án chạy chủ yếu bằng python nên tech lead gợi ý sử dụng Celery, một hệ thống quản lý queue phổ biến.

Kiến trúc sau khi chuyển sang sử dụng queue trong hệ thống của mình sẽ như sau. Một bài viết khá chi tiết về một dạng thiết kế queue là message queue mọi người có thể đọc thêm ở [toidicodedao](https://toidicodedao.com/2019/10/08/message-queue-la-gi-ung-dung-microservice/)

## 1. Chọn Message Broker

Message broker là nền tảng trung gian giúp giao tiếp giữa 2 ứng dụng. Với Celery, bạn có nhiều lựa chọn:

### RabbitMQ
Tính năng hoàn chỉnh, ổn định, bền bỉ và dễ dàng cài đặt là nhưng điều kiện để lựa chọn RabbitMQ.

Nếu bạn đang sử dụng Ubuntu hoặc Debian, hãy cài đặt RabbitMQ bằng cách thực hiện lệnh này:
```bat
$ sudo apt-get install rabbitmq-server
```

Hoặc, nếu bạn muốn chạy nó trên Docker, hãy thực hiện điều này:
```bat
$ docker run -d -p 5672:5672 rabbitmq
```

Sau khi cài đặt xong thì RabbitMQ sẽ chạy ở chế độ background cùng một message: `Starting rabbitmq-server: SUCCESS`


### Redis
Điểm trừ của Redis so với RabbitMQ là có thể mất data nếu bị dừng đột ngột do lỗi nào đó hoặc mất điện.

```bat
$ wget http://download.redis.io/redis-stable.tar.gz
$ tar xvzf redis-stable.tar.gz
$ cd redis-stable
$ make
```

Nếu bạn muốn chạy nó trên Docker, hãy thực hiện điều này:
```bat
$ docker run -d -p 6379:6379 redis
```


### Other brokers
Cũng có thể chọn những dịch vụ Message broker khác từ [Amason SQS](https://docs.celeryproject.org/en/latest/getting-started/backends-and-brokers/sqs.html). Đây là [danh sách các broker](https://docs.celeryproject.org/en/latest/getting-started/backends-and-brokers/index.html) được hỗ trợ trong Celery


## 2. Cài đặt
Có thể cài đặt Celery dễ dàng qua `pip` hoặc `easy_install` hoặc `conda`:
```bat
$ pip install celery
```

```bat
$ conda install -c conda-forge celery
```

## 3. Application
Tạo một file `tasks.py` trong thư mục dự án:

```python
from celery import Celery

app = Celery('tasks', broker='pyamqp://guest@localhost//')

@app.task
def add(x, y):
    return x + y
```

_Giải thích_: Đối số đầu tiên của *Celery* là tên của module. Việc đặt tên này sẽ cần thiết cho việc tạo tự động các task được định nghĩa trong hàm `__main__`

Đối số thứ 2 là keyword cho broker, nếu chọn Redis thì thay đổi giá trị thành `redis://localhost`

Sau đó, defined một task có tên `add` nhận 2 tham số đầu vào và trả về tổng giá trị của chúng


## 4. Chạy Celery worker server
Chạy câu lệnh sau:

```bat
$ celery -A tasks worker --loglevel=info
```

Để Celery chạy nền thì cần follow theo các bước sau:

Step 1: Cài đặt `supervisord` qua `apt-get`

Step 2: Tạo file: `/etc/supervisor/conf.d/celery.conf` và thêm vào nội dung sau
```bat
[program:celery]
directory = /my_project/
command = /usr/bin/python manage.py celery worker
```

Step 3: Khởi động lại `supervisor` và sau đó sử dụng các câu lệnh sau
```bat
$ supervisorctl start/restart/stop celery
$ supervisorctl tail [-f] celery [stderr]
```

## 5. Call task

Để call một task, bạn có thể sử dụng method `delay()`
```bat
>>> from tasks import add
>>> add.delay(4, 4)
```

Sau khi gọi method trên, task vụ được đưa vào thực hiện và bạn có thể confirm tại màn hình console log lúc chạy `Celery` server. Khi gọi hàm trên thì bạn sẽ được trả về một `AsyncResult`. Bạn có thể sử dụng `AsyncResult` để kiểm tra trạng thái của task mình vừa add vào, đợi task hoàn thành hoặc nhận giá trị trả về của task(có thể nhận được ngoại lệ và traceback)


## 6. Lưu giữ Result

Mặc định, Celery sẽ không trả về `AsyncResult` nếu không được cấu hình. Để nhận được kết quả khi chạy task bạn cần khai báo như sau:
```python
app = Celery('tasks', backend='rpc://', broker='pyamqp://')
```

Trong đó param `backend` là nơi bạn muốn lưu trữ, ví dụ như: `SQLAlchemy/Django ORM, Memcached, Redis, RPC (RabbitMQ/AMQP)...` Nếu muốn sử dụng Redis thay thế giá trị của param `backend` thành `redis://localhost`. Ok, sau khi cấu hình xong, chạy lại server và thử lại với câu lệnh trên:

```bat
>>> result = add.delay(4, 4)
>>> result.ready()
False
>>> result.get(timeout=1)
8
```

Nếu muốn handle ngoại lệ, bạn có thể dùng
```bat
>>> result.traceback
```

Thông tin có nhiều hơn tại [celery.result](https://docs.celeryproject.org/en/latest/reference/celery.result.html#module-celery.result)


## 7. Kết luận
Mình vừa giới thiệu cho các bạn về `Celery`, cách cài đặt và demo đơn giản. Hẹn gặp lại các bạn ở những phần nâng cao của Celery.


-----
Tham khảo:
- [Tìm hiểu về Celery](https://viblo.asia/p/tim-hieu-ve-celery-1VgZv4dr5Aw)
- [Giới thiệu Celery](https://viblo.asia/p/gioi-thieu-celery-maGK7mvBlj2)
- [First Steps with Celery](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html)
- [First steps with Django](http://docs.celeryproject.org/en/latest/django/first-steps-with-django.html)
- [Learn Django Celery](https://www.youtube.com/playlist?list=PLOLrQ9Pn6caz-6WpcBYxV84g9gwptoN20)
- [the guide of Celery Redis Django](https://www.codingforentrepreneurs.com/blog/celery-redis-django/)
- [Asynchronous Tasks With Django and Celery](https://realpython.com/asynchronous-tasks-with-django-and-celery/)

- [https://github.com/ebysofyan/django-celery-progress-sample](https://github.com/ebysofyan/django-celery-progress-sample)
- [https://github.com/jessamynsmith/django-celery-example](https://github.com/jessamynsmith/django-celery-example)
- [https://github.com/engineervix/django-celery-sample](https://github.com/engineervix/django-celery-sample)
- [https://github.com/Gabriel-Gardin/celery_django](https://github.com/Gabriel-Gardin/celery_django)
- [https://github.com/reouno/django-task-queue](https://github.com/reouno/django-task-queue)
- [https://github.com/Hassanzadeh-sd/Django-Celery](https://github.com/Hassanzadeh-sd/Django-Celery)