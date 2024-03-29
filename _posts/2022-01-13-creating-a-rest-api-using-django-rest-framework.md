---
layout: post
title: Xây dựng API với Django Rest Framework
subtitle: Creating a REST API using Django Rest Framework

tags:
- Django
- DjangoREST
- framework
- API
---

# Giới thiệu chung

Việc xây dựng một API REST trong Django quá dễ dàng. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn các bước để thiết lập và chạy API đầu tiên của bạn.

![RESTful API](https://boxxv.github.io/img/posts/restful-api.jpg "RESTful API")

## RESTful API là gì?

RESTful API là một tiêu chuẩn dùng trong việc thiết kế API cho các ứng dụng web (thiết kế Web services) để tiện cho việc quản lý các resource. Nó chú trọng vào tài nguyên hệ thống (tệp văn bản, ảnh, âm thanh, video, hoặc dữ liệu động…), bao gồm các trạng thái tài nguyên được định dạng và được truyền tải qua HTTP.

`API` (Application Programming Interface) là một tập các quy tắc và cơ chế mà theo đó, một ứng dụng hay một thành phần sẽ tương tác với một ứng dụng hay thành phần khác. API có thể trả về dữ liệu mà bạn cần cho ứng dụng của mình ở những kiểu dữ liệu phổ biến như JSON hay XML.

`REST` (REpresentational State Transfer) là một dạng chuyển đổi cấu trúc dữ liệu, một kiểu kiến trúc để viết API. Nó sử dụng phương thức HTTP đơn giản để tạo cho giao tiếp giữa các máy. Vì vậy, thay vì sử dụng một URL cho việc xử lý một số thông tin người dùng, REST gửi một yêu cầu HTTP như GET, POST, DELETE, vv đến một URL để xử lý dữ liệu.

`RESTful API` là một tiêu chuẩn dùng trong việc thiết kế các API cho các ứng dụng web để quản lý các resource. RESTful là một trong những kiểu thiết kế API được sử dụng phổ biến ngày nay để cho các ứng dụng (web, mobile…) khác nhau giao tiếp với nhau.

Chức năng quan trọng nhất của REST là quy định cách sử dụng các HTTP method (như `GET`, `POST`, `PUT`, `DELETE`…) và cách định dạng các URL cho ứng dụng web để quản các resource. RESTful không quy định logic code ứng dụng và không giới hạn bởi ngôn ngữ lập trình ứng dụng, bất kỳ ngôn ngữ hoặc framework nào cũng có thể sử dụng để thiết kế một RESTful API.

REST hoạt động chủ yếu dựa vào giao thức HTTP. Các hoạt động cơ bản nêu trên sẽ sử dụng những phương thức HTTP riêng.

- GET (`SELECT`): Trả về một Resource hoặc một danh sách Resource.
- POST (`CREATE`): Tạo mới một Resource.
- PUT (`UPDATE`): Cập nhật thông tin cho Resource.
- DELETE (`DELETE`): Xoá một Resource.
Những phương thức hay hoạt động này thường được gọi là `CRUD` tương ứng với Create, Read, Update, Delete – Tạo, Đọc, Sửa, Xóa.

## Authentication và dữ liệu trả về

`RESTful API` không sử dụng `session` và `cookie`, nó sử dụng một `access_token` với mỗi request. Dữ liệu trả về thường có cấu trúc như sau:

```json
{
    "data" : {
        "id": "1",
        "name": "TopDev"
    }
}
```

## Tại sao nên sử dụng Django REST Framework?

![Django REST Framework](https://boxxv.github.io/img/posts/1_lAMsvtB6afHwTQYCNM1xvw.png "Django REST Framework")

Lý do lớn nhất để sử dụng Django REST Framework là vì nó giúp tuần tự hóa quá dễ dàng!

Trong Django, bạn xác định các mô hình cho cơ sở dữ liệu của mình bằng Python. Mặc dù bạn có thể viết SQL thô, nhưng đối với hầu hết các phần, Django ORM xử lý tất cả các truy vấn và di chuyển cơ sở dữ liệu.

Hãy coi Django ORM giống như một thủ thư, lấy thông tin cần thiết cho bạn, vì vậy bạn không cần phải tự mình đi lấy.

Là một nhà phát triển, điều này giúp bạn không phải lo lắng về logic kinh doanh của ứng dụng của mình và quên đi các chi tiết triển khai cấp thấp. Django ORM xử lý tất cả những điều đó cho bạn.

Sau đó, Django REST Framework hoạt động tốt với Django ORM đã thực hiện tất cả các công việc nặng nhọc của việc truy vấn cơ sở dữ liệu. Chỉ cần một vài dòng mã sử dụng Django REST Framework và bạn có thể tuần tự hóa các mô hình cơ sở dữ liệu của mình sang các định dạng REST-ful.

## Bài toán
Mình sẽ viết những API phục vụ cho phép thực hiện Create, Read, Update và Delete `cars`.

`Car` bao gồm những field sau:
- Name
- Color
- Brand

# Danh sách việc cần làm để tạo REST API trong Django

- Cài đặt Django
- Tạo một Model trong cơ sở dữ liệu mà Django ORM sẽ quản lý
- Thiết lập Khung Django REST
- Tuần tự hóa mô hình từ bước 2
- Tạo các điểm cuối URI để xem dữ liệu được tuần tự hóa

## Cài đặt Django

```bat
pip install django
pip install djangorestframework

django-admin startproject src
django-admin startapp car

python manage.py migrate
python manage.py runserver
```

Và chúng ta nhận được cấu trúc thư mục của project như sau:
```
.
|__car
    |-- __init__.py
    |-- apps.py
    |-- admin.py
    |-- views.py
    |-- models.py
    |-- tests.py
    |__migrations
        |-- __init__.py
|__src
    |-- __init__.py
    |-- settings.py
    |-- urls.py
    |-- wsgi.py
|-- manage.py

.
+-- car
|   +-- __init__.py
|   +-- apps.py
|   +-- admin.py
|   +-- views.py
|   +-- models.py
|   +-- tests.py
|   +-- migrations
|   |   +-- __init__.py
+-- src
|   +-- __init__
|   +-- settings.py
|   +-- urls.py
|   +-- wsgi.py
+-- manage.py

.
├── car
│   ├── __init__.py
│   ├── apps.py
│   ├── admin.py
│   ├── views.py
│   ├── urls.py
│   ├── models.py
│   ├── tests.py
│   └── migrations
│       └── __init__.py
├── src
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py
```

Và khi cài đặt xong xuôi, các bạn truy cập vào [http://127.0.0.1:8000](http://127.0.0.1:8000) và  [http://127.0.0.1:8000/admin](http://127.0.0.1:8000/admin)


## Tạo một Model trong cơ sở dữ liệu mà Django ORM sẽ quản lý

Đầu tiên, tạo một Model để lưu trữ các dữ liệu về Cars sẽ được trả về trong response. Mở file `car/models.py` và nhập đoạn code sau:
```python
from django.db import models

# Create your models here.
class Car(models.Model):
    name = models.CharField(max_length=50)
    color = models.CharField(max_length=20)
    brand = models.CharField(max_length=20)

    def __str__(self):
        return self.name
```

## Serializer
```python
from rest_framework import serializers

from car.models import Car

class CarSerializer(serializers.ModelSerializer):

    class Meta: 
        model = Car
        fields = ('name', 'color', 'brand')
```

## View
```python
from rest_framework import viewsets

from car.models import Car
from car.serializers import CarSerializer

class CarViewSet(viewsets.ModelViewSet):
    queryset = Car.objects.all().order_by('name')
    serializer_class = CarSerializer
```

## Url
```python
from django.urls import include, path
from rest_framework import routers
from . import views

router = routers.DefaultRouter()
router.register(r'cars', views.CarViewSet)

urlpatterns = [
    path('cars', include(router.urls)),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```

Lưu ý rằng chúng tôi đã thêm một thứ gọi là bộ định tuyến `routers` mà chúng tôi đã nhập từ `rest_framework`.

Bộ định tuyến REST Framework sẽ đảm bảo động các yêu cầu của chúng tôi kết thúc tại đúng tài nguyên. Nếu chúng tôi thêm hoặc xóa các mục khỏi cơ sở dữ liệu, các URL sẽ cập nhật để phù hợp. Tuyệt vời phải không?

## Setting
```python
INSTALLED_APPS = [
    ...
    'rest_framework',

    'car.apps.CarConfig'
]
```

Sau khi đã tạo ra được một ứng dụng hoàn chỉnh, việc của chúng ta là tạo migration
```bat
python manage.py makemigrations
python manage.py migrate
```

## Test API
Và cuối cùng thì chúng ta cùng hưởng thành quả nào:
```bat
python manage.py runserver
```

Bây giờ vào [http://127.0.0.1:8000/cars](http://127.0.0.1:8000/cars)

Nếu chúng ta nhấp vào liên kết (Siêu liên kết là thiết kế REST-ful tốt, btw), chúng ta sẽ thấy kết quả API của tất cả cars

### GET một Car cụ thể
Chúng ta có thể NHẬN một phiên bản mô hình duy nhất bằng cách sử dụng ID của nó.

Các bộ khung nhìn Django REST Framework sẽ giải quyết vấn đề này cho chúng ta.

Nếu bạn truy cập `127.0.0.1:8000/cars/<id>/` trong đó `<id>` là ID của một trong các mô hình Car của bạn, bạn sẽ chỉ có thể nhìn thấy Car đó.

Ví dụ: [http://127.0.0.1:8000/cars/1/](http://127.0.0.1:8000/cars/1/)




Khi làm việc với API thì mình thường dùng [Postman](https://www.postman.com) để kiểm tra những API đó

Đây là mã nguồn, vì vậy bạn có thể kiểm tra công việc của mình:
[https://github.com/bennett39/drf_tutorial](https://github.com/bennett39/drf_tutorial)


### Lời kết
Trên đây là toàn bộ quá trình khi mình bắt đầu tìm hiểu và tiếp cận Django Rest.

Tôi hy vọng bạn thích hướng dẫn nhanh này. Tất nhiên, các API có thể phức tạp hơn nhiều với nhiều mô hình giao nhau và các điểm cuối có các truy vấn phức tạp hơn.

Điều đó nói rằng, bạn đang trên con đường của mình với bài đăng này. REST Framework xử lý độ phức tạp khá tốt. Nếu bạn gặp khó khăn, có một cộng đồng tuyệt vời sẵn sàng giúp bạn tìm ra giải pháp.

Chúc bạn vui khi xây dựng một số API mới!

Chúc các bạn thành công trong con đường học tập và tìm hiểu về Django nói chung và Django Rest Framework nói riêng.

Có nhiều công cụ thiết kế API tốt mà giúp tạo ra các tài liệu API rõ ràng như
- [API Blueprint](https://apiblueprint.org)
- [Swagger](https://swagger.io)

-----
Tham khảo:
- [Build a REST API in 30 minutes with Django REST Framework](https://medium.com/swlh/build-your-first-rest-api-with-django-rest-framework-e394e39a482c)
- [How to Develop APIs with Django REST Framework](https://djangostars.com/blog/rest-apis-django-development/)
- [Creating a REST API using Django Rest Framework](https://www.ginkgobioworks.com/2021/02/04/creating-a-rest-api-using-django-rest-framework/)
- [Xây dựng API với Django Rest Framework](https://viblo.asia/p/xay-dung-api-voi-django-rest-framework-Do754PXJ5M6)
- [Django Rest Framework Tutorial - Todo API](https://learndjango.com/tutorials/django-rest-framework-tutorial-todo-api)
- [RESTful API là gì? Cách thiết kế RESTful API](https://topdev.vn/blog/restful-api-la-gi/)
- [Một vài best practice khi xây dựng REST API](https://viblo.asia/p/mot-vai-best-practice-khi-xay-dung-rest-api-3P0lP36PZox)