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


## Về Celery
- Là một hệ thống quản lý hàng đợi xử lý task thời gian thực. Trong hệ thống Celery chúng ta sẽ sử dụng khái niệm task giống như job ở một số framework khác như Sidekiq.
- Input của celery cần kết nối với một loại message broker còn output có thể kết nối tới một hệ thống backend để lưu trữ kết quả

Các bài toán nên sử dụng Celery
- Chạy background jobs
- Chạy các job lập lịch
- Tính toán phân tán
- Xử lý song song

Các chức năng chính Celery cung cấp
- Monitor: giám sát các job/task được đưa vào queue
- Scheduling: chạy các task lập lịch (giống cronjob)
- Workflows: tạo một luồng xử lý task
- Time & Rate Limits: kiểm soát số lượng task được thực thi trong một khoảng thời gian, thời gian một task được chạy,...
- Resource Leak Protection: kiểm soát tài nguyên trong quá trình xử lý task
- User Component: cho phép người dùng tự customize các worker.

Cơ chế của Celery
- Celery hoạt động dựa trên khái niệm task queue. Đây là cơ chế queue dùng để điều phối các job/work giữa các máy khác nhau. Các worker sẽ nhận task, chạy task và trả về kết quả.
- Input của queue:
	+ Task
- Các process trên từng worker sẽ theo dõi queue để thực thi các task mới được đẩy vào queue
- Celery thường dùng một message broker để điều phối task giữa các clients và worker. Để tạo một task mới client sẽ thêm một message vào queue, broker sau đó sẽ chuyển message này tới worker. Celery hỗ trợ 3 loại broker:
	+ RabbitMQ
	+ Redis
	+ SQS
- Một hệ thống sử dụng celery có thể có nhiều workers và brokers, nhờ vậy việc scale theo chiều ngang sẽ rất dễ dàng.




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