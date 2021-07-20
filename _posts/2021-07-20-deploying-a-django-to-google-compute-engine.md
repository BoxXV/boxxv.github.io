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

## Tạo phiên bản Compute Engine Virtual Machine (VM instances)

Chi phí của Google Compute Engine phụ thuộc vào phân bổ CPU, Bộ nhớ và Hardisk.

1. Tạo Google Cloud `Project` từ [Google Cloud Console](https://console.cloud.google.com/cloud-resource-manager).
2. Tạo tài khoản thanh toán và kích hoạt [thanh toán](https://console.cloud.google.com/billing) cho dự án.
3. Tạo một phiên bản [Virtual Machine](https://console.cloud.google.com/compute/instances).
4. Cấu hình máy có tối thiểu Ram 2 GB, 1 CPU và khu vực `asia-northeast1 (Tokyo)`.
![copmute-engine-configuration-django](https://boxxv.github.io/img/gcp/vm-instances.png "copmute-engine-configuration-django")

5. Cấu hình máy Hệ điều hành Ubuntu và kích thước Ổ cứng và thiết lập cho phép lưu lượng truy cập HTTP và HTTPS:
![copmute-engine-configuration-django](https://boxxv.github.io/img/gcp/vm-instances-2.png "copmute-engine-configuration-django")

## Tạo phiên bản Google Cloud SQL.
[https://console.cloud.google.com/sql/instances](https://console.cloud.google.com/sql/instances)

## Cài đặt Nginx trên Google Compute Engine

6. Thực hiện đăng nhập ssh bằng cách nhấn vào nút `SSH` như được hiển thị trong ảnh chụp màn hình bên dưới.



## Issues
[Collecting package metadata (repodata.json): / Killed](https://github.com/conda/conda/issues/9728)

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
