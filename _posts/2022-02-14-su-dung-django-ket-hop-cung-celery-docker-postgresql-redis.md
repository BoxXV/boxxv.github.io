---
layout: post
title: Sử dụng Django kết hợp cùng Celery, Docker, PostgreSQL, Redis
subtitle: Distributed Task Queue

tags:
- Celery
- Queue
- background jobs
- asynchronous task
- Docker
- PostgreSQL
- Redis
---

## Giới thiệu
`Celery` là một hàng đợi tác vụ không đồng bộ mã nguồn mở hoặc hàng đợi công việc dựa trên việc truyền thông điệp phân tán. Mặc dù nó hỗ trợ lập lịch trình, nhưng trọng tâm của nó là hoạt động trong thời gian thực.

![Async task architecture](https://boxxv.github.io/img/posts/23b9b40f-7f2b-4248-9aea-798c25a6879d.png "Async task architecture")

Khi nào cần sử dụng celery
- Chạy background jobs
- Chạy các job lập lịch
- Tính toán phân tán
- Xử lý song song

Chức năng
- Monitor: giám sát các job/task được đưa vào queue
- Scheduling: chạy các task lập lịch (giống cronjob)
- Workflows: tạo một luồng xử lý task
- Time & Rate Limits: kiểm soát số lượng task được thực thi trong một khoảng thời gian, thời gian một task được chạy,...
- Resource Leak Protection: kiểm soát tài nguyên trong quá trình xử lý task
- User Component: cho phép người dùng tự customize các worker.

Cơ chế của Celery
- Celery hoạt động dựa trên khái niệm task queue. Đây là cơ chế queue dùng để điều phối các job/work giữa các máy khác nhau. Các worker sẽ nhận task, chạy task và trả về kết quả.
- Input của queue:
- Task
- Các process trên từng worker sẽ theo dõi queue để thực thi các task mới được đẩy vào queue
- Celery thường dùng một message broker để điều phối task giữa các clients và worker. Để tạo một task mới client sẽ thêm một message vào queue, broker sau đó sẽ chuyển message này tới worker. Celery hỗ trợ 3 loại broker:
- RabbitMQ
- Redis
- SQS
- Một hệ thống sử dụng celery có thể có nhiều workers và brokers, nhờ vậy việc scale theo chiều ngang sẽ rất dễ dàng.


## Cài đặt



Thanks for reading!


-----
Tham khảo:
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