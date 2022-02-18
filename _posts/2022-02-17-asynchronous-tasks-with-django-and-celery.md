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

## 0. Giới thiệu
Khi tôi mới làm quen với Django, một trong những điều khó chịu nhất mà tôi trải qua là phải chạy một chút mã định kỳ. Tôi đã viết một hàm hay thực hiện một hành động cần chạy hàng ngày lúc 12 giờ sáng. Dễ dàng, phải không? Sai. Điều này hóa ra là một vấn đề lớn đối với tôi vì vào thời điểm đó tôi đã quen với việc lưu trữ web "Cpanel-type", nơi có một GUI tiện dụng tốt đẹp để thiết lập cron job cho mục đích này.

Sau nhiều nghiên cứu, tôi đã tìm ra một giải pháp hay — Celery, một hàng đợi công việc không đồng bộ mạnh mẽ được sử dụng để chạy các tác vụ trong nền. Nhưng điều này dẫn đến các vấn đề khác, vì tôi không thể tìm thấy một bộ hướng dẫn dễ dàng để tích hợp Celery vào Dự án Django.

Tất nhiên, cuối cùng tôi đã cố gắng tìm ra nó — đó là nội dung mà bài viết này sẽ đề cập: *Cách tích hợp Celery vào Dự án Django và tạo Nhiệm vụ định kỳ*.


## 1. What is Celery?

“Celery là một hàng đợi nhiệm vụ/hàng đợi công việc không đồng bộ dựa trên việc truyền thông điệp phân tán. Nó tập trung vào hoạt động thời gian thực, nhưng cũng hỗ trợ lập lịch trình.” Đối với bài đăng này, chúng tôi sẽ tập trung vào tính năng lập lịch để chạy một công việc/nhiệm vụ theo định kỳ.

