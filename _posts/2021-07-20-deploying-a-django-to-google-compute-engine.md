---
layout: post
title: Triển khai ứng dụng web Python Django trên Google Compute Engine
subtitle: Deploying with a Python Django web app and Google
image: "img/projects-bg.jpg"
tags:
- Django
- Python
- GCE
- Google Compute Engine
---

## I. Tạo phiên bản Compute Engine Virtual Machine (VM instances)

Chi phí của Google Compute Engine phụ thuộc vào phân bổ CPU, Bộ nhớ và Hardisk.

__1)__ Tạo Google Cloud `Project` từ [Google Cloud Console](https://console.cloud.google.com/cloud-resource-manager).  
__2)__ Tạo tài khoản thanh toán và kích hoạt [thanh toán](https://console.cloud.google.com/billing) cho dự án.  
__3)__ Tạo một phiên bản [Virtual Machine](https://console.cloud.google.com/compute/instances).  
__4)__ Cấu hình máy có tối thiểu Ram 2 GB, 1 CPU và khu vực `asia-northeast1 (Tokyo)`.  
![copmute-engine-configuration-django](https://boxxv.github.io/img/gcp/vm-instances.png "copmute-engine-configuration-django")

__5)__ Cấu hình máy Hệ điều hành Ubuntu và kích thước Ổ cứng và thiết lập cho phép lưu lượng truy cập HTTP và HTTPS:
![copmute-engine-configuration-django](https://boxxv.github.io/img/gcp/vm-instances-2.png "copmute-engine-configuration-django")


## II. Tạo phiên bản Google Cloud SQL.
[https://console.cloud.google.com/sql/instances](https://console.cloud.google.com/sql/instances)

## III. Kết nối với các phiên bản Linux VM

__6)__ Trong danh sách các virtual machine, Thực hiện đăng nhập ssh bằng cách nhấn vào nút `SSH` trong hàng của instance mà bạn muốn kết nối.
![establish-ssh-connection](https://boxxv.github.io/img/gcp/establish-ssh-connection-1.png "establish-ssh-connection")


__7)__ Sau khi kết nối được thiết lập, hãy nhấp vào biểu tượng bánh răng ở phía trên bên phải của SSH từ cửa sổ Trình duyệt và chọn `Upload file`. Ngoài ra, hãy chọn `Download file` để tải tệp xuống từ máy ảo.
![upload-file-ssh-browser](https://boxxv.github.io/img/gcp/upload-file-ssh-browser.png "upload-file-ssh-browser")


## IV. Cài đặt môi trường trên Linux VMs

Chúng ta sẽ cài đặt và định cấu hình máy chủ ứng dụng `Gunicorn`. Điều này sẽ đóng vai trò như một giao diện (interface) cho ứng dụng của chúng ta, dịch các yêu cầu của khách hàng từ các cuộc gọi HTTP sang Python mà ứng dụng của chúng ta có thể xử lý. Sau đó, chúng ta sẽ thiết lập `Nginx` trước Gunicorn để tận dụng các cơ chế xử lý kết nối hiệu suất cao và các tính năng bảo mật dễ triển khai của nó.
![Request Flow](https://boxxv.github.io/img/gcp/1_rYdZRYct2FKHiGxlJIvORg.png "Request Flow")


__8) Cập nhật `apt` package index__
{% highlight js %}
> sudo apt update
hoặc
> sudo apt update && sudo apt upgrade
{% endhighlight %}


__9) Cài đặt `conda`__
Tải xuống và cài đặt thủ công Miniconda

```bat
wget "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh"
bash Miniconda3-latest-Linux-x86_64.sh

hoặc

wget "https://repo.anaconda.com/miniconda/Miniconda3-py39_4.9.2-Linux-x86_64.sh"
bash Miniconda3-py39_4.9.2-Linux-x86_64.sh
```
Làm theo hướng dẫn để hoàn tất cài đặt

Note: đóng `SSH from the Browser` sau đó mở lại SSH Browser và kiểm tra xem Conda đã cài đặt thành công hay chưa:
```bat
conda list

hoặc
conda --version
python --version
python -V
```

Tham khảo thêm tại:  
[Linux installers](https://docs.conda.io/en/latest/miniconda.html#linux-installers)  
[Installing on Linux](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html)


__10) Cài đặt các packages cần thiết__
{% highlight js %}
conda install -c conda-forge django
conda install -c conda-forge freecad
conda install -c conda-forge pythonocc-core
hoặc
conda install -c conda-forge pythonocc-core=7.5.1
conda install -c conda-forge djangorestframework
conda install -c conda-forge pandas
conda install -c conda-forge gunicorn

conda install -c conda-forge pyvirtualdisplay

pip install django-allauth
pip install django-background-tasks

conda install -c conda-forge matplotlib
{% endhighlight %}

kiểm tra xem các packages cài đặt thành công hay chưa:
```bat
conda list

hoặc
python -m django --version
which python
which freecad
hoặc
where python
where freecad
sudo find / -iname FreeCAD.so
```


__11) Cài đặt `nginx`__
```bat
sudo apt install nginx curl
```

