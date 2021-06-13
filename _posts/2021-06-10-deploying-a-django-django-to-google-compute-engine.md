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

[`N2`](https://cloud.google.com/compute/docs/machine-types#n2_machine_types), [`N2D`](https://cloud.google.com/compute/docs/machine-types#n2d_machine_types) và [`N1`](https://cloud.google.com/compute/docs/machine-types#n1_machine_types) là các máy đa dụng thế hệ thứ hai cung cấp tỷ lệ hiệu suất giá cả tốt nhất. Chúng hỗ trợ lên đến 224 vCPU và 896 GB bộ nhớ và rất tốt cho việc phân phát web, phân phát ứng dụng và các ứng dụng văn phòng.


### Ultra-high memory (M2, M1) - Bộ nhớ cực cao

[`Memory-optimized machines`](https://cloud.google.com/compute/docs/machine-types#memory-optimized_machine_type_family) cung cấp cấu hình bộ nhớ cao nhất với tối đa 12 TB cho một phiên bản. Chúng rất phù hợp với khối lượng công việc sử dụng nhiều bộ nhớ như cơ sở dữ liệu lớn trong bộ nhớ như SAP HANA và khối lượng công việc phân tích dữ liệu trong bộ nhớ.


### Compute-intensive workloads (C2) - Khối lượng công việc sử dụng máy tính nhiều

[`Compute-optimized machines`](https://cloud.google.com/compute/docs/machine-types#compute-optimized_machine_type_family) cung cấp hiệu suất cao nhất trên mỗi lõi trên Compute Engine và được tối ưu hóa cho các khối lượng công việc như máy tính hiệu suất cao (HPC), máy chủ trò chơi và cung cấp API nhạy cảm với độ trễ.


### Most demanding applications and workloads (A2) - Các ứng dụng và khối lượng công việc đòi hỏi khắt khe nhất (A2)

[`Accelerator-optimized machines`](https://cloud.google.com/compute/docs/machine-types#accelerator-optimized_machine_type_family) dựa trên GPU NVIDIA Ampere A100 Tensor Core. Mỗi GPU A100 cung cấp hiệu suất tính toán gấp 20 lần so với GPU thế hệ trước. Các máy ảo này được thiết kế cho các khối lượng công việc đòi hỏi khắt khe nhất của bạn như máy học và máy tính hiệu suất cao.





-----
[Deploy Django on Google Compute Engine with Nginx, Gunicorn and Postgresql (Google Cloud SQL)](https://djangocircle.com/deploy-django-on-google-compute-engine-with-nginx-gunicorn-and-postgresql-google-cloud-sql/)  
[Deploy Django to GCP Compute Engine](https://www.minimalistbeing.com/blog/django-deployment-gcp-compute-engine/)  
[Get started with Bitnami Django on Google Cloud](https://cloud.google.com/community/tutorials/get-started-bitnami-django)  
[Using SQLITE for local Django development for Google App Engine?](https://stackoverflow.com/questions/21302612/using-sqlite-for-local-django-development-for-google-app-engine)  
[Deploy ứng dụng Rails với Google app engine-P2: Cài đặt SDK cho máy local](https://viblo.asia/p/deploy-ung-dung-rails-voi-google-app-engine-p2-cai-dat-sdk-cho-may-local-63vKjbGVK2R)  

