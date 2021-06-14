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

Chi phí của sản phẩm Google Compute Engine phụ thuộc vào phân bổ CPU, Bộ nhớ và Hardisk của bạn. Sản phẩm của Google Compute Engine tính phí với chính sách "thanh toán khi bạn di chuyển". Nếu chúng ta tạo một máy với 1 CPU, Bộ nhớ 0,6 GB và ổ cứng SSD 10 GB trong 730 giờ một tháng, nó sẽ có giá 3,88 đô la (cho VM) và 1,7 đô la (10 GB SSD), tổng cộng là 5,58 đô la. Cấu hình này đủ để chạy ứng dụng trang web Django CMS. Điều này sẽ khiến tất cả các Cơ quan Tiếp thị Kỹ thuật số và Cơ quan Thiết kế Trang web nghĩ lại về chi phí máy chủ truyền thống và chất lượng máy chủ của họ.

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


## Bắt đầu nhanh với Windows Server VM

[https://cloud.google.com/compute/docs/quickstart-windows](https://cloud.google.com/compute/docs/quickstart-windows)


## Bắt đầu nhanh với  Linux VM

[https://cloud.google.com/compute/docs/quickstart-linux](https://cloud.google.com/compute/docs/quickstart-linux)


## [Transferring files to Linux VMs](https://cloud.google.com/compute/docs/instances/transfer-files)

Transfer from `Linux` or `macOS` To `Linux VMs`
- [Cloud Storage](https://cloud.google.com/compute/docs/instances/transfer-files#gcstransfer)
- [gcloud command-line tool](https://cloud.google.com/compute/docs/instances/transfer-files#transfergcloud)
- [SSH in the browser](https://cloud.google.com/compute/docs/instances/transfer-files#transferbrowser)
- [SCP](https://cloud.google.com/compute/docs/instances/transfer-files#scp)

Transfer from `Windows` To `Linux VMs`
- [Cloud Storage](https://cloud.google.com/compute/docs/instances/transfer-files#gcstransfer)
- [gcloud command-line tool](https://cloud.google.com/compute/docs/instances/transfer-files#transfergcloud)
- [SSH in the browser](https://cloud.google.com/compute/docs/instances/transfer-files#transferbrowser)
- [WinSCP](https://cloud.google.com/compute/docs/instances/transfer-files#winscp)


### Chuyển tệp bằng công cụ dòng lệnh `gcloud`
Công cụ dòng lệnh `gcloud` cung cấp tiện ích truyền tệp `SCP`, tạo cặp khóa `SSH` cho bạn trong lần đầu tiên kết nối. Khóa riêng tư của bạn được lưu trữ trên thiết bị cục bộ của bạn và khóa công khai tương ứng của nó được sao chép vào siêu dữ liệu bản sao của dự án hoặc máy ảo.

Để chuyển tệp bằng SCP, bạn phải có quy tắc tường lửa (firewall rule) trên mạng mà máy ảo của bạn sử dụng cho phép kết nối SSH trên cổng `22`. Bạn có thể xác minh rằng quy tắc tường lửa này tồn tại bằng cách tìm kiếm quy tắc tường lửa cho phép `tcp:22` kết nối trong Google Cloud Console.
<a href="https://console.cloud.google.com/networking/firewalls" target="_blank">Go to Firewall rules</a>

Nếu bạn không có quy tắc tường lửa cho phép kết nối SSH trên cổng `22`, hãy [tạo quy tắc tường lửa](https://cloud.google.com/vpc/docs/using-firewalls#creating_firewall_rules).

Bạn có thể cần cài đặt các công cụ `gcloud` và sử dụng nó để sao chép tập tin và thư mục để VM của bạn bằng cách sử dụng lệnh `scp`.

Ví dụ sau đây sao chép một tệp từ máy trạm của bạn vào thư mục chính của máy ảo.
```bat
gcloud compute scp LOCAL_FILE_PATH VM_NAME:~
```
Thay thế những điều sau:
- `LOCAL_FILE_PATH`: đường dẫn đến tệp trên máy trạm của bạn
- `VM_NAME`: tên máy ảo của bạn

Bạn cũng có thể sao chép các tệp và thư mục từ máy ảo sang máy trạm cục bộ của mình. Ví dụ sau sao chép đệ quy một thư mục từ máy ảo của bạn (nguồn) sang máy trạm cục bộ của bạn (đích).

```bat
gcloud compute scp --recurse VM_NAME:REMOTE_DIR LOCAL_DIR
```


### Chuyển tệp bằng SCP trên máy trạm Linux và macOS

Công cụ dòng lệnh `scp` hoạt động tương tự như lệnh `gcloud compute scp` nhưng yêu cầu bạn quản lý các khóa `SSH` của mình theo cách [thủ công](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys).

Công cụ `scp` sử dụng cùng một tệp chính mà bạn sử dụng để kết nối với các phiên bản của mình bằng SSH tiêu chuẩn.





-----
[Deploy Django on Google Compute Engine with Nginx, Gunicorn and Postgresql (Google Cloud SQL)](https://djangocircle.com/deploy-django-on-google-compute-engine-with-nginx-gunicorn-and-postgresql-google-cloud-sql/)  
[Deploy Django to GCP Compute Engine](https://www.minimalistbeing.com/blog/django-deployment-gcp-compute-engine/)  
[Get started with Bitnami Django on Google Cloud](https://cloud.google.com/community/tutorials/get-started-bitnami-django)  
[Deploy Django to GCP Compute Engine](https://www.minimalistbeing.com/blog/django-deployment-gcp-compute-engine/)  
[Deploy Django app with Python on Google Compute Engine](https://stackoverflow.com/questions/46783781/deploy-django-1-10-app-with-python-3-6-on-google-compute-engine)  

