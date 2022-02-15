---
layout: post
title: Giới thiệu Celery
subtitle: Distributed Task Queue

tags:
- Celery
- Queue
- background jobs
- asynchronous task
---

Celery là một open source asynchronous task queue or job queue. Nó dễ sử dụng, bạn không cần phải nắm quá rõ để sử dụng được nó. Celery được thiết kế có khả năng mở rộng, tích hợp với nhiều ngôn ngữ và có riêng phần quản lý


## 1. Chọn Message Broker

Message broker là nền tảng trung gian giúp giao tiếp giữa 2 ứng dụng. Với Celery, bạn có nhiều lựa chọn:

#### RabbitMQ
Tính năng hoàn chỉnh, ổn định, bền bỉ và dễ dàng cài đặt là nhưng điều kiện để lựa chọn RabbitMQ. Để cài đặt RabbitMQ chạy lệnh sau:

```bat
$ sudo apt-get install rabbitmq-server
```

Sau khi cài đặt xong thì RabbitMQ sẽ chạy ở chế độ background cùng một message:
```bat
Starting rabbitmq-server: SUCCESS
```

#### Redis
Điểm trừ của Redis so với RabbitMQ là có thể mất data nếu bị dừng đột ngột do lỗi nào đó hoặc mất điện.

```bat
$ wget http://download.redis.io/redis-stable.tar.gz
$ tar xvzf redis-stable.tar.gz
$ cd redis-stable
$ make
```

#### Other brokers
Cũng có thể chọn những dịch vụ Message broker khác từ [Amason SQS](https://docs.celeryproject.org/en/latest/getting-started/backends-and-brokers/sqs.html). Đây là [danh sách các broker](https://docs.celeryproject.org/en/latest/getting-started/backends-and-brokers/index.html) được hỗ trợ trong Celery



-----
Tham khảo:
- [http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html)