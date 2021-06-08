---
layout: post
title: Hướng dẫn tạo ứng dụng web Python Flask trên Google App Engine 
subtitle: Lập trình hướng đối tượng với ES5 và ES6
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

Tạo một file `main.py` có nội dung như sau:
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



-----
[Hướng dẫn tạo ứng dụng web Python đơn giản trên Google App Engine](https://viblo.asia/p/huong-dan-tao-ung-dung-web-python-don-gian-tren-google-app-engine-QpmleARnlrd)  
[Deploy ứng dụng Rails với Google app engine-P2: Cài đặt SDK cho máy local](https://viblo.asia/p/deploy-ung-dung-rails-voi-google-app-engine-p2-cai-dat-sdk-cho-may-local-63vKjbGVK2R)  

