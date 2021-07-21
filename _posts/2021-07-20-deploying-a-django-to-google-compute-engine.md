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

1) Tạo Google Cloud `Project` từ [Google Cloud Console](https://console.cloud.google.com/cloud-resource-manager).
2) Tạo tài khoản thanh toán và kích hoạt [thanh toán](https://console.cloud.google.com/billing) cho dự án.
3) Tạo một phiên bản [Virtual Machine](https://console.cloud.google.com/compute/instances).
4) Cấu hình máy có tối thiểu Ram 2 GB, 1 CPU và khu vực `asia-northeast1 (Tokyo)`.
![copmute-engine-configuration-django](https://boxxv.github.io/img/gcp/vm-instances.png "copmute-engine-configuration-django")

5) Cấu hình máy Hệ điều hành Ubuntu và kích thước Ổ cứng và thiết lập cho phép lưu lượng truy cập HTTP và HTTPS:
![copmute-engine-configuration-django](https://boxxv.github.io/img/gcp/vm-instances-2.png "copmute-engine-configuration-django")


## II. Tạo phiên bản Google Cloud SQL.
[https://console.cloud.google.com/sql/instances](https://console.cloud.google.com/sql/instances)

## III. Kết nối với các phiên bản Linux VM

6) Trong danh sách các virtual machine, Thực hiện đăng nhập ssh bằng cách nhấn vào nút `SSH` trong hàng của instance mà bạn muốn kết nối.
![establish-ssh-connection](https://boxxv.github.io/img/gcp/establish-ssh-connection-1.png "establish-ssh-connection")


7) Sau khi kết nối được thiết lập, hãy nhấp vào biểu tượng bánh răng ở phía trên bên phải của SSH từ cửa sổ Trình duyệt và chọn `Upload file`. Ngoài ra, hãy chọn `Download file` để tải tệp xuống từ máy ảo.
![upload-file-ssh-browser](https://boxxv.github.io/img/gcp/upload-file-ssh-browser.png "upload-file-ssh-browser")


## IV. Cài đặt môi trường trên Linux VMs

Chúng ta sẽ cài đặt và định cấu hình máy chủ ứng dụng `Gunicorn`. Điều này sẽ đóng vai trò như một giao diện (interface) cho ứng dụng của chúng ta, dịch các yêu cầu của khách hàng từ các cuộc gọi HTTP sang Python mà ứng dụng của chúng ta có thể xử lý. Sau đó, chúng ta sẽ thiết lập `Nginx` trước Gunicorn để tận dụng các cơ chế xử lý kết nối hiệu suất cao và các tính năng bảo mật dễ triển khai của nó.
![Request Flow](https://boxxv.github.io/img/gcp/1_rYdZRYct2FKHiGxlJIvORg.png "Request Flow")


8) Cập nhật `apt` package index
{% highlight js %}
> sudo apt update
hoặc
> sudo apt update && sudo apt upgrade
{% endhighlight %}


9) Cài đặt `conda`
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


10) Cài đặt các packages cần thiết
{% highlight js %}
conda install -c conda-forge django
conda install -c conda-forge freecad
conda install -c conda-forge pythonocc-core
hoặc
conda install -c conda-forge pythonocc-core=7.5.1
conda install -c conda-forge pandas
conda install -c conda-forge gunicorn

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


11) Cài đặt `nginx`
```bat
sudo apt install nginx curl
```

kiểm tra xem nginx cài đặt thành công hay chưa:
```bat
nginx -v
nginx -V
```

12) Tạo thư mục cho ứng dụng web django
```bat
mkdir ~/mitsumori
```

13) Upload code của dự án vào folder
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

14) 


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
