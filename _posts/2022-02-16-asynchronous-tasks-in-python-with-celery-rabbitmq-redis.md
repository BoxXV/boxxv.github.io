---
layout: post
title: Asynchronous Tasks với Django, Celery, RabbitMQ và Redis
subtitle: Tác vụ không đồng bộ với Django, Celery, RabbitMQ và Redis

tags:
- Django
- Celery
- Queue
- RabbitMQ
- background jobs
- asynchronous task
- Redis
---

## Giới thiệu
Trong bài viết này, chúng ta sẽ sử dụng Celery, RabbitMQ và Redis để xây dựng một hàng đợi Task phân tán.
Nhưng hàng đợi tác vụ phân tán là gì và tại sao bạn lại tạo hàng đợi này?

Hàng đợi tác vụ phân tán cho phép bạn giảm tải công việc sang một quy trình khác, được xử lý không đồng bộ (khi bạn đẩy công việc lên hàng đợi, bạn không cần chờ đợi) và song song (bạn có thể sử dụng các lõi khác để xử lý công việc).

Vì vậy, về cơ bản nó cung cấp cho bạn khả năng thực thi các tác vụ ở chế độ nền trong khi ứng dụng tiếp tục giải quyết các tác vụ khác.

![Async task architecture](https://boxxv.github.io/img/posts/Django_Celery_Redis.jpg "Async task architecture")


## Các trường hợp sử dụng của hàng đợi công việc

Ví dụ cơ bản và dễ hiểu nhất sẽ là gửi email sau khi người dùng đã đăng ký. Trong trường hợp này, bạn không biết sẽ mất bao nhiêu thời gian để gửi email cho người dùng, nó có thể là 1 ms nhưng cũng có thể nhiều hơn, hoặc đôi khi thậm chí không gửi được, bởi vì, trong những trường hợp này, bạn không chịu trách nhiệm hoặc nói đơn giản là bạn không biết nhiệm vụ sẽ được thực hiện thành công, bởi vì chính một nhà cung cấp khác sẽ làm điều đó cho bạn.

Vì vậy, bây giờ bạn đã có một ý tưởng đơn giản về cách bạn có thể hưởng lợi từ các hàng đợi nhiệm vụ, việc xác định các nhiệm vụ như vậy cũng đơn giản như kiểm tra xem chúng có thuộc một trong các loại sau:

- **Nhiệm vụ của bên thứ ba**: Ứng dụng web phải phục vụ người dùng một cách nhanh chóng mà không cần đợi các hành động khác hoàn thành trong khi tải trang, ví dụ: gửi email hoặc thông báo hoặc tuyên truyền các bản cập nhật cho các công cụ nội bộ (chẳng hạn như thu thập dữ liệu để kiểm tra A/B hoặc ghi nhật ký hệ thống ).
- **Các công việc kéo dài**: Các công việc tốn kém tài nguyên, trong đó người dùng cần đợi trong khi tính toán kết quả của họ, ví dụ: thực thi quy trình công việc phức tạp (quy trình công việc DAG), tạo đồ thị, các tác vụ tương tự Map-Reduce và phân phát nội dung đa phương tiện (video, âm thanh).
- **Nhiệm vụ định kỳ**: Công việc mà bạn sẽ lên lịch để chạy vào một thời điểm cụ thể hoặc sau một khoảng thời gian, ví dụ: tạo báo cáo hàng tháng hoặc trình duyệt web chạy hai lần một ngày.


## Thiết lập các phụ thuộc cho Celery

Celery yêu cầu vận chuyển thông điệp để gửi và nhận tin nhắn. Một số ứng cử viên mà bạn có thể sử dụng làm nhà môi giới tin nhắn là:
- [RabbitMQ](https://www.rabbitmq.com)
- [Redis](https://redis.io)
- [Amazon SQS](https://aws.amazon.com/sqs)

Đối với hướng dẫn này, chúng tôi sẽ sử dụng `RabbitMQ`, bạn có thể sử dụng bất kỳ nhà môi giới tin nhắn nào khác mà bạn muốn (ví dụ: Redis).

Chúng ta cũng nên đề cập đến những gì chúng ta sẽ sử dụng `Redis` bây giờ vì đối với trình vận chuyển tin nhắn mà chúng ta đang sử dụng RabbitMQ.
Khi các tác vụ được gửi đến nhà môi giới và sau đó được thực thi bởi celery worker, chúng tôi muốn lưu trạng thái và cũng để xem các tác vụ nào đã được thực thi trước đó. Để làm được điều đó, bạn sẽ cần một số loại lưu trữ dữ liệu và đối với loại này, chúng tôi sẽ sử dụng Redis.

Đối với các cửa hàng kết quả, chúng tôi cũng có nhiều ứng cử viên:
- AMQP, Redis
- Memcached,
- SQLAlchemy, Django ORM
- Apache Cassandra, Elasticsearch, Riak, v.v.

Để thiết lập các dịch vụ này, chúng tôi sẽ sử dụng docker vì nó rất dễ thiết lập, đó là môi trường riêng biệt và bạn có thể dễ dàng tạo lại môi trường giống như vậy khi bạn có cấu hình (Dockerfile hoặc docker-compos).


### Thiết lập dự án

Hãy bắt đầu một dự án python mới từ đầu. Trước tiên, hãy tạo một thư mục mới, tạo tất cả các tệp cần thiết cho dự án, sau đó khởi tạo môi trường ảo.

```bat
$ touch docker-compose.yml requirements.txt
$ touch tasks.py

# create & activate the virtualenv

$ python -m venv env
$ source env/bin/activate
```

Bây giờ, hãy cài đặt các yêu cầu của dự án từ tệp tests.txt. Đối với dự án này, chúng tôi chỉ cần Celery và Redis.

```bat
pip install celery==5.0.5 redis
```

Bây giờ đã đến lúc định cấu hình trình soạn thảo để chạy RabbitMQ và Redis. Trong **docker-compos.yaml**, hãy dán cấu hình YAML sau đây.

```yaml
version: "3"
services:
  rabbitmq:
    image: rabbitmq:latest
    environment:
      - RABBITMQ_DEFAULT_USER=guest
      - RABBITMQ_DEFAULT_PASS=guest
    ports:
      - "5672:5672"

  redis:
    image: redis:latest
    ports:
      - "6379:6379"
```

Ở đây, chúng tôi chỉ cần khởi động hai dịch vụ, bằng cách xác định khóa hình ảnh để trỏ đến hình ảnh trong [dockerhub](https://hub.docker.com), ánh xạ các cổng `<host: docker>` và thêm các biến môi trường. Để xem những loại biến môi trường nào bạn có thể sử dụng với hình ảnh của mình, bạn chỉ cần truy cập hình ảnh tương ứng trong dockerhub và xem tài liệu. Ví dụ, bạn có thể kiểm tra cách sử dụng hình ảnh RabbitMQ [tại đây](https://hub.docker.com/_/rabbitmq)




-----
Tham khảo:
- [Asynchronous tasks in Python with Celery + RabbitMQ + Redis](https://levelup.gitconnected.com/asynchronous-tasks-in-python-with-celery-rabbitmq-redis-480f6e506d76)
- [Sử dụng Celery kết hợp Docker, PostgreSQL, Redis trong Django](https://viblo.asia/p/su-dung-celery-ket-hop-docker-postgresql-redis-trong-django-bWrZnz99Zxw)
- [Sử dụng Django kết hợp cùng Celery](https://viblo.asia/p/su-dung-django-ket-hop-cung-celery-GrLZDwzwKk0)
- [Tìm hiểu về Celery](https://viblo.asia/p/tim-hieu-ve-celery-1VgZv4dr5Aw)
- [Giới thiệu Celery](https://viblo.asia/p/gioi-thieu-celery-maGK7mvBlj2)
- [First Steps with Celery](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html)
- [First steps with Django](http://docs.celeryproject.org/en/latest/django/first-steps-with-django.html)
- [Building Your Own Export and Import Data Into Excel Using Django + Celery + Pandas + ❤️ With Progress Bar](https://blog.devgenius.io/building-your-own-export-and-import-data-into-excel-using-django-celery-pandas-%EF%B8%8F-with-784fd688e328)
- [Implementing Celery using Django for Background Task Processing](https://www.botreetechnologies.com/blog/implementing-celery-using-django-for-background-task-processing/)
- [Distributed Task Queues With Django, RabbitMQ, and Celery](https://laptrinhx.com/distributed-task-queues-with-django-rabbitmq-and-celery-124689327/)
- [Django channels hướng dẫn cơ bản](https://viblo.asia/p/django-channels-huong-dan-co-ban-3Q75wEjeZWb)
- [Videos tutorial - Learn Django Celery](https://www.youtube.com/playlist?list=PLOLrQ9Pn6caz-6WpcBYxV84g9gwptoN20)
- [the guide of Celery Redis Django](https://www.codingforentrepreneurs.com/blog/celery-redis-django/)
- [Asynchronous Tasks With Django and Celery](https://realpython.com/asynchronous-tasks-with-django-and-celery/)

-----
- [https://github.com/ebysofyan/django-celery-progress-sample](https://github.com/ebysofyan/django-celery-progress-sample)
- [https://github.com/jessamynsmith/django-celery-example](https://github.com/jessamynsmith/django-celery-example)
- [https://github.com/engineervix/django-celery-sample](https://github.com/engineervix/django-celery-sample)
- [https://github.com/Gabriel-Gardin/celery_django](https://github.com/Gabriel-Gardin/celery_django)
- [https://github.com/reouno/django-task-queue](https://github.com/reouno/django-task-queue)
- [https://github.com/Hassanzadeh-sd/Django-Celery](https://github.com/Hassanzadeh-sd/Django-Celery)