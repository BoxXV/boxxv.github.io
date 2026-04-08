---
layout: post
title: Hướng dẫn cấu hình Networking trên VMware ESXi 8.0
subtitle: How to connect a VM to the internet using VMware ESXi
date: 2026-04-06 10:11:12
tags:
- VMware
- ESXi
- Networking
---

- [Các nơi có thể ghi Log - Logging Target Types](#các-nơi-có-thể-ghi-log---logging-target-types)
- [Tổng kết](#tổng-kết)


Bài viết này sẽ hướng dẫn các bạn có thể cấu hình Networking trên ESXi để tiện cho việc quản lý và theo dõi.

![VMware ESXi](https://boxxv.github.io/img/2026/vm.jpg "VMware ESXi")


## Sơ đồ kết nối

![VMware ESXi](https://boxxv.github.io/img/2026/vmware_esxi8_topology_clean.svg "VMware ESXi")

Đây là sơ đồ Networking VMware ESXi 8.0 đầy đủ, bao gồm các thành phần

Từ trong ra ngoài:

- **Windows VM** — Máy ảo với `vNIC` kết nối vào port group `VM Network` (VLAN 0), nhận IP qua DHCP hoặc cấu hình tĩnh.
- **vmk0** — `VMkernel interface` phục vụ `Management Network` (VLAN 0)
- **VM Network** — Port group nằm trong vSwitch0, là nơi các VM kết nối vào. Mỗi ô nhỏ bên trong là một virtual port.
- **vSwitch0** — `Virtual Switch` (switch ảo) trung tâm do ESXi tạo ra, kết nối cả `VM Network` và `Management Network` với `Uplink` vật lý
- **vmnic0** — Driver đại diện cho NIC vật lý đang hoạt động, truyền toàn bộ traffic ra ngoài, đóng vai trò uplink kết nối vào virtual switch.
- **vmnic1** — Driver đại diện cho NIC vật lý dự phòng (chưa dùng), hiển thị dưới dạng đường nét đứt.
- **Physical Network** — Card mạng vật lý (NIC) gắn trên máy chủ, là điểm đầu vào từ mạng bên ngoài.


## 





-----
Tham khảo:
- [How to connect a VM to the internet using VMware ESXi](https://support.us.ovhcloud.com/hc/en-us/articles/360002175944-How-to-connect-a-VM-to-the-internet-using-VMware-ESXi)
- [HOW TO: Install Windows Server 2025 on our ESXi 8.0.3 & Enable PCI Passthrough](https://youtu.be/aellrOQR2c0)
- [Hướng dẫn cấu hình Networking trên ESXi 6.7](https://blog.vinahost.vn/cau-hinh-networking-tren-esxi-6-7/)
- [[ESXi] Cấu hình IP tĩnh (Static IP) và kích hoạt SSH](https://thuanbui.me/esxi-static-ip-ssh/)
- []()