Tại sao điều này lại hữu ích?
- Hãy nghĩ về tất cả những lần bạn phải thực hiện một nhiệm vụ nào đó trong tương lai. Có lẽ bạn cần [truy cập một API](https://realpython.com/api-integration-in-python/) mỗi giờ. Hoặc có thể bạn cần gửi một loạt email vào cuối ngày. Dù lớn hay nhỏ, Celery đều làm cho việc lên lịch các công việc định kỳ như vậy trở nên dễ dàng.
- Bạn không bao giờ muốn người dùng cuối phải đợi các trang tải hoặc các hành động hoàn thành một cách không cần thiết. Nếu quy trình dài là một phần của quy trình làm việc của ứng dụng, bạn có thể sử dụng Celery để thực thi quy trình đó trong nền, khi các tài nguyên trở nên sẵn có, để ứng dụng của bạn có thể tiếp tục phản hồi các yêu cầu của khách hàng. Điều này giữ cho nhiệm vụ nằm ngoài ngữ cảnh của ứng dụng.


## 2. Setup

Trước khi tìm hiểu về Celery, hãy lấy dự án khởi đầu từ [repo Github](https://github.com/realpython/Picha/releases/tag/v1). Đảm bảo kích hoạt `virtualenv`, cài đặt các yêu cầu và [chạy quá trình migrations](https://realpython.com/django-migrations-a-primer/). Sau đó khởi động máy chủ và điều hướng đến [http://localhost:8000/](http://localhost:8000/) trong trình duyệt của bạn. Bạn sẽ thấy dòng chữ quen thuộc “Congratulations on your first Django-powered page”. Khi hoàn tất, kill the server.

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

Hãy ghi chú các nhận xét trong mã.

### Bước 2: Import ứng dụng Celery mới của bạn

Để đảm bảo rằng ứng dụng Celery được tải khi Django khởi động, hãy thêm mã sau vào tệp `__init__.py` nằm bên cạnh tệp `settings.py` của bạn:

```python
from __future__ import absolute_import

# This will make sure the app is always imported when
# Django starts so that shared_task will use this app.
from .celery import app as celery_app
```

Sau khi thực hiện điều đó, [bố cục dự án](https://realpython.com/python-application-layouts/) của bạn bây giờ sẽ giống như sau:

```bat
helloworld/
│
├── .gitignore
├── helloworld.py
├── LICENSE
├── README.md
├── requirements.txt
├── setup.py
└── tests.py
```

### Bước 3: Cài đặt Redis với tư cách là Celery “Broker”

Celery sử dụng "[brokers](https://docs.celeryproject.org/en/latest/getting-started/backends-and-brokers/index.html)" để chuyển các thông điệp giữa Dự án Django và các [workers](https://docs.celeryproject.org/en/latest/userguide/workers.html) Celery . Trong hướng dẫn này, chúng tôi sẽ sử dụng `Redis` làm message broker.

Đầu tiên, cài đặt [Redis](https://redis.io) từ trang tải xuống chính thức hoặc qua brew (`brew install redis`), sau đó chuyển sang terminal của bạn, trong cửa sổ đầu cuối mới, kích hoạt máy chủ:

```bat
$ redis-server
```

Bạn có thể kiểm tra xem Redis có hoạt động bình thường không bằng cách nhập mã này vào terminal của bạn:

```bat
$ redis-cli ping
```

Redis nên trả lời bằng PONG - try it!

Sau khi Redis hoạt động, hãy thêm mã sau vào tệp settings.py của bạn:

```python
# CELERY STUFF
BROKER_URL = 'redis://localhost:6379'
CELERY_RESULT_BACKEND = 'redis://localhost:6379'
CELERY_ACCEPT_CONTENT = ['application/json']
CELERY_TASK_SERIALIZER = 'json'
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TIMEZONE = 'Africa/Nairobi'
```

Bạn cũng cần thêm Redis làm phụ thuộc trong Dự án Django:

```bat
$ pip install redis==2.10.3
$ pip freeze > requirements.txt
```

Đó là nó! Bây giờ bạn có thể sử dụng Celery với Django. Để biết thêm thông tin về cách thiết lập Celery với Django, vui lòng xem [tài liệu chính thức](https://docs.celeryproject.org/en/latest/django/first-steps-with-django.html#using-celery-with-django) về Celery.

Trước khi tiếp tục, hãy chạy một vài kiểm tra sự tỉnh táo để đảm bảo tất cả đều tốt…

Kiểm tra xem Celery worker đã sẵn sàng nhận nhiệm vụ chưa:

```bat
$ celery -A picha worker -l info
...
[2015-07-07 14:07:07,398: INFO/MainProcess] Connected to redis://localhost:6379//
[2015-07-07 14:07:07,410: INFO/MainProcess] mingle: searching for neighbors
[2015-07-07 14:07:08,419: INFO/MainProcess] mingle: all alone
```

Kill the process bằng CTRL-C. Bây giờ, hãy kiểm tra xem bộ lập lịch tác vụ Celery đã sẵn sàng hoạt động chưa:

```bat
$ celery -A picha beat -l info
...
[2015-07-07 14:08:23,054: INFO/MainProcess] beat: Starting...
```

Bùm!

Một lần nữa, hãy kill the process khi hoàn tất.


## 3. Celery Tasks

Celery sử dụng các [tác vụ](https://docs.celeryproject.org/en/latest/userguide/tasks.html), có thể được coi là các hàm Python thông thường được gọi với Celery.

Ví dụ: hãy biến chức năng cơ bản này thành một tác vụ Celery:

```python
def add(x, y):
    return x + y
```

Đầu tiên, hãy thêm một decorator:

```python
from celery.decorators import task

@task(name="sum_two_numbers")
def add(x, y):
    return x + y
```

Sau đó, bạn có thể chạy tác vụ này không đồng bộ với Celery như sau:

```bat
add.delay(7, 8)
```

Đơn giản, phải không?

Vì vậy, những loại tác vụ này hoàn toàn phù hợp khi bạn muốn tải một trang web mà không bắt người dùng phải đợi một số quá trình nền hoàn thành.

Hãy xem một ví dụ…

-----

Quay trở lại Dự án Django, lấy [phiên bản v3](https://github.com/realpython/Picha/releases/tag/v3), bao gồm một ứng dụng chấp nhận phản hồi từ người dùng, được gọi là `feedback`:

```bat
├── feedback
│   ├── __init__.py
│   ├── admin.py
│   ├── emails.py
│   ├── forms.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── manage.py
├── picha
│   ├── __init__.py
│   ├── celery.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── requirements.txt
└── templates
    ├── base.html
    └── feedback
        ├── contact.html
        └── email
            ├── feedback_email_body.txt
            └── feedback_email_subject.txt
```

Cài đặt các yêu cầu mới, kích hoạt ứng dụng và điều hướng đến (http://localhost:8000/feedback/)[http://localhost:8000/feedback/]. Bạn nên thấy:

![Async task architecture](https://boxxv.github.io/img/posts/feedback-app.webp "Async task architecture")

Hãy lên dây cót nhiệm vụ Celery.

### Add the Task

Về cơ bản, sau khi người dùng gửi biểu mẫu phản hồi, chúng tôi muốn ngay lập tức để họ tiếp tục theo cách vui vẻ của mình trong khi chúng tôi xử lý phản hồi, gửi email, v.v., tất cả đều ở chế độ nền.

Để thực hiện điều này, trước tiên hãy thêm một tệp có tên là `task.py` vào thư mục "feedback":

```python
from celery.decorators import task
from celery.utils.log import get_task_logger

from feedback.emails import send_feedback_email

logger = get_task_logger(__name__)


@task(name="send_feedback_email_task")
def send_feedback_email_task(email, message):
    """sends an email when feedback form is filled successfully"""
    logger.info("Sent feedback email")
    return send_feedback_email(email, message)
```

Sau đó, cập nhật các `form.py` như sau:

```python
from django import forms
from feedback.tasks import send_feedback_email_task

class FeedbackForm(forms.Form):
    email = forms.EmailField(label="Email Address")
    message = forms.CharField(
        label="Message", widget=forms.Textarea(attrs={'rows': 5}))
    honeypot = forms.CharField(widget=forms.HiddenInput(), required=False)

    def send_email(self):
        # try to trick spammers by checking whether the honeypot field is
        # filled in; not super complicated/effective but it works
        if self.cleaned_data['honeypot']:
            return False
        send_feedback_email_task.delay(
            self.cleaned_data['email'], self.cleaned_data['message'])
```

Về bản chất, `send_feedback_email_task.delay(email, message)` chức năng xử lý và gửi email phản hồi trong nền khi người dùng tiếp tục sử dụng trang web.

> *LƯU Ý*: `success_url` trong `views.py` được đặt để chuyển hướng người dùng đến `/`, chưa tồn tại. Chúng tôi sẽ thiết lập điểm cuối này trong phần tiếp theo.


## 4. Nhiệm vụ định kỳ

Thông thường, bạn sẽ cần phải lên lịch một tác vụ để chạy vào một thời điểm cụ thể thường xuyên - ví dụ, một trình duyệt [web scraper](https://realpython.com/python-web-scraping-practical-introduction/) có thể cần chạy hàng ngày. Những nhiệm vụ như vậy, được gọi là [nhiệm vụ định kỳ](https://docs.celeryproject.org/en/latest/userguide/periodic-tasks.html), rất dễ thiết lập với Celery.

Celery sử dụng “celery beat” để lên lịch các công việc định kỳ. Celery beat chạy các nhiệm vụ trong khoảng thời gian đều đặn, sau đó được thực hiện bởi các Celery workers.

Ví dụ: tác vụ sau được lên lịch chạy mười lăm phút một lần:

```python
from celery.task.schedules import crontab
from celery.decorators import periodic_task


@periodic_task(run_every=(crontab(minute='*/15')), name="some_task", ignore_result=True)
def some_task():
    # do something
```

Hãy xem ví dụ mạnh mẽ hơn bằng cách thêm chức năng này vào Dự án Django…

-----

Quay lại Dự án Django, lấy [phiên bản v4](https://github.com/realpython/Picha/releases/tag/v4), bao gồm một ứng dụng mới khác, được gọi là `photos`, sử dụng [API Flickr](https://www.flickr.com/services/api/) để tải ảnh mới hiển thị trên trang web:

```bat
├── feedback
│   ├── __init__.py
│   ├── admin.py
│   ├── emails.py
│   ├── forms.py
│   ├── models.py
│   ├── tasks.py
│   ├── tests.py
│   └── views.py
├── manage.py
├── photos
│   ├── __init__.py
│   ├── admin.py
│   ├── models.py
│   ├── settings.py
│   ├── tests.py
│   ├── utils.py
│   └── views.py
├── picha
│   ├── __init__.py
│   ├── celery.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── requirements.txt
└── templates
    ├── base.html
    ├── feedback
    │   ├── contact.html
    │   └── email
    │       ├── feedback_email_body.txt
    │       └── feedback_email_subject.txt
    └── photos
        └── photo_list.html
```

Cài đặt các yêu cầu mới, chạy quá trình migrations và sau đó khởi động máy chủ để đảm bảo tất cả đều ổn. Hãy thử kiểm tra lại biểu mẫu `feedback`. Lần này nó sẽ chuyển hướng tốt.

Cái gì tiếp theo?

Chà, vì chúng tôi cần gọi API Flickr định kỳ để thêm nhiều ảnh hơn vào trang web của mình, chúng tôi có thể thêm tác vụ Celery.

### Add the Task

Thêm một `task.py` vào ứng dụng `photos`:

```python
from celery.task.schedules import crontab
from celery.decorators import periodic_task
from celery.utils.log import get_task_logger

from photos.utils import save_latest_flickr_image

logger = get_task_logger(__name__)

@periodic_task(
    run_every=(crontab(minute='*/15')),
    name="task_save_latest_flickr_image",
    ignore_result=True
)
def task_save_latest_flickr_image():
    """
    Saves latest image from Flickr
    """
    save_latest_flickr_image()
    logger.info("Saved image from Flickr")
```

Ở đây, chúng tôi chạy hàm `save_latest_flickr_image()` mười lăm phút một lần bằng cách gói lệnh gọi hàm trong `task`. decorator `@periodic_task` sẽ tóm tắt mã để chạy tác vụ Celery, để lại tệp `task.py` sạch sẽ và dễ đọc!


## 5. Running Locally

Sẵn sàng để chạy điều này?

Với Ứng dụng Django và Redis của bạn đang chạy, hãy mở terminal windows/tabs. mới. Trong mỗi cửa sổ mới, điều hướng đến thư mục dự án của bạn, kích hoạt `virtualenv` của bạn, sau đó chạy các lệnh sau (một lệnh trong mỗi cửa sổ):

```bat
$ celery -A picha worker -l info
$ celery -A picha beat -l info
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