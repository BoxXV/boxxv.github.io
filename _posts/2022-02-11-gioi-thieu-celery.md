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

Celery là một open source asynchronous task queue or job queue. Nó dễ sử dụng, bạn không cần phải nắm quá rõ để sử dụng được nó. Celery được thiết kế dựa trên các phương pháp hay nhất để sản phẩm của bạn có thể mở rộng quy mô và tích hợp với các ngôn ngữ khác, đồng thời nó đi kèm với các công cụ và hỗ trợ bạn cần để vận hành một hệ thống như vậy trong quá trình sản xuất.

![Async task architecture](https://boxxv.github.io/img/posts/1_8728xEI7y5oSQ7YwC6USug.png "Async task architecture")

# 1. Chọn Message Broker

Message broker là nền tảng trung gian giúp giao tiếp giữa 2 ứng dụng. Với Celery, bạn có nhiều lựa chọn:

## RabbitMQ
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

### Trên Windows
Đừng lo lắng nếu bạn không chạy Ubuntu hoặc Debian, bạn có thể truy cập trang web này để tìm hướng dẫn cài đặt đơn giản tương tự cho các nền tảng khác, bao gồm Microsoft Windows:  
[https://www.rabbitmq.com/install-windows.html](https://www.rabbitmq.com/install-windows.html)  

Download and install Erlang  
[https://erlang.org/download/otp_versions_tree.html](https://erlang.org/download/otp_versions_tree.html)

Download and install RabbitMQ  
[https://github.com/rabbitmq/rabbitmq-server/releases](https://github.com/rabbitmq/rabbitmq-server/releases)  


## Redis
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


## Other brokers
Cũng có thể chọn những dịch vụ Message broker khác từ [Amason SQS](https://docs.celeryproject.org/en/latest/getting-started/backends-and-brokers/sqs.html). Đây là [danh sách các broker](https://docs.celeryproject.org/en/latest/getting-started/backends-and-brokers/index.html) được hỗ trợ trong Celery


# 2. Cài đặt
Có thể cài đặt Celery dễ dàng qua `pip` hoặc `easy_install`:
```bat
$ pip install celery
```

hoặc [`conda`](https://anaconda.org):
```bat
$ conda install -c conda-forge celery
$ conda install -c conda-forge rabbitmq-server
```

# 3. Application
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


# 4. Chạy Celery worker server
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

# 5. Call task

Để call một task, bạn có thể sử dụng method `delay()`
```bat
>>> from tasks import add
>>> add.delay(4, 4)
```

Sau khi gọi method trên, task vụ được đưa vào thực hiện và bạn có thể confirm tại màn hình console log lúc chạy `Celery` server. Khi gọi hàm trên thì bạn sẽ được trả về một `AsyncResult`. Bạn có thể sử dụng `AsyncResult` để kiểm tra trạng thái của task mình vừa add vào, đợi task hoàn thành hoặc nhận giá trị trả về của task(có thể nhận được ngoại lệ và traceback)


# 6. Lưu giữ Result

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


# 7. Retrying
Tính ổn định của các tác vụ nền không đồng bộ là rất quan trọng đối với thiết kế hệ thống của bạn. Khi bạn di chuyển công việc xử lý từ ứng dụng chính và thay vào đó sử dụng một thứ gì đó như Celery, để thực hiện công việc ở chế độ nền, điều quan trọng là bạn có thể cảm thấy tự tin rằng những tác vụ đó được thực thi chính xác mà không cần phải trông nom nó và chờ đợi kết quả.

Nhìn chung, có hai điều có thể xảy ra khi bạn gửi một nhiệm vụ cho Celery worker để xử lý nó trong nền:
- Sự cố kết nối với Broker và Message Queue.
- Các trường hợp ngoại lệ Exceptions xảy ra đối với worker.

May mắn thay, Celery cung cấp cho chúng tôi các công cụ và tùy chọn cần thiết để chúng tôi kiểm soát những gì sẽ xảy ra trong những tình huống này để chúng tôi có thể đảm bảo rằng worker của chúng tôi cố gắng thử lại và thực hiện lại các tác vụ.

## 7.1 Retry Connection to Broker with Celery

Vấn đề đầu tiên chúng tôi gặp phải là vấn đề kết nối với broker. Điều này có nghĩa là client thậm chí không thể tự gửi tin nhắn, điều này rõ ràng là một vấn đề quan trọng vì điều đó có thể có nghĩa là tin nhắn đã biến mất.

Điều này không giống như các loại sự cố khác mà sự cố xảy ra sau khi tin nhắn được gửi đi. Trong những trường hợp đó, thông báo ít nhất đã được lưu trữ trong hàng đợi và có thể đợi ở đó cho đến khi các vấn đề về nhân viên của chúng tôi được giải quyết.

Điều này được giải quyết bằng cách kích hoạt `retry=True` trên message và cũng chỉ định chính sách thử lại để xác định cách thực hiện thử lại.

Lưu ý rằng điều này có thể được áp dụng cả trên `task.apply_async()` và dưới `celery.send_task()`, vì vậy nó có thể được thực hiện cả trên các lệnh gọi đến các tác vụ cục bộ mà còn cho các tác vụ từ xa được lưu trữ trong các cơ sở mã khác.

Dưới đây là ví dụ về cách chúng tôi có thể bật thử lại và đặt chính sách thử lại:

```python
from tasks.celery import app

app.send_task(
    "foo.task",
    retry=True,
    retry_policy=dict(
        max_retries=3,
        interval_start=3,
        interval_step=1,
        interval_max=6
    )
)
```

Điều này có nghĩa là nếu kết nối không thành công và chúng tôi không thể gửi tin nhắn đến message queue, chúng tôi sẽ cố gắng thử lại 3 lần. Lần thử lại đầu tiên sẽ diễn ra sau `interval_start` giây, nghĩa là 3 giây. Sau đó, mỗi lỗi bổ sung sẽ đợi thêm `interval_step` 1 giây cho đến khi nó cố gắng gửi lại tin nhắn.

Lưu ý rằng kiểu thử lại này chỉ xảy ra khi không gửi được tin nhắn, không xảy ra khi bản thân tác vụ không thành công và kết thúc bằng một trạng thái `FAILURE`.

Nếu bạn muốn bật các chính sách thử lại trên globally trong ứng dụng của mình, bạn cũng có thể đặt nó trong [cài đặt Celery](https://docs.celeryproject.org/en/latest/userguide/configuration.html#std:setting-task_publish_retry) của mình .


## 7.2 Retry Failed Tasks in Celery

Loại vấn đề tiếp theo mà chúng tôi có thể gặp phải mà chúng tôi cũng muốn tận dụng các lần thử lại là khi các tác vụ không thành công. Lưu ý rằng kịch bản này hoàn toàn khác so với kịch bản đầu tiên. Trong trường hợp đầu tiên, chúng tôi _không gửi được tin nhắn_ . Trong trường hợp này, chúng tôi _không thực hiện thành công tác vụ_.

Lý do tại sao một nhiệm vụ có thể không thành công thường là do một sự cố đã xảy ra trên worker và một Ngoại lệ Exception được đưa ra. Có lẽ có lỗi trong mã, một số service đã hết thời gian chờ hoặc nhu cầu quá cao.

Không giống như tình huống đầu tiên chúng tôi yêu cầu client thử gửi lại tác vụ, lần này chúng tôi muốn thêm mã vào chính tác vụ, có nghĩa là, worker sẽ thử lại để thực thi tác vụ, chứ không phải khách hàng thử lại gửi lại nhiệm vụ. Lưu ý sự khác biệt đáng kể này.


### 7.2.1 - Solution 1: Sử dụng Try/Except Block

Chúng ta có thể sử dụng khối `Try/Except` trừ để bắt ngoại lệ và retry:

Dưới đây là một ví dụ về cách chúng tôi có thể thử lại một tác vụ khi một Ngoại lệ được nâng lên:

```python
import logging
from tasks.celery import app

logger = logging.getLogger(__name__)

@app.task(name="foo.task", bind=True, max_retries=3)
def foo_task(self):
    try:
        execute_something()
    except Exception as ex:
        logger.exception(ex)
        self.retry(countdown=3**self.request.retries)
```

Hãy xem qua tất cả những gì mã này làm:
- `bind=True` đây là một tác vụ bị ràng buộc, cung cấp cho chúng tôi quyền truy cập vào `self` keyword argument.
- `max_retries` xác định thời gian tối đa mà tác vụ này có thể được thực thi lại bằng phương thức `self.retry()`.
- Bất cứ khi nào chúng tôi bắt gặp một ngoại lệ mà chúng tôi không tăng lại và im lặng, chúng tôi muốn đảm bảo rằng chúng tôi ghi lại lỗi bằng cách sử dụng phương pháp `logger.exception()` sẽ bao gồm toàn bộ theo dõi.
- `self.retry()` sẽ thử lại tác vụ. Kwarg `countdown` xác định chúng ta nên đợi bao nhiêu giây trước khi thử lại. Lưu ý rằng chúng tôi xác định nó là một giá trị hàm mũ sẽ tăng lên sau mỗi lần thử lại.

### 7.2.2 - Solution 2: Task Retry Decorator

Celery 4.0 đã thêm hỗ trợ tích hợp để thử lại, vì vậy bạn có thể để bubble ngoại lệ lên và chỉ định trong Decorator cách xử lý nó:

```python
@shared_task(bind=True, autoretry_for=(Exception,), retry_kwargs={'max_retries': 7, 'countdown': 5})
def task_process_notification(self):
    if not random.choice([0, 1]):
        # mimic random error
        raise Exception()

    requests.post('https://httpbin.org/delay/5')
```

- `autoretry_for` lấy một list/tuple ngoại lệ mà bạn muốn thử lại.
- `retry_kwargs` có một từ điển các [tùy chọn](https://docs.celeryproject.org/en/latest/userguide/tasks.html#list-of-options) bổ sung để chỉ định cách các truy vấn tự động được thực hiện. Trong ví dụ trên, tác vụ sẽ thử lại sau 5 giây trễ (qua `countdown`) và nó cho phép tối đa 7 lần thử lại (qua `max_retries`). Celery sẽ ngừng thử lại sau 7 lần thử không thành công và đưa ra một ngoại lệ.

#### Backoff theo cấp số nhân
Nếu nhiệm vụ Celery của bạn cần gửi yêu cầu đến dịch vụ của bên thứ ba, bạn nên sử dụng [Backoff theo cấp số nhân](https://en.wikipedia.org/wiki/Exponential_backoff) để tránh áp đảo dịch vụ.

```python
@shared_task(bind=True, autoretry_for=(Exception,), retry_backoff=True, retry_kwargs={'max_retries': 5})
def task_process_notification(self):
    if not random.choice([0, 1]):
        # mimic random error
        raise Exception()

    requests.post('https://httpbin.org/delay/5')
```

Trong ví dụ này, lần thử lại đầu tiên sẽ chạy sau 1 giây, lần sau sau 2 giây, lần thứ ba sau 4 giây, lần thứ tư sau 8 giây, v.v.:

```bat
[02:09:59,014: INFO/ForkPoolWorker-8] Task polls.tasks.task_process_notification[fbe041b6-e6c1-453d-9cc9-cb99236df6ff] retry: Retry in 1s: Exception()
[02:10:00,210: INFO/ForkPoolWorker-2] Task polls.tasks.task_process_notification[fbe041b6-e6c1-453d-9cc9-cb99236df6ff] retry: Retry in 2s: Exception()
[02:10:02,291: INFO/ForkPoolWorker-4] Task polls.tasks.task_process_notification[fbe041b6-e6c1-453d-9cc9-cb99236df6ff] retry: Retry in 4s: Exception()
```

Bạn cũng có thể đặt `retry_backoff` thành một số để sử dụng làm hệ số trễ

#### Ngẫu nhiên
Khi bạn xây dựng chiến lược thử lại tùy chỉnh cho tác vụ Celery của mình (cần gửi yêu cầu đến một dịch vụ khác), bạn nên thêm một số ngẫu nhiên vào tính toán độ trễ để ngăn tất cả các tác vụ được thực hiện đồng thời dẫn đến một [thundering herd](https://en.wikipedia.org/wiki/Thundering_herd_problem).

Celery cũng được bạn đề cập ở đây với `retry_jitter`:

```python
@shared_task(bind=True, autoretry_for=(Exception,), retry_backoff=5, retry_jitter=True, retry_kwargs={'max_retries': 5})
def task_process_notification(self):
    if not random.choice([0, 1]):
        # mimic random error
        raise Exception()

    requests.post('https://httpbin.org/delay/5')
```

Tùy chọn này được đặt thành `True` mặc định, giúp ngăn chặn sự cố đàn sấm sét khi bạn sử dụng cài sẵn của Celery `retry_backoff`.

#### Task Base Class
Nếu bạn thấy mình đang viết các đối số thử lại giống nhau trong trình trang trí tác vụ Celery của mình, bạn có thể (kể từ [Celery 4.4](https://docs.celeryproject.org/en/v4.4.4/whatsnew-4.4.html#task-class-definitions-can-now-have-retry-attributes) ) xác định các đối số thử lại trong một lớp cơ sở, sau đó bạn có thể sử dụng làm lớp cơ sở trong các tác vụ Celery của mình:

```python
class BaseTaskWithRetry(celery.Task):
    autoretry_for = (Exception, KeyError)
    retry_kwargs = {'max_retries': 5}
    retry_backoff = True

@shared_task(bind=True, base=BaseTaskWithRetry)
def task_process_notification(self):
    raise Exception()
```

Một lần nữa, mã nguồn của bài viết này có thể được tìm thấy trên [GitHub](https://github.com/testdrivenio/django-celery-project).


# 8. Logging
Updating: coming soon


# 9. Kết luận
Mình vừa giới thiệu cho các bạn về `Celery`, cách cài đặt và demo đơn giản. Hẹn gặp lại các bạn ở những phần nâng cao của Celery.


-----
Tham khảo:
- [Giới thiệu Celery](https://viblo.asia/p/gioi-thieu-celery-maGK7mvBlj2)
- [First Steps with Celery](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html)
- [First steps with Django](http://docs.celeryproject.org/en/latest/django/first-steps-with-django.html)
- [Learn Django Celery](https://www.youtube.com/playlist?list=PLOLrQ9Pn6caz-6WpcBYxV84g9gwptoN20)
- [the guide of Celery Redis Django](https://www.codingforentrepreneurs.com/blog/celery-redis-django/)
- [Asynchronous Tasks With Django and Celery](https://realpython.com/asynchronous-tasks-with-django-and-celery/)
- [Cấu hình Supervisor để chạy Laravel Queue trên linux](https://viblo.asia/p/cau-hinh-supervisor-de-chay-laravel-queue-tren-linux-RQqKLoGN57z)
- [How to Automatically Retry Failed Tasks with Celery](https://coderbook.com/@marcus/how-to-automatically-retry-failed-tasks-with-celery/)
- [Automatically Retrying Failed Celery Tasks](https://testdriven.io/blog/retrying-failed-celery-tasks/)
- [Celery > Tasks > Retrying ](https://docs.celeryproject.org/en/stable/userguide/tasks.html?highlight=autoretry_for#retrying)
-----
- [https://github.com/ebysofyan/django-celery-progress-sample](https://github.com/ebysofyan/django-celery-progress-sample)
- [https://github.com/jessamynsmith/django-celery-example](https://github.com/jessamynsmith/django-celery-example)
- [https://github.com/engineervix/django-celery-sample](https://github.com/engineervix/django-celery-sample)
- [https://github.com/Gabriel-Gardin/celery_django](https://github.com/Gabriel-Gardin/celery_django)
- [https://github.com/reouno/django-task-queue](https://github.com/reouno/django-task-queue)
- [https://github.com/Hassanzadeh-sd/Django-Celery](https://github.com/Hassanzadeh-sd/Django-Celery)