kiểm tra xem nginx cài đặt thành công hay chưa:
```bat
nginx -v
nginx -V
```


__12) Tạo thư mục cho ứng dụng web django__
```bat
mkdir ~/myprojectdir
hoặc
mkdir ~/mitsumori
```


__13) Upload code của dự án vào folder__
Tại thư mục gốc của dự án có chứa manage.py và db.sqlite3
- nén code dự án, chẳng hạn với tên up.zip
- upload up.zip như ở bước số 7
- up.zip sẽ nằm ở /home/{username}/up.zip
- giải nén up.zip với lệnh

```bat
# Cài đặt unzip
sudo apt install unzip

unzip up.zip -d mitsumori

# Giải nén với tùy chọn ghi đè tệp
unzip -o up.zip -d mitsumori
```

## V. Tạo systemd Socket và tệp Service cho Gunicorn
Tiếp theo chúng ta sẽ triển khai cách khởi động và dừng máy chủ ứng dụng. Gunicorn socket sẽ được tạo khi khởi động và sẽ lắng nghe các kết nối. Khi kết nối xảy ra, systemd sẽ tự động bắt đầu quá trình Gunicorn để xử lý kết nối.

Tham khảo thêm tại: [creating-systemd-socket-and-service-files-for-gunicorn](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-20-04#creating-systemd-socket-and-service-files-for-gunicorn)


__14) Tạo và mở tệp socket systemd cho Gunicorn với các đặc quyền sudo__
```bat
sudo nano /etc/systemd/system/gunicorn.socket
```

Bên trong, chúng tôi sẽ tạo phần `[Unit]` để mô tả socket, phần `[Socket]` để xác định vị trí socket và phần `[Install]` để đảm bảo socket được tạo vào đúng thời điểm:

{% highlight js %}
[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target
{% endhighlight %}

Lưu và đóng tệp khi bạn hoàn tất.


__15) Tạo tệp dịch vụ systemd cho Gunicorn__

Tên tệp dịch vụ phải khớp với tên tệp socket ngoại trừ phần mở rộng

```bat
sudo nano /etc/systemd/system/gunicorn.service
```

Bắt đầu với phần `[Unit]`, được sử dụng để chỉ định siêu dữ liệu và phần phụ thuộc. Chúng tôi sẽ đặt mô tả về dịch vụ của mình ở đây và yêu cầu hệ thống init chỉ bắt đầu việc này sau khi đã đạt được mục tiêu mạng. Vì dịch vụ của chúng tôi dựa vào socket từ tệp socket, chúng tôi cần bao gồm chỉ thị `Requires ` để chỉ ra mối quan hệ đó

Tiếp theo, chúng tôi sẽ mở phần `[Service]`. Chúng tôi sẽ chỉ định người dùng và nhóm mà chúng tôi muốn xử lý để điều hành. Chúng tôi sẽ cấp cho tài khoản người dùng thông thường quyền sở hữu quy trình vì nó sở hữu tất cả các tệp có liên quan. Chúng tôi sẽ cấp quyền sở hữu nhóm cho nhóm `www-data` để Nginx có thể giao tiếp dễ dàng với Gunicorn.

