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