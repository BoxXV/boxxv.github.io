---
layout: post
title: Hướng dẫn tạo ứng dụng web Python Flask trên Google App Engine 
subtitle: Deploying with a Python Flask web app and Google
image: "img/projects-bg.jpg"
tags:
- Flask
- Python
- GAE
- Google App Engine 
---

Bài hướng dẫn này mình sử dụng microframework Flask làm web app. Những framework khác của Python như Django, Pyramid, Tornado ... có thể làm tương tự. Máy tính client để mình code chạy trên Ubuntu 16.04 cùng với Python 2.7.12.

### Chuẩn bị

Trước khi chạy và deploy ứng dụng Python web, bạn cần phải chuẩn bị

- Sử dụng Cloud Platform để tạo mới Cloud Platform project. Tạo mới một App Engine application và tất nhiên là [enable billing](https://cloud.google.com/billing/docs/how-to/modify-project) tại: [Consle Cloud Google](https://console.cloud.google.com/appengine)

Cài đặt một số tool cần thiết:
- [Git](https://git-scm.com)
- [Google Cloud SDK](https://cloud.google.com/sdk/docs/)


### Tạo web Flask đơn giản

Ở bài hưởng dẫn này, mình sẽ tạo một web đơn giản. Nó sẽ in ra dòng `Hello Word`

Đầu tiên, tạo một thư mục project `hello_world`. Trong thư mực project, ta sẽ tạo lần lượt các file:
- `main.py`: chạy web
- `requirements.txt`: quản lý lib python
- `app.yaml`: cấu hình deploy và chạy code trên Google App Engine

#### 1. Tạo một file `main.py` có nội dung như sau:
```python
import logging

from flask import Flask


app = Flask(__name__)


@app.route('/')
def hello():
    """Return a friendly HTTP greeting."""
    return 'Hello World!'


@app.errorhandler(500)
def server_error(e):
    logging.exception('An error occurred during a request.')
    return """
    An internal error occurred: <pre>{}</pre>
    See logs for full stacktrace.
    """.format(e), 500


if __name__ == '__main__':
    # This is used when running locally. Gunicorn is used to run the
    # application on Google App Engine. See entrypoint in app.yaml.
    app.run(host='127.0.0.1', port=8080, debug=True)
```

#### 2. Tạo một file `requirements.txt` để quản lý các gói
```txt
Flask==0.12.2
gunicorn==19.7.1
```

#### 3. Tiếp theo, bạn chạy thử ứng dụng:

1. Nếu bạn không có `virtualenv` bạn có thể cài đặt chúng qua pip
```python
sudo pip install virtualenv
```

2. Tạo môi trường cô lập và cài đặt các gói cần thiết
```python
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
```

3. Chạy thử
```python
python main.py
```

4. Trên trình duyệt, gõ địa chỉ:
```python
http://localhost:8080
```

![localhost:8080](https://boxxv.github.io/img/posts/d2565015-fab5-4302-8879-a274c7ee7318.png "localhost")_localhost:8080_

### Deploy
Trước khi deploy, bạn cần tạo một file `app.yaml` để cấu hình việc deploy
```python
runtime: python
env: flex
entrypoint: gunicorn -b :$PORT main:app

runtime_config:
  python_version: 2
```

Điểm chú ý ở đây là `env: flex`  
`flex` là tên môi trường mà web app sẽ chạy trên đó. Thông tin cụ thể bạn có thể vào đây: [https://cloud.google.com/appengine/docs/flexible/](https://cloud.google.com/appengine/docs/flexible/)

OK. Tiếp theo là việc deploy.

#### 1. `cd` tới thư mục project `hello_world`. Sau đó, gõ lệnh deploy:
```bat
gcloud app deploy
```

Sau khi bạn cài đặt xong Google Cloud SDK bạn có thể sử dụng CLI `gcloud` để thực hiện deloy app

#### 2. Trên browser bạn có thể xem kết quả của bạn tại `http://YOUR_PROJECT_ID.appspot.com`. Hoặc có thể sử dụng `gcloud`:
```bat
gcloud app browse
```

Đã hoàn thành!!

Điểm mấu chốt của bài hướng dẫn
- Tạo được project trên Goold App Engine
- Cài được CLI `gcloud` tools
- Có một web app Python: tất nhiên rồi
- Chú ý cấu hình trên `app.yaml` file.

Chúc bạn thành công !!!

source code: [https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/appengine/standard_python3/hello_world](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/appengine/standard_python3/hello_world)

[![Introduction App Engine’s new Python 3 Runtime](https://img.youtube.com/vi/qeSpDwA2qcU/0.jpg)](https://www.youtube.com/watch?v=qeSpDwA2qcU)

-----
[Hướng dẫn tạo ứng dụng web Python đơn giản trên Google App Engine](https://viblo.asia/p/huong-dan-tao-ung-dung-web-python-don-gian-tren-google-app-engine-QpmleARnlrd)  
[Deploying Envoy with a Python Flask web app and Google Kubernetes Engine](https://cloud.google.com/community/tutorials/envoy-flask-google-container-engine)  
[Deploy ứng dụng Rails với Google app engine-P2: Cài đặt SDK cho máy local](https://viblo.asia/p/deploy-ung-dung-rails-voi-google-app-engine-p2-cai-dat-sdk-cho-may-local-63vKjbGVK2R)  