Sau đó, chúng tôi sẽ vạch ra thư mục làm việc và chỉ định lệnh sử dụng để bắt đầu dịch vụ. Trong trường hợp này, chúng tôi sẽ phải chỉ định đường dẫn đầy đủ đến tệp thi hành Gunicorn, tệp này được cài đặt trong môi trường ảo của chúng tôi. Chúng tôi sẽ liên kết quy trình với ổ cắm Unix mà chúng tôi đã tạo trong thư mục `/run` để quy trình có thể giao tiếp với Nginx. Chúng tôi ghi lại tất cả dữ liệu vào đầu ra tiêu chuẩn để quá trình `journald` có thể thu thập nhật ký Gunicorn. Chúng tôi cũng có thể chỉ định bất kỳ chỉnh sửa Gunicorn tùy chọn nào tại đây. Ví dụ: chúng tôi đã chỉ định 3 quy trình công nhân trong trường hợp này: 

{% highlight js %}
[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User={username}
Group=www-data
WorkingDirectory=/home/{username}/myprojectdir
ExecStart=/home/{username}/miniconda3/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          myproject.wsgi:application
{% endhighlight %}

Khi triển khai thật, thay bằng tên trong dự án thực tế:
- thay `{username}` => `tanvd`
- thay `myprojectdir` => `mitsumori`
- thay `myproject.wsgi` => `estimate_info.wsgi`

Với điều đó, tệp dịch vụ systemd của chúng ta đã hoàn tất. Lưu và đóng nó ngay bây giờ.


__16) Khởi động và kích hoạt ổ cắm Gunicorn__
Thao tác này sẽ tạo tệp socket tại `/run/gunicorn.sock` ngay bây giờ và khi khởi động. Khi kết nối được thực hiện với socket đó, systemd sẽ tự động khởi động gunicorn.service để xử lý nó:

```bat
sudo systemctl start gunicorn.socket
sudo systemctl enable gunicorn.socket
```

Chúng tôi có thể xác nhận rằng thao tác đã thành công bằng cách kiểm tra tệp socket.

## VI. Kiểm tra tệp Gunicorn Socket

__17)__ Kiểm tra trạng thái của quá trình để tìm hiểu xem liệu quá trình có thể bắt đầu hay không
```bat
sudo systemctl status gunicorn.socket
```

Bạn sẽ nhận được một đầu ra như thế này: 

{% highlight js %}
Output
● gunicorn.socket - gunicorn socket
     Loaded: loaded (/etc/systemd/system/gunicorn.socket; enabled; vendor prese>
     Active: active (listening) since Fri 2020-06-26 17:53:10 UTC; 14s ago
   Triggers: ● gunicorn.service
     Listen: /run/gunicorn.sock (Stream)
      Tasks: 0 (limit: 1137)
     Memory: 0B
     CGroup: /system.slice/gunicorn.socket
{% endhighlight %}


__18)__ Kiểm tra sự tồn tại của tệp `gunicorn.sock` trong thư mục `/run`

```bat
file /run/gunicorn.sock
```

{% highlight js %}
Output
/run/gunicorn.sock: socket
{% endhighlight %}

Nếu lệnh `systemctl status` cho biết rằng đã xảy ra lỗi hoặc nếu bạn không tìm thấy tệp `gunicorn.sock` trong thư mục, thì đó là dấu hiệu cho thấy không thể tạo đúng ổ cắm Gunicorn. Kiểm tra nhật ký của ổ cắm Gunicorn bằng cách nhập: 

```bat
sudo journalctl -u gunicorn.socket
```
Hãy xem lại tệp `/etc/systemd/system/gunicorn.socket` của bạn để khắc phục bất kỳ sự cố nào trước khi tiếp tục.


## VII. Kiểm tra kích hoạt Socket

Hiện tại, nếu bạn chỉ khởi động đơn vị `gunicorn.socket`, thì `gunicorn.service` sẽ chưa hoạt động vì socket chưa nhận được bất kỳ kết nối nào.

```bat
sudo systemctl status gunicorn
```

