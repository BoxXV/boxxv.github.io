---
layout: post
title: Giới thiệu về Windows App SDK
subtitle: Introducing the Windows App SDK
description: Windows App SDK có gì đáng chú ý?
author: "TAn, Nhuttran"
tags:
- Windows App SDK
---

# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
  - [Windows App SDK 1.5](#windows-app-sdk-15)
  - [Windows App SDK 1.4](#windows-app-sdk-14)
  - [Windows App SDK 1.3](#windows-app-sdk-13)
  - [Windows App SDK 1.2](#windows-app-sdk-12)
  - [Windows App SDK 1.1](#windows-app-sdk-11)
  - [Windows App SDK 1.0](#windows-app-sdk-10)
- [Cài đặt Windows App SDK](#cài-đặt-windows-app-sdk)
  - [Cài đặt Visual Studio](#cài-đặt-visual-studio)
    - [Workloads và Components cần thiết](#workloads-và-components-cần-thiết)
      - [Để phát triển ứng dụng C# bằng Windows App SDK](#để-phát-triển-ứng-dụng-c-bằng-windows-app-sdk)
      - [Để phát triển ứng dụng C++ bằng Windows App SDK](#để-phát-triển-ứng-dụng-c-bằng-windows-app-sdk-1)
      - [Để phát triển ứng dụng Universal Windows Platform (UWP)](#để-phát-triển-ứng-dụng-universal-windows-platform-uwp)
- [Tổng kết](#tổng-kết)

# Giới thiệu

Windows SDK, mà thay vào đó chỉ cung cấp một bộ công cụ thống nhất gồm các API có thể được sử dụng như “đòn bẩy” để bổ sung cho ứng dụng hiện có của bạn. Microsoft vừa chính thức phát hành phiên bản 1.2 của Windows App SDK với hàng loạt tính năng mới đáng chú ý. Hãy cùng Nhuttran theo dõi bài viết Windows App SDK 1.2 hiện đã khả dụng, có gì đáng chú ý? biết thêm nhiều thông tin thú vị hơn.

![Windows App SDK](https://boxxv.github.io/img/2023/app-sdk.webp "Windows App SDK")

## Windows App SDK 1.5

- Windows App SDK 1.5.3: 05/01/2024
- Windows App SDK 1.5.2: 04/09/2024
- Windows App SDK 1.5.1: 03/12/2024
- Windows App SDK 1.5.0: 02/29/2024

## Windows App SDK 1.4

- Windows App SDK 1.4.5: 02/13/2024
- Windows App SDK 1.4.4: 01/09/2024
- Windows App SDK 1.4.3: 11/16/2023
- Windows App SDK 1.4.2: 10/10/2023
- Windows App SDK 1.4.1: 09/19/2023
- Windows App SDK 1.4.0: 08/29/2023

## Windows App SDK 1.3

- Windows App SDK 1.3.3: 07/25/2023
- Windows App SDK 1.3.2: 06/13/2023
- Windows App SDK 1.3.1: 05/09/2023
- Windows App SDK 1.3.0: 04/12/2023

## Windows App SDK 1.2

- Windows App SDK 1.2.5: 03/15/2023
- Windows App SDK 1.2.4: 02/22/2023
- Windows App SDK 1.2.3: 01/25/2023
- Windows App SDK 1.2.2: 12/14/2022
- Windows App SDK 1.2.0: 11/10/2022

Windows App SDK 1.2 điểm nổi bật của bản phát hành này có lẽ là tính năng cho phép các nhà phát triển bên thứ ba tạo Widget cho ứng dụng Win32 trong các bản dựng preview Windows 11 Insider và test cục bộ. Đây là điều mà Microsoft đã lên kế hoạch từ lâu, nhưng phải bây giờ mới được triển khai. Các nhà phát triển quan tâm có thể tham khảo tài liệu hướng dẫn của Microsoft để biết thêm thông tin chi tiết.

Windows App SDK 1.2 cho phép nhà phát triển khai thác các chức năng điều khiển phát phương tiện (media playback) mới nhất của `WinUI 3`. Họ cũng có thể tận dụng dịch vụ Azure Communication Services của Microsoft trên đám mây để bổ sung thêm khả năng gọi thoại và video vào ứng dụng của mình. Đây là công nghệ tương tự hiện đang được Microsoft Teams sử dụng.

Một số thay đổi đáng chú ý khác cần phải kể tới trong Windows App SDK 1.2

Windows App SDK 1.2 HDR và ​​Auto Color Management (ACM) hiện cũng được hỗ trợ thông qua lớp DisplayInformation của Windows App SDK. Nó cho phép các ứng dụng khách theo dõi mọi thay đổi liên quan đến chế độ xem cũng như giao diện một cách tương đối dễ dàng. Và nếu bạn đang sử dụng Visual Studio 17.3 Preview 2 trở lên, sẽ có thêm một mục thú vị khác là khả năng phát triển nguyên bản cho kiến ​​trúc Arm64.

Một số thay đổi đáng chú ý khác cần phải kể tới trong Windows App SDK 1.2 bao gồm việc ứng dụng .NET, Dynamic Refresh Rate(DRR) trong Windows 11 và thành phần AppNotificationBuilder để dễ dàng tạo và xác định thông báo đều đã được tinh giản. Microsoft cũng nhấn mạnh rằng binary footprint x64 của Windows App SDK 1.2 hiện đã nhỏ hơn 11% so với phiên bản cũ 1.1.5

## Windows App SDK 1.1

- Windows App SDK 1.1.5: 09/14/2022
- Windows App SDK 1.1.4: 08/11/2022
- Windows App SDK 1.1.3: 07/20/2022
- Windows App SDK 1.1.2: 06/28/2022
- Windows App SDK 1.1.1: 06/14/2022
- Windows App SDK 1.1.0: 05/24/2022

## Windows App SDK 1.0

- Windows App SDK 1.0.4: 06/14/2022
- Windows App SDK 1.0.3: 04/18/2022
- Windows App SDK 1.0.2: 04/05/2022
- Windows App SDK 1.0.1: 03/15/2022
- Windows App SDK 1.0.0: 11/16/2021
- Windows App SDK 0.8: 06/24/2021
- Windows App SDK 0.5: 03/29/2021
- Windows App SDK 0.1: 12/11/2020

# Cài đặt Windows App SDK

## Cài đặt Visual Studio

Cài đặt Visual Studio 2022 (được khuyến nghị) hoặc Visual Studio 2019. Bạn có thể chọn giữa Visual Studio Community Edition, Visual Studio Professional hoặc Visual Studio Enterprise miễn phí.

> Quan trọng: Visual Studio 2019 chỉ hỗ trợ Windows App SDK 1.1 trở về trước. Visual Studio 2022 được khuyên dùng để phát triển ứng dụng với tất cả các phiên bản SDK ứng dụng Windows.

### Workloads và Components cần thiết

#### Để phát triển ứng dụng C# bằng Windows App SDK

- .NET Desktop Development
- Windows App SDK C# Templates

![Windows App SDK C# Templates](https://boxxv.github.io/img/2023/winui-desktop-dev-workload.png "Windows App SDK C# Templates")

#### Để phát triển ứng dụng C++ bằng Windows App SDK

- Desktop development with C++
- Windows App SDK C++ Templates

#### Để phát triển ứng dụng Universal Windows Platform (UWP)

- Universal Windows Platform development
- C++ (v143) Universal Windows Platform tools

> Note: Trên tab **Individual components** của hộp thoại cài đặt, trong **SDKs, libraries, and frameworks**, hãy đảm bảo **Windows 10 SDK (10.0.19041.0)** được chọn.


# Tổng kết

Microsoft hiện đang tích cực làm việc với các đối tác phát triển để chuyển ứng dụng của họ sang WinUI 3 và Windows App SDK. Đây là điều mà công ty đã làm ngay từ năm ngoái khi khuyến khích các nhà phát triển chuyển từ Universal Windows Platform (UWP) sang Windows App SDK.


-----
Tham khảo
- [Windows Software Development Kit là gì? Ưu nhược điểm của Windows SDK](https://wiki.tino.org/windows-software-development-kit-la-gi/)
- [Microsoft bỏ hỗ trợ UWP trên Windows 11: Đây là lý do](https://suachualaptop24h.com/tin-cong-nghe-trong-ngay/microsoft-bo-ho-tro-uwp-tren-windows-11-day-la-ly-do-n8008.html)
- [Windows App SDK 1.2 hiện đã khả dụng, có gì đáng chú ý?](https://nhuttran.vn/tin-tuc-su-kien/windows-app-sdk-12-hien-da-kha-dung-co-gi-dang-chu-y)

-----
- [Develop Windows desktop apps](https://learn.microsoft.com/en-us/windows/apps/develop/)
- [Windows App SDK](https://learn.microsoft.com/en-us/windows/apps/windows-app-sdk/)
- [Install tools for the Windows App SDK](https://learn.microsoft.com/en-us/windows/apps/windows-app-sdk/set-up-your-development-environment)
- [Visual Studio project and item templates for Windows apps](https://learn.microsoft.com/en-us/windows/apps/desktop/visual-studio-templates)
- [Tutorial: Create your first Windows App SDK application in Visual Studio with XAML and C#](https://learn.microsoft.com/en-us/visualstudio/get-started/csharp/tutorial-wasdk)
- [Build a Hello World app using C# and WinUI 3 / Windows App SDK](https://learn.microsoft.com/vi-vn/windows/apps/how-tos/hello-world-winui3)

-----
- [Title bar](https://learn.microsoft.com/en-us/windows/apps/design/basics/titlebar-design)
- [Title bar customization](https://learn.microsoft.com/en-us/windows/apps/develop/title-bar)
- [Developing for Windows 11: Like developing for Windows 10, but with rounded corners?](https://www.theregister.com/2021/06/28/developing_for_windows_11/)