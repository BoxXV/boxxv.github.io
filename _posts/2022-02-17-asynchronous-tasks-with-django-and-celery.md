---
layout: post
title: Asynchronous Tasks với Django và Celery
subtitle: Tác vụ không đồng bộ với Django và Celery

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

## Giới thiệu
Khi tôi mới làm quen với Django, một trong những điều khó chịu nhất mà tôi trải qua là phải chạy một chút mã định kỳ. Tôi đã viết một hàm hay thực hiện một hành động cần chạy hàng ngày lúc 12 giờ sáng. Dễ dàng, phải không? Sai. Điều này hóa ra là một vấn đề lớn đối với tôi vì vào thời điểm đó tôi đã quen với việc lưu trữ web "Cpanel-type", nơi có một GUI tiện dụng tốt đẹp để thiết lập cron job cho mục đích này.

Sau nhiều nghiên cứu, tôi đã tìm ra một giải pháp hay — Celery, một hàng đợi công việc không đồng bộ mạnh mẽ được sử dụng để chạy các tác vụ trong nền. Nhưng điều này dẫn đến các vấn đề khác, vì tôi không thể tìm thấy một bộ hướng dẫn dễ dàng để tích hợp Celery vào Dự án Django.

Tất nhiên, cuối cùng tôi đã cố gắng tìm ra nó — đó là nội dung mà bài viết này sẽ đề cập: `Cách tích hợp Celery vào Dự án Django và tạo Nhiệm vụ định kỳ`.


## What is Celery?

“Celery là một hàng đợi nhiệm vụ/hàng đợi công việc không đồng bộ dựa trên việc truyền thông điệp phân tán. Nó tập trung vào hoạt động thời gian thực, nhưng cũng hỗ trợ lập lịch trình.” Đối với bài đăng này, chúng tôi sẽ tập trung vào tính năng lập lịch để chạy một công việc/nhiệm vụ theo định kỳ.

Tại sao điều này lại hữu ích?
- Hãy nghĩ về tất cả những lần bạn phải thực hiện một nhiệm vụ nào đó trong tương lai. Có lẽ bạn cần [truy cập một API](https://realpython.com/api-integration-in-python/) mỗi giờ. Hoặc có thể bạn cần gửi một loạt email vào cuối ngày. Dù lớn hay nhỏ, Celery đều làm cho việc lên lịch các công việc định kỳ như vậy trở nên dễ dàng.
- Bạn không bao giờ muốn người dùng cuối phải đợi các trang tải hoặc các hành động hoàn thành một cách không cần thiết. Nếu quy trình dài là một phần của quy trình làm việc của ứng dụng, bạn có thể sử dụng Celery để thực thi quy trình đó trong nền, khi các tài nguyên trở nên sẵn có, để ứng dụng của bạn có thể tiếp tục phản hồi các yêu cầu của khách hàng. Điều này giữ cho nhiệm vụ nằm ngoài ngữ cảnh của ứng dụng.


## Setup

Trước khi tìm hiểu về Celery, hãy lấy dự án khởi đầu từ [repo Github](https://github.com/realpython/Picha/releases/tag/v1). Đảm bảo kích hoạt `virtualenv`, cài đặt các yêu cầu và [chạy quá trình di chuyển](https://realpython.com/django-migrations-a-primer/). Sau đó khởi động máy chủ và điều hướng đến [http://localhost:8000/](http://localhost:8000/) trong trình duyệt của bạn. Bạn sẽ thấy dòng chữ quen thuộc “Congratulations on your first Django-powered page”. Khi hoàn tất, kill the server.

Tiếp theo, hãy cài đặt Celery bằng cách sử dụng pip:

```bat
$ pip install celery==3.1.18
$ pip freeze > requirements.txt
```

Giờ đây, chúng ta có thể tích hợp Celery vào Dự án Django của mình chỉ trong ba bước đơn giản.

### Bước 1: Thêm celery.py

Bên trong thư mục “picha”, tạo một tệp mới có tên `celery.py`:

```python
from __future__ import absolute_import
import os
from celery import Celery
from django.conf import settings

# set the default Django settings module for the 'celery' program.
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'picha.settings')
app = Celery('picha')

# Using a string here means the worker will not have to
# pickle the object when using Windows.
app.config_from_object('django.conf:settings')
app.autodiscover_tasks(lambda: settings.INSTALLED_APPS)


@app.task(bind=True)
def debug_task(self):
    print('Request: {0!r}'.format(self.request))
```










-----
Tham khảo:
- [Asynchronous Tasks With Django and Celery](https://realpython.com/asynchronous-tasks-with-django-and-celery/)
- [How to Use Celery and Django to Handle Periodic Tasks](https://nickmccullum.com/celery-django-periodic-tasks/)
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