{% highlight js %}
Output
● gunicorn.service - gunicorn daemon
   Loaded: loaded (/etc/systemd/system/gunicorn.service; disabled; vendor preset: enabled)
   Active: inactive (dead)
{% endhighlight %}


__19)__ Kiểm tra cơ chế kích hoạt socket, chúng ta có thể gửi kết nối đến ổ cắm thông qua curl

```bat
curl --unix-socket /run/gunicorn.sock localhost
```

Bạn sẽ nhận được đầu ra HTML từ ứng dụng của mình trong thiết bị đầu cuối. Điều này cho thấy rằng Gunicorn đã được khởi động và có thể phục vụ ứng dụng Django của bạn.

Bạn có thể xác minh rằng dịch vụ Gunicorn đang chạy bằng cách nhập:
```bat
sudo systemctl status gunicorn
```

{% highlight js %}
Output

● gunicorn.service - gunicorn daemon
     Loaded: loaded (/etc/systemd/system/gunicorn.service; disabled; vendor preset: enabled)
     Active: active (running) since Fri 2020-06-26 18:52:21 UTC; 2s ago
TriggeredBy: ● gunicorn.socket
   Main PID: 22914 (gunicorn)
      Tasks: 4 (limit: 1137)
     Memory: 89.1M
     CGroup: /system.slice/gunicorn.service
             ├─22914 /home/sammy/myprojectdir/myprojectenv/bin/python /home/sammy/myprojectdir/myprojectenv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunico>
             ├─22927 /home/sammy/myprojectdir/myprojectenv/bin/python /home/sammy/myprojectdir/myprojectenv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunico>
             ├─22928 /home/sammy/myprojectdir/myprojectenv/bin/python /home/sammy/myprojectdir/myprojectenv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunico>
             └─22929 /home/sammy/myprojectdir/myprojectenv/bin/python /home/sammy/myprojectdir/myprojectenv/bin/gunicorn --access-logfile - --workers 3 --bind unix:/run/gunico>

Jun 26 18:52:21 django-tutorial systemd[1]: Started gunicorn daemon.
Jun 26 18:52:21 django-tutorial gunicorn[22914]: [2020-06-26 18:52:21 +0000] [22914] [INFO] Starting gunicorn 20.0.4
Jun 26 18:52:21 django-tutorial gunicorn[22914]: [2020-06-26 18:52:21 +0000] [22914] [INFO] Listening at: unix:/run/gunicorn.sock (22914)
Jun 26 18:52:21 django-tutorial gunicorn[22914]: [2020-06-26 18:52:21 +0000] [22914] [INFO] Using worker: sync
Jun 26 18:52:21 django-tutorial gunicorn[22927]: [2020-06-26 18:52:21 +0000] [22927] [INFO] Booting worker with pid: 22927
Jun 26 18:52:21 django-tutorial gunicorn[22928]: [2020-06-26 18:52:21 +0000] [22928] [INFO] Booting worker with pid: 22928
Jun 26 18:52:21 django-tutorial gunicorn[22929]: [2020-06-26 18:52:21 +0000] [22929] [INFO] Booting worker with pid: 22929
{% endhighlight %}

Nếu đầu ra từ `curl` hoặc đầu ra của `systemctl status` cho biết rằng đã xảy ra sự cố, hãy kiểm tra nhật ký để biết thêm chi tiết:
```bat
sudo journalctl -u gunicorn
```

Kiểm tra tệp `/etc/systemd/system/gunicorn.service` của bạn xem có vấn đề gì không. Nếu bạn thực hiện thay đổi đối với tệp `/etc/systemd/system/gunicorn.service`, hãy tải lại daemon để đọc lại định nghĩa dịch vụ và khởi động lại quy trình Gunicorn bằng cách nhập: 

```bat
sudo systemctl daemon-reload
sudo systemctl restart gunicorn
```

Đảm bảo bạn khắc phục sự cố ở trên trước khi tiếp tục.


## VIII. Cấu hình Nginx thành Proxy Pass tới Gunicorn

Bây giờ Gunicorn đã được thiết lập, chúng ta cần định cấu hình Nginx để chuyển lưu lượng truy cập vào quy trình.


__20)__ Tạo và mở một block máy chủ mới trong thư mục có sẵn trên các trang web của Nginx

