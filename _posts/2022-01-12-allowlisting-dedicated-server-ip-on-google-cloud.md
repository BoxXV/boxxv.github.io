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

1. Mở bảng điều khiển GCP console
2. Trong thanh công cụ bên trái, chọn `VPC network` , sau đó chọn `Firewall`



-----
Tham khảo:
- [Allowlisting dedicated server IP on Google Cloud](https://help.nordlayer.com/hc/en-us/articles/360019722838-Allowlisting-dedicated-server-IP-on-Google-Cloud)