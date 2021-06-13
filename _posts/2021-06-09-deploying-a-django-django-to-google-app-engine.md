---
layout: post
title: Triển khai ứng dụng web Python Django trên Google App Engine
subtitle: Deploying with a Python Django web app and Google
image: "img/projects-bg.jpg"
tags:
- Django
- Python
- GAE
- Google App Engine
---

## Hosting platforms

Đây là các tùy chọn có sẵn để triển khai Django trên Google Cloud: 

| Django deployment option        | Get started           |
| ------------- |:-------------|
| App Engine standard environment | [Running Django on App Engine standard environment](https://cloud.google.com/python/django/appengine) |
| App Engine flexible Environment | [Running Django on App Engine flexible environment](https://cloud.google.com/python/django/flexible-environment) |
| Cloud Run | [Running Django on Cloud Run](https://cloud.google.com/python/django/run), <br>[Running Django on Cloud Run with Cloud Code for VS Code](https://cloud.google.com/code/docs/vscode/quickstart-cloud-run), <br>[Running Django on Cloud Run with Cloud Code for IntelliJ](https://cloud.google.com/code/docs/intellij/quickstart-cloud-run) |
| Google Kubernetes Engine (GKE) | [Running Django on Google Kubernetes Engine](https://cloud.google.com/python/django/kubernetes-engine) |
| Compute Engine | [Django in Google Cloud Marketplace](https://cloud.google.com/marketplace/solution/bitnami-launchpad/djangostack?q=django) |

## Databases
Bộ ánh xạ quan hệ đối tượng Django (ORM) hoạt động tốt nhất với cơ sở dữ liệu quan hệ SQL.

Nếu bạn đang bắt đầu một dự án mới, Cloud SQL là một lựa chọn tốt. Bạn có thể triển khai cơ sở dữ liệu PostgreSQL hoặc MySQL do Google quản lý và mở rộng, và được hỗ trợ bởi Django.


## Chạy Django trên môi trường tiêu chuẩn của App Engine 

Các ứng dụng Django chạy trên môi trường tiêu chuẩn của App Engine sẽ thay đổi tỷ lệ động theo lưu lượng truy cập.

### Chuẩn bị
1. Nếu bạn là người mới sử dụng Google Cloud, hãy [tạo một tài khoản](https://console.cloud.google.com/freetrial) để đánh giá cách các sản phẩm của chúng tôi hoạt động trong các tình huống thực tế. Khách hàng mới cũng nhận được 300 đô la tín dụng miễn phí để chạy, thử nghiệm và triển khai khối lượng công việc.

2. Trong Google Cloud Console, trên trang chọn dự án, hãy chọn hoặc tạo một dự án Google Cloud.  
<a href="https://console.cloud.google.com/projectselector2/home/dashboard" target="_blank">Go to project selector</a>

3. Đảm bảo rằng thanh toán được bật cho dự án Đám mây của bạn. Tìm hiểu cách xác nhận rằng [thanh toán được bật](https://cloud.google.com/billing/docs/how-to/modify-project) cho dự án của bạn. 

4. Bật Cloud SQL Admin API  
<a href="https://console.cloud.google.com/flows/enableapi?apiid=sqladmin.googleapis.com" target="_blank">Enable the API</a>

5. Cài đặt và khởi chạy [Cloud SDK](https://cloud.google.com/sdk/docs/install)


#### Đăng nhập `gcloud`
Nhận thông tin đăng nhập mới để sử dụng Cloud SQL Admin API:
```bat
gcloud auth application-default login
```

### Tải xuống và chạy ứng dụng mẫu

source code: [https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/appengine/standard_python3/django](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/appengine/standard_python3/django)


### Setting up your local environment

Khi được triển khai, ứng dụng của bạn sử dụng Cloud SQL Proxy được tích hợp sẵn trong môi trường App Engine để giao tiếp với phiên bản Cloud SQL của bạn. Tuy nhiên, để kiểm tra cục bộ ứng dụng của bạn, bạn phải cài đặt và sử dụng bản sao cục bộ của proxy trong môi trường phát triển của mình.

Tìm hiểu thêm về [Cloud SQL Proxy](https://cloud.google.com/sql/docs/postgres/sql-proxy).

Để thực hiện các tác vụ quản trị cơ bản trên phiên bản Cloud SQL của bạn, bạn có thể sử dụng ứng dụng PostgreSQL client.


#### Installing the Cloud SQL Proxy

Tải xuống và cài đặt `Cloud SQL Proxy`. `Cloud SQL Proxy` kết nối với phiên bản `Cloud SQL` của bạn khi chạy cục bộ. 

Windows 64-bit: [https://dl.google.com/cloudsql/cloud_sql_proxy_x64.exe](https://dl.google.com/cloudsql/cloud_sql_proxy_x64.exe)


#### Creating a Cloud SQL instance

1. [Create a Cloud SQL for MySQL Second Generation instance](https://cloud.google.com/sql/docs/mysql/create-instance).

Đặt tên cho instance `polls-instance` hoặc tương tự. Có thể mất vài phút để phiên bản sẵn sàng. Khi phiên bản đã sẵn sàng, nó sẽ hiển thị trong danh sách phiên bản. 

2. Sử dụng Cloud SDK để chạy lệnh sau trong đó [YOUR_INSTANCE_NAME] đại diện cho tên của phiên bản Cloud SQL của bạn: 
```bat
gcloud sql instances describe [YOUR_INSTANCE_NAME]
```

Trong đầu ra, lưu ý giá trị được hiển thị cho `[CONNECTION_NAME]`.

Giá trị `[CONNECTION_NAME]` có định dạng `[PROJECT_NAME]: [REGION_NAME]: [INSTANCE_NAME]`.


#### Initializing your Cloud SQL instance

1. Khởi động Cloud SQL Proxy bằng cách sử dụng giá trị `[CONNECTION_NAME]` từ bước trước: 
```bat
cloud_sql_proxy.exe -instances="[YOUR_INSTANCE_CONNECTION_NAME]"=tcp:3306
```

Thay thế `[YOUR_INSTANCE_CONNECTION_NAME]` bằng giá trị `[CONNECTION_NAME]` mà bạn đã ghi ở bước trước.

Bước này thiết lập kết nối từ máy tính cục bộ của bạn đến phiên bản Cloud SQL của bạn cho mục đích kiểm tra cục bộ. Giữ cho Cloud SQL Proxy chạy trong toàn bộ thời gian bạn kiểm tra ứng dụng của mình cục bộ.

2. Tạo cơ sở dữ liệu và người dùng Cloud SQL:

Cloud Console
a. Tạo [new database by using the Cloud Console](https://cloud.google.com/sql/docs/mysql/create-manage-databases#create) cho `polls-instance` Cloud SQL của bạn. Ví dụ, bạn có thể sử dụng các cuộc thăm dò tên.

b. Tạo [new user by using the Cloud Console](https://cloud.google.com/sql/docs/mysql/create-manage-users#creating) cho phiên bản `polls-instance` Cloud SQL của bạn.


### Configuring the database settings



### Running the app on your local computer
```bat
python manage.py runserver
```

### Using the Django admin console
```bat
python manage.py createsuperuser
```


### Deploying the app to the App Engine standard environment
```bat
python manage.py collectstatic

gcloud app deploy
```

### Seeing the app run in Google Cloud

Lệnh sau triển khai ứng dụng như được mô tả trong `app.yaml` và đặt phiên bản mới được triển khai làm phiên bản mặc định, khiến nó phân phát tất cả lưu lượng truy cập mới.

Trong trình duyệt của bạn, hãy nhập URL sau:

https://`PROJECT_ID`.`REGION_ID`.r.appspot.com

Thay thế những điều sau:
- `PROJECT_ID`: ID dự án Google Cloud của bạn
- `REGION_ID`: Mã mà App Engine chỉ định cho ứng dụng của bạn 

Yêu cầu của bạn được phục vụ bởi một máy chủ web chạy trong môi trường tiêu chuẩn của App Engine.

Nếu bạn cập nhật ứng dụng của mình, bạn triển khai phiên bản cập nhật bằng cách nhập cùng một lệnh mà bạn đã sử dụng để triển khai ứng dụng. Việc triển khai tạo ra một [phiên bản mới](https://console.cloud.google.com/projectselector2/appengine/versions) của ứng dụng của bạn và quảng bá nó lên phiên bản mặc định. Các phiên bản trước đó của ứng dụng của bạn vẫn còn. Tất cả các phiên bản ứng dụng này đều là tài nguyên có thể thanh toán. Để giảm chi phí, hãy xóa các phiên bản không phải mặc định của ứng dụng.

Để biết thông tin về cách xóa các phiên bản không phải mặc định của ứng dụng, hãy xem [Cleaning up](https://cloud.google.com/python/getting-started/delete-tutorial-resources).



[![Deploy Django Website to Google Cloud](https://img.youtube.com/vi/8Vxo0P_P8TU/0.jpg)](https://www.youtube.com/watch?v=8Vxo0P_P8TU)


[![How to Deploy Django to Google Cloud in One Click](https://img.youtube.com/vi/NcgcN2t19ww/0.jpg)](https://www.youtube.com/watch?v=NcgcN2t19ww)

-----
[Running Django on the App Engine standard environment](https://cloud.google.com/python/django/appengine)  
[Deploying a Django Application to Google App Engine](https://bennettgarner.medium.com/deploying-a-django-application-to-google-app-engine-f9c91a30bd35)  
[Get started with Bitnami Django on Google Cloud](https://cloud.google.com/community/tutorials/get-started-bitnami-django)  
[Using SQLITE for local Django development for Google App Engine?](https://stackoverflow.com/questions/21302612/using-sqlite-for-local-django-development-for-google-app-engine)  
[Deploy ứng dụng Rails với Google app engine-P2: Cài đặt SDK cho máy local](https://viblo.asia/p/deploy-ung-dung-rails-voi-google-app-engine-p2-cai-dat-sdk-cho-may-local-63vKjbGVK2R)  

