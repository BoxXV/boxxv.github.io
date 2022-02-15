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




-----
Tham khảo:
- [Tìm hiểu về Celery](https://viblo.asia/p/tim-hieu-ve-celery-1VgZv4dr5Aw)
- [Giới thiệu Celery](https://viblo.asia/p/gioi-thieu-celery-maGK7mvBlj2)
- [First Steps with Celery](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html)
- [First steps with Django](http://docs.celeryproject.org/en/latest/django/first-steps-with-django.html)
- [Learn Django Celery](https://www.youtube.com/playlist?list=PLOLrQ9Pn6caz-6WpcBYxV84g9gwptoN20)
- [the guide of Celery Redis Django](https://www.codingforentrepreneurs.com/blog/celery-redis-django/)
- [Asynchronous Tasks With Django and Celery](https://realpython.com/asynchronous-tasks-with-django-and-celery/)
- [Cấu hình Supervisor để chạy Laravel Queue trên linux](https://viblo.asia/p/cau-hinh-supervisor-de-chay-laravel-queue-tren-linux-RQqKLoGN57z)

- [https://github.com/ebysofyan/django-celery-progress-sample](https://github.com/ebysofyan/django-celery-progress-sample)
- [https://github.com/jessamynsmith/django-celery-example](https://github.com/jessamynsmith/django-celery-example)
- [https://github.com/engineervix/django-celery-sample](https://github.com/engineervix/django-celery-sample)
- [https://github.com/Gabriel-Gardin/celery_django](https://github.com/Gabriel-Gardin/celery_django)
- [https://github.com/reouno/django-task-queue](https://github.com/reouno/django-task-queue)
- [https://github.com/Hassanzadeh-sd/Django-Celery](https://github.com/Hassanzadeh-sd/Django-Celery)