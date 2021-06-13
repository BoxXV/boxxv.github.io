---
layout: post
title: Triển khai ứng dụng web Python Django trên Google Compute Engine
subtitle: Deploying with a Python Django web app and Google
image: "img/projects-bg.jpg"
tags:
- Django
- Python
- GAE
- Google Compute Engine
---

## [Google Compute Engine](https://cloud.google.com/compute)

Cơ sở hạ tầng như một Dịch vụ để chạy các máy ảo Microsoft Windows và Linux.

- `Predefined machine types`: Loại máy được xác định trước. Bắt đầu chạy nhanh chóng với các cấu hình được tạo sẵn và sẵn sàng sử dụng
- `Custom machine types`: Loại máy tùy chỉnh. Tạo máy ảo với số lượng vCPU và bộ nhớ tối ưu, đồng thời cân bằng chi phí
- `Preemptible machines`: Máy có quyền mua trước. Giảm chi phí bằng cách tăng tính tới 80% với trường hợp ngắn hạn giá cả phải chăng
- `Confidential computing`: Máy tính bí mật. Mã hóa dữ liệu nhạy cảm nhất của bạn khi dữ liệu đang được xử lý
- `Rightsizing recommendations`: Đề xuất kích thước phù hợp. Tối ưu hóa việc sử dụng tài nguyên với các đề xuất tự động

## Chọn loại máy ảo phù hợp

### Day-to-day computing (E2) - Máy tính hàng ngày

[`E2 machines`](https://cloud.google.com/compute/docs/machine-types#e2_machine_types) cung cấp mức giá theo yêu cầu thấp nhất cho máy tính đa năng và hỗ trợ lên đến 32 vCPU và bộ nhớ 128 GB. Chúng tốt cho các dịch vụ vi mô, máy tính để bàn ảo và môi trường phát triển.

### Balanced price and performance (N2, N2D, N1) - Giá cả và hiệu suất cân bằng



-----
[Deploy Django on Google Compute Engine with Nginx, Gunicorn and Postgresql (Google Cloud SQL)](https://djangocircle.com/deploy-django-on-google-compute-engine-with-nginx-gunicorn-and-postgresql-google-cloud-sql/)  
[Deploy Django to GCP Compute Engine](https://www.minimalistbeing.com/blog/django-deployment-gcp-compute-engine/)  
[Get started with Bitnami Django on Google Cloud](https://cloud.google.com/community/tutorials/get-started-bitnami-django)  
[Using SQLITE for local Django development for Google App Engine?](https://stackoverflow.com/questions/21302612/using-sqlite-for-local-django-development-for-google-app-engine)  
[Deploy ứng dụng Rails với Google app engine-P2: Cài đặt SDK cho máy local](https://viblo.asia/p/deploy-ung-dung-rails-voi-google-app-engine-p2-cai-dat-sdk-cho-may-local-63vKjbGVK2R)  

