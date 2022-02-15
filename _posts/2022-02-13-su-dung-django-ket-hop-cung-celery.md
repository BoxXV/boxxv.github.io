---
layout: post
title: Sử dụng Django kết hợp cùng Celery
subtitle: Distributed Task Queue

tags:
- Celery
- Queue
- background jobs
- asynchronous task
---

`Celery` là một `asynchronous job queue` cực mạnh. Nó là sự thay thế rất tốt cho contab của Linux. Django là top framework tốt nhất của Python.

![Async task architecture](https://boxxv.github.io/img/posts/async-task-architecture.png "Async task architecture")

## Setup simple Django project

Thực hiện việc tạo project Django cơ bản bằng lện sau:
```bat
% mkdir celery-simple
% cd celery-simple
% virtualenv venv -p python3
Running virtualenv with interpreter /Users/minhhahao/.pyenv/versions/3.6.2/bin/python3
Using base prefix '/Users/minhhahao/.pyenv/versions/3.6.2'
New python executable in /Users/minhhahao/workspace/celery-simple/venv/bin/python3
Also creating executable in /Users/minhhahao/workspace/celery-simple/venv/bin/python
Installing setuptools, pip, wheel...done.
% source venv/bin/activatele
(venv) % pip install django==1.9 celery==4.0
Collecting django==1.9
  Downloading https://files.pythonhosted.org/packages/ea/9b/b5a6360b3dfcd88d4bad70f59da26cbde4bdec395a31bb26dc840e806a50/Django-1.9-py2.py3-none-any.whl (6.6MB)
    100% |████████████████████████████████| 6.6MB 2.2MB/s
Collecting celery==4.0
  Downloading https://files.pythonhosted.org/packages/4b/19/745db97793f786644df142f059beea7c784fa3e856758bb5c18891004d49/celery-4.0.0-py2.py3-none-any.whl (395kB)
    100% |████████████████████████████████| 399kB 2.2MB/s
Collecting pytz>dev (from celery==4.0)
  Downloading https://files.pythonhosted.org/packages/dc/83/15f7833b70d3e067ca91467ca245bae0f6fe56ddc7451aa0dc5606b120f2/pytz-2018.4-py2.py3-none-any.whl (510kB)
    100% |████████████████████████████████| 512kB 9.6MB/s
Collecting billiard<3.6.0,>=3.5.0.2 (from celery==4.0)
  Downloading https://files.pythonhosted.org/packages/82/55/76f4e786141b7174926cdffa7a155aeea316b729118fb48ec548f3c6754f/billiard-3.5.0.3-py3-none-any.whl (89kB)
    100% |████████████████████████████████| 92kB 7.8MB/s
Collecting kombu<5.0,>=4.0 (from celery==4.0)
  Downloading https://files.pythonhosted.org/packages/62/a4/5d16954803224a1e451713293c2a028614099f5538cf626e1fdd7b438c86/kombu-4.1.0-py2.py3-none-any.whl (181kB)
    100% |████████████████████████████████| 184kB 8.6MB/s
Collecting amqp<3.0,>=2.1.4 (from kombu<5.0,>=4.0->celery==4.0)
  Downloading https://files.pythonhosted.org/packages/88/4a/8c45a882d842678963516ebd9cf584a4ded51af719234c3b696c2e884c60/amqp-2.2.2-py2.py3-none-any.whl (48kB)
    100% |████████████████████████████████| 51kB 15.6MB/s
Collecting vine>=1.1.3 (from amqp<3.0,>=2.1.4->kombu<5.0,>=4.0->celery==4.0)
  Downloading https://files.pythonhosted.org/packages/10/50/5b1ebe42843c19f35edb15022ecae339fbec6db5b241a7a13c924dabf2a3/vine-1.1.4-py2.py3-none-any.whl
Installing collected packages: django, pytz, billiard, vine, amqp, kombu, celery
Successfully installed amqp-2.2.2 billiard-3.5.0.3 celery-4.0.0 django-1.9 kombu-4.1.0 pytz-2018.4 vine-1.1.4
(venv) % django-admin startproject simple
(venv) % cd simple
(venv) % python manage.py startapp ce
```

Cấu trúc simple project:
```bat
(venv) % tree
.
├── ce
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations
│   │   └── __init__.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── manage.py
└── simple
    ├── __init__.py
    ├── __pycache__
    │   ├── __init__.cpython-36.pyc
    │   └── settings.cpython-36.pyc
    ├── settings.py
    ├── urls.py
    └── wsgi.py

4 directories, 14 files
```

Sau khi tạo xong, mình tạo một view print "Hello World!" trên web:
```python
# simple/settings.py
# Application definition
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'ce'
]

# simple/urls.py
from django.conf.urls import url, include
from django.contrib import admin


urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^', include('ce.urls'))
]


# ce/urls.py
# Create new file `ce/urls.py` to define url of app ce
from django.conf.urls import url
from ce import views


urlpatterns = [
    url(r'^$', views.index),
]

# ce/views.py
# Define view
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello World!")
```

Run server!
```bat
(venv) % python manage.py runserver                                                                     
Performing system checks...

System check identified no issues (0 silenced).

May 03, 2018 - 02:22:31
Django version 1.9, using settings 'simple.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

## Setup a simple celery task


## 



-----
Tham khảo:
- [Tìm hiểu về Celery](https://viblo.asia/p/tim-hieu-ve-celery-1VgZv4dr5Aw)
- [Giới thiệu Celery](https://viblo.asia/p/gioi-thieu-celery-maGK7mvBlj2)
- [First Steps with Celery](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html)
- [First steps with Django](http://docs.celeryproject.org/en/latest/django/first-steps-with-django.html)
- [Building Your Own Export and Import Data Into Excel Using Django + Celery + Pandas + ❤️ With Progress Bar](https://blog.devgenius.io/building-your-own-export-and-import-data-into-excel-using-django-celery-pandas-%EF%B8%8F-with-784fd688e328)
- [Django channels hướng dẫn cơ bản](https://viblo.asia/p/django-channels-huong-dan-co-ban-3Q75wEjeZWb)