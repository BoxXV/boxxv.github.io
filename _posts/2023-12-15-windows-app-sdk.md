---
layout: post
title: Giới thiệu về Windows App SDK
subtitle: Introducing the Windows App SDK
description: Windows App SDK có gì đáng chú ý?
tags:
- Windows App SDK
---

# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
- [Windows App SDK 1.2](#windows-app-sdk-12)
- [Tổng kết](#tổng-kết)

# Giới thiệu

Windows SDK, mà thay vào đó chỉ cung cấp một bộ công cụ thống nhất gồm các API có thể được sử dụng như “đòn bẩy” để bổ sung cho ứng dụng hiện có của bạn. Microsoft vừa chính thức phát hành phiên bản 1.2 của Windows App SDK với hàng loạt tính năng mới đáng chú ý. Hãy cùng Nhuttran theo dõi bài viết Windows App SDK 1.2 hiện đã khả dụng, có gì đáng chú ý? biết thêm nhiều thông tin thú vị hơn.

# Windows App SDK 1.2

Windows App SDK 1.2 điểm nổi bật của bản phát hành này có lẽ là tính năng cho phép các nhà phát triển bên thứ ba tạo Widget cho ứng dụng Win32 trong các bản dựng preview Windows 11 Insider và test cục bộ. Đây là điều mà Microsoft đã lên kế hoạch từ lâu, nhưng phải bây giờ mới được triển khai. Các nhà phát triển quan tâm có thể tham khảo tài liệu hướng dẫn của Microsoft để biết thêm thông tin chi tiết.

Windows App SDK 1.2 cho phép nhà phát triển khai thác các chức năng điều khiển phát phương tiện (media playback) mới nhất của WinUI 3. Họ cũng có thể tận dụng dịch vụ Azure Communication Services của Microsoft trên đám mây để bổ sung thêm khả năng gọi thoại và video vào ứng dụng của mình. Đây là công nghệ tương tự hiện đang được Microsoft Teams sử dụng.

Một số thay đổi đáng chú ý khác cần phải kể tới trong Windows App SDK 1.2

Windows App SDK 1.2 HDR và ​​Auto Color Management (ACM) hiện cũng được hỗ trợ thông qua lớp DisplayInformation của Windows App SDK. Nó cho phép các ứng dụng khách theo dõi mọi thay đổi liên quan đến chế độ xem cũng như giao diện một cách tương đối dễ dàng. Và nếu bạn đang sử dụng Visual Studio 17.3 Preview 2 trở lên, sẽ có thêm một mục thú vị khác là khả năng phát triển nguyên bản cho kiến ​​trúc Arm64.

Một số thay đổi đáng chú ý khác cần phải kể tới trong Windows App SDK 1.2 bao gồm việc ứng dụng .NET, Dynamic Refresh Rate(DRR) trong Windows 11 và thành phần AppNotificationBuilder để dễ dàng tạo và xác định thông báo đều đã được tinh giản. Microsoft cũng nhấn mạnh rằng binary footprint x64 của Windows App SDK 1.2 hiện đã nhỏ hơn 11% so với phiên bản cũ 1.1.5

# Tổng kết

Microsoft hiện đang tích cực làm việc với các đối tác phát triển để chuyển ứng dụng của họ sang WinUI 3 và Windows App SDK. Đây là điều mà công ty đã làm ngay từ năm ngoái khi khuyến khích các nhà phát triển chuyển từ Universal Windows Platform (UWP) sang Windows App SDK.


-----
Tham khảo
- [Windows App SDK 1.2 hiện đã khả dụng, có gì đáng chú ý?](https://nhuttran.vn/tin-tuc-su-kien/windows-app-sdk-12-hien-da-kha-dung-co-gi-dang-chu-y)
- []()