```bat
sudo nano /etc/nginx/sites-available/myproject
hoặc
sudo nano /etc/nginx/sites-available/mitsumori.conf
```

Bên trong, mở một block máy chủ mới. Chúng tôi sẽ bắt đầu bằng cách chỉ định rằng khối này sẽ lắng nghe trên cổng thông thường `80` và nó sẽ phản hồi với tên miền hoặc địa chỉ IP của máy chủ của chúng ta

Tiếp theo, chúng tôi sẽ yêu cầu Nginx bỏ qua bất kỳ vấn đề nào với việc tìm biểu tượng yêu thích. Chúng tôi cũng sẽ cho nó biết nơi tìm các tài sản tĩnh mà chúng tôi đã thu thập trong thư mục `~/myprojectdir/` static của chúng tôi. Tất cả các tệp này đều có tiền tố URI tiêu chuẩn là `“/static”`, vì vậy chúng tôi có thể tạo khối vị trí để khớp với các yêu cầu đó: 

{% highlight js %}
server {
    listen 80;
    server_name {server_domain_or_IP};

    location = /favicon.ico { access_log off; log_not_found off; }
    location /static/ {
        root /home/{username}/myprojectdir;
    }
}
{% endhighlight %}

Khi triển khai thật, thay bằng tên trong dự án thực tế:
- thay `{username}` => `tanvd`
- thay `myprojectdir` => `mitsumori`
- thay `server_domain_or_IP` => `123.45.6.78` hoặc `example.com`

Lưu và đóng tệp khi bạn hoàn tất.


__21)__ Kích hoạt tệp bằng cách liên kết tệp với thư mục hỗ trợ trang web

```bat
sudo ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled

hoặc
sudo ln -s /etc/nginx/sites-available/mitsumori.conf /etc/nginx/sites-enabled/mitsumori.conf
```


__22)__ Kiểm tra cấu hình Nginx của bạn để tìm lỗi cú
```bat
sudo nginx -t
```

Nếu không có lỗi nào được báo cáo, hãy tiếp tục


__23)__ Khởi động lại Nginx
```bat
sudo systemctl restart nginx
```



## Issues
[Collecting package metadata (repodata.json): / Killed](https://github.com/conda/conda/issues/9728)  
Cách khác phục: Adding ram from 0.5 GB to 2GB RAM also solved my issue

[ImportError: libGL.so.1: cannot open shared object file: No such file or directory](https://stackoverflow.com/a/67302144/15518966)  
[ImportError: libGL.so.1: cannot open shared object file: No such file or directory](https://github.com/conda-forge/pygridgen-feedstock/issues/10)  
Cách khác phục: sudo apt install libgl1-mesa-glx




-----
[Deploy Django on Google Compute Engine with Nginx, Gunicorn and Postgresql (Google Cloud SQL)](https://djangocircle.com/deploy-django-on-google-compute-engine-with-nginx-gunicorn-and-postgresql-google-cloud-sql/)  
[How To Set Up Django with Postgres, Nginx, and Gunicorn on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-20-04)  
[How To Set Up Django with Postgres, Nginx, and Gunicorn on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-18-04)  
[How To Set Up Django with Postgres, Nginx, and Gunicorn on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-16-04)  
[How To Install Django and Set Up a Development Environment on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-django-and-set-up-a-development-environment-on-ubuntu-16-04)  
[How To Set Up Django with Postgres, Nginx, and Gunicorn on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-14-04)  
[Setting Up Django with MySQL, Nginx, and Gunicorn on Ubuntu 18.04](https://codeforcore.com/2020/2474/)  
[Deploy Django to GCP Compute Engine](https://www.minimalistbeing.com/blog/django-deployment-gcp-compute-engine/)  
[Get started with Bitnami Django on Google Cloud](https://cloud.google.com/community/tutorials/get-started-bitnami-django)  
[https://www.x.org](https://www.x.org/releases/X11R7.6/doc/man/man1/Xvfb.1.xhtml)  
[https://anaconda.org/conda-forge/pyvirtualdisplay](https://anaconda.org/conda-forge/pyvirtualdisplay)  
