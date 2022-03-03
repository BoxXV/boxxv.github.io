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