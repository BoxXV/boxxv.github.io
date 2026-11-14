---
layout: post
categories: ["DevOps & Hạ tầng"]
title: "Các công cụ thay thế Inno Setup: NSIS, WiX Toolset, InstallForge"
subtitle: "Inno Setup alternatives for commercial Windows installers"
date: 2026-11-14 09:00:00 +0700
tags:
- Inno Setup
- NSIS
- WiX
- InstallForge
- Installer
- .NET
- CI/CD
---

> Bài viết dành cho công ty muốn **thay Inno Setup mà không phải mua Commercial License**: ưu tiên giải pháp miễn phí, mã nguồn mở (hoặc ít nhất miễn phí) và cho phép dùng thương mại. Điều khoản của Inno Setup có thể thay đổi theo phiên bản, nên hãy đọc [trang điều khoản chính thức](https://jrsoftware.org/isorder-terms.php) trước khi quyết định. Điều khoản của các công cụ dưới đây cũng nên được kiểm tra lại trước khi đưa vào quy trình doanh nghiệp.

- [1. NSIS — thay thế Inno Setup tốt nhất](#1-nsis--thay-thế-inno-setup-tốt-nhất)
- [2. WiX Toolset — tốt nhất nếu công ty cần MSI](#2-wix-toolset--tốt-nhất-nếu-công-ty-cần-msi)
- [3. InstallForge — dễ sử dụng](#3-installforge--dễ-sử-dụng)
- [So sánh nhanh](#so-sánh-nhanh)
- [Nên chọn công cụ nào?](#nên-chọn-công-cụ-nào)
- [Chuyển từ Inno Setup sang NSIS](#chuyển-từ-inno-setup-sang-nsis)
- [Project mẫu: C# .NET 8 + NSIS](#project-mẫu-c-net-8--nsis)

## 1. NSIS — thay thế Inno Setup tốt nhất

NSIS (Nullsoft Scriptable Install System) là lựa chọn mình khuyên dùng nhất nếu bạn đã quen với Inno Setup.

- Miễn phí, mã nguồn mở, dùng được cho phần mềm thương mại.
- Tạo installer `.exe`, hỗ trợ silent install / uninstall.
- Tạo shortcut, ghi registry, cài service...
- Chạy bằng dòng lệnh (`makensis.exe`) nên rất hợp CI/CD.
- Nhẹ.
- Nhược điểm: cú pháp script khác Inno Setup, phải học lại một chút.

NSIS được nhiều nguồn xếp vào nhóm alternative miễn phí / mã nguồn mở hàng đầu của Inno Setup ([AlternativeTo](https://alternativeto.net/software/inno-setup/)).

Trang chính thức: [NSIS](https://nsis.sourceforge.io/)

## 2. WiX Toolset — tốt nhất nếu công ty cần MSI

Nếu phần mềm viết bằng C#/.NET và triển khai trong doanh nghiệp, WiX rất đáng cân nhắc.

- Miễn phí, mã nguồn mở, dùng thương mại được.
- Tạo gói `.msi` chuẩn Windows Installer; có thể tạo thêm bootstrapper `.exe`.
- Tích hợp tốt với Visual Studio / MSBuild, hợp CI/CD.
- Nhược điểm: khó học hơn Inno Setup và NSIS, cấu hình (XML) phức tạp hơn.

MSI phù hợp môi trường IT deployment (GPO, SCCM/Intune...) vì các hệ thống này hỗ trợ MSI rất tốt.

Trang chính thức: [WiX Toolset trên GitHub](https://github.com/wixtoolset/wix)

## 3. InstallForge — dễ sử dụng

Nếu muốn **giao diện GUI** để tạo installer mà không phải viết script, InstallForge là lựa chọn khá dễ dùng.

- Miễn phí, chạy trên Windows, có GUI.
- Tạo installer `.exe` với shortcut, registry, uninstaller, hỗ trợ update.
- Nhược điểm: **không phải mã nguồn mở** (proprietary), cần kiểm tra kỹ license hiện tại trước khi dùng trong doanh nghiệp.

Trang chính thức: [InstallForge](https://installforge.net/)

## So sánh nhanh

| Tiêu chí | NSIS | WiX | InstallForge | Inno Setup |
|---|:---:|:---:|:---:|:---:|
| Miễn phí | Có | Có | Có | Xem điều khoản |
| Mã nguồn mở | Có | Có | Không | Không |
| Dùng thương mại | Có | Có | Xem license | Xem điều khoản |
| Installer EXE | Có | Có (bootstrapper) | Có | Có |
| MSI | Không | **Có** | Không | Không |
| GUI | Hạn chế | Hạn chế | **Có** | Có |
| Cách viết | Script NSIS | XML / MSBuild | Giao diện | Pascal Script |
| CI/CD | **Rất tốt** | **Rất tốt** | Tốt | Tốt |
| Dễ chuyển từ Inno Setup | Khá dễ | Trung bình | Khá dễ | — |
| Độ linh hoạt | Rất cao | Rất cao | Trung bình | Rất cao |

## Nên chọn công cụ nào?

Với phần mềm C#/.NET đang dùng Inno Setup trong doanh nghiệp:

1. **NSIS** nếu muốn thay Inno Setup nhưng vẫn giữ mô hình `Setup.exe`.
2. **WiX Toolset** nếu muốn chuyển sang chuẩn **MSI**, phù hợp môi trường IT deployment.
3. **InstallForge** nếu ưu tiên GUI dễ dùng, không muốn học scripting nhiều.

## Chuyển từ Inno Setup sang NSIS

Nếu đang có hàng trăm file `.iss`, NSIS là hướng chuyển đổi dễ hiểu hơn WiX. Lưu ý: **script Inno Setup không chạy trực tiếp trên NSIS**, bạn phải chuyển từng phần sang cú pháp NSIS:

| Inno Setup | Ý nghĩa | Hướng chuyển sang NSIS |
|---|---|---|
| `[Setup]` | Tên app, version, thư mục cài đặt, output | `Name`, `OutFile`, `InstallDir`, `VIProductVersion` |
| `[Files]` | Danh sách file cần copy | `File`, `SetOutPath` |
| `[Dirs]` | Tạo thư mục | `CreateDirectory` |
| `[Icons]` | Shortcut Start Menu / Desktop | `CreateShortcut` |
| `[Registry]` | Ghi registry | `WriteRegStr`, `WriteRegDWORD` |
| `[Run]` | Chạy chương trình sau khi cài | `Exec`, `ExecWait`, hoặc trang Finish |
| `[UninstallRun]` | Chạy khi gỡ cài đặt | Lệnh trong `Section "Uninstall"` |
| Pascal Script (`[Code]`) | Logic tùy biến | Hàm / macro NSIS, plugin |

## Project mẫu: C# .NET 8 + NSIS

Mô hình: **C# .NET 8 (Console / WinForms / WPF) → `dotnet publish` → NSIS → `Setup.exe`**. `dotnet publish` là cách chính thức để chuẩn bị ứng dụng .NET cho deployment; có thể publish dạng self-contained để máy khách không cần cài .NET Runtime ([Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/core/deploying/)).

Cấu trúc thư mục:

```text
MyApp/
├── MyApp.sln
├── src/
│   └── MyApp/
│       ├── MyApp.csproj
│       └── Program.cs
├── installer/
│   └── MyApp.nsi
├── scripts/
│   ├── build.ps1
│   └── clean.ps1
├── publish/
└── installer-output/
```

Quy trình build:

```text
C# Source
   │
   ▼
dotnet build
   │
   ▼
dotnet publish  (win-x64, self-contained)
   │
   ▼
publish/
   │
   ▼
makensis.exe installer\MyApp.nsi
   │
   ▼
MyApp-1.0.0-Setup.exe
```

NSIS sẽ tạo ra installer có các tính năng:

- Cài vào `Program Files\MyCompany\MyApp`, cho phép chọn `InstallDir`.
- Shortcut Start Menu và Desktop.
- Uninstaller và thông tin gỡ cài đặt trong registry.
- Nâng cấp / cài đè.
- Silent install và silent uninstall.
- Số phiên bản, License / README.

Chỉ cần chạy một lệnh:

```powershell
.\scripts\build.ps1
```

Script sẽ tự động: dọn dẹp → `dotnet restore` → `dotnet publish -c Release -r win-x64 --self-contained true` → `makensis installer\MyApp.nsi` → xuất file `installer-output\MyApp-1.0.0-Setup.exe`.

-----
Tham khảo:
- [Inno Setup – điều khoản và giá](https://jrsoftware.org/isorder-terms.php)
- [AlternativeTo – Inno Setup alternatives](https://alternativeto.net/software/inno-setup/)
- [NSIS](https://nsis.sourceforge.io/)
- [WiX Toolset – GitHub](https://github.com/wixtoolset/wix)
- [InstallForge](https://installforge.net/)
- [.NET application publishing overview – Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/core/deploying/)
