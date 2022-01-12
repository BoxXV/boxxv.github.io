---
layout: post
title: Cho phép IP máy chủ chuyên dụng trên Google Cloud
subtitle: Allowlisting dedicated server IP on Google Cloud

tags:
- GCE
- Google Compute Engine
- Google Cloud
---

Bài viết này mô tả quy trình bạn sẽ cần làm theo để cho phép (danh sách trắng) địa chỉ IP của cổng riêng của bạn trên Google Cloud Platform. Điều này sẽ cho phép bạn hạn chế quyền truy cập vào một VPC cụ thể (Đám mây riêng ảo) - chỉ dành cho những người dùng được kết nối với máy chủ chuyên dụng của bạn.

Đảm bảo địa chỉ IP và điểm cuối của bạn được thiết lập chính xác sẽ giúp bạn yên tâm hơn nhiều về các lớp bảo mật của mình.

## Cấu hình Firewall Rule trong Google Cloud Platform

#### 1. Mở bảng điều khiển GCP console
#### 2. Trong thanh công cụ bên trái, chọn `VPC network` , sau đó chọn `Firewall`
![Dedicated server IP on Google](https://boxxv.github.io/img/gcp/01 Dedicated server IP on Google.png "Dedicated server IP on Google")

#### 3. Chọn `Create Firewall Rule` và điền vào các thông tin sau:

**Name**: Chọn một tên mà bạn lựa chọn  
**Description**: Để cho các quản trị viên khác biết quy tắc này dùng để làm gì (tùy chọn)  
**Logs**: Bạn có thể chọn ghi lưu lượng truy cập liên quan đến quy tắc (điều này có thể dẫn đến chi phí bổ sung từ phía Google)  
**Network**: Chọn mạng có chứa các tài nguyên mà bạn muốn cho phép danh sách  
**Priority**: Sự ưu tiên thì để giá trị mặc định  
**Direction of traffic**: `Ingress`  
**Action on match**: `Allow`  
**Targets**: Tùy thuộc vào nhu cầu của bạn, chọn toàn bộ mạng ( Tất cả các phiên bản trong mạng ) hoặc chọn tài nguyên được gắn nhãn bằng một thẻ nhất định ( Thẻ mục tiêu được chỉ định )  
**Source filter**: Dải IP  
**Source IP ranges**: Dán địa chỉ IP của cổng riêng của bạn  
**Second source filter**: Bộ lọc nguồn thứ hai chọn `None`  
**Protocols and ports**: `Allow all`

![Dedicated server IP on Google](https://boxxv.github.io/img/gcp/02 Dedicated server IP on Google.png "Dedicated server IP on Google")
![Dedicated server IP on Google](https://boxxv.github.io/img/gcp/03 Dedicated server IP on Google.png "Dedicated server IP on Google")

#### 4. Chọn `Create`


Và đó là tất cả! Bây giờ, bạn đã tạo thành công danh sách cho phép IP đầu tiên của mình trong Google Cloud Platform.


-----
Tham khảo:
- [Allowlisting dedicated server IP on Google Cloud](https://help.nordlayer.com/hc/en-us/articles/360019722838-Allowlisting-dedicated-server-IP-on-Google-Cloud)