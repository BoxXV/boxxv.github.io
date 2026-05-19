---
layout: post
title: Triển khai ứng dụng React trên máy chủ Windows
subtitle: Deploying a React App to a Windows Server
image: "img/2026/gtp1ukda88hjpf3qoski.png"
date: 2026-02-04 10:11:12
tags:
- React
- Node.js
- Windows Server
---

Đây là hướng dẫn đầy đủ để triển khai React app lên Windows Server IIS:

![Node IIS](https://boxxv.github.io/img/2026/Node-IIS.png "Node IIS")

- [Bước 1: Build React app](#bước-1-build-react-app)
- [Bước 2: Cài URL Rewrite Module](#bước-2-cài-url-rewrite-module)
- [Bước 3: Cài URL Rewrite Module](#bước-3-cài-url-rewrite-module)
- [Bước 4: Tạo file web.config](#bước-4-tạo-file-webconfig)
- [Bước 5: Cấu hình IIS](#bước-5-cấu-hình-iis)
- [Bước 6: Kiểm tra](#bước-6-kiểm-tra)
- [7. Xử Lý Sự Cố Thường Gặp](#7-xử-lý-sự-cố-thường-gặp)
- [8. Tối Ưu Hóa (Tùy Chọn)](#8-tối-ưu-hóa-tùy-chọn)
  - [Bật Compression:](#bật-compression)
  - [Thêm HTTPS:](#thêm-https)


![React IIS](https://boxxv.github.io/img/2026/react_iis_deploy_flow.svg "React IIS")

---

### Bước 1: Build React app

```bat
npm install
npm run build
```

Kết quả là thư mục `build/` (CRA) hoặc `dist/` (Vite) chứa các file tĩnh.

### Bước 2: Cài URL Rewrite Module

Chép toàn bộ nội dung thư mục `build/` vào:

```
C:\inetpub\wwwroot\myapp\
```

### Bước 3: Cài URL Rewrite Module

Tải và cài `IIS URL Rewrite 2.1` từ Microsoft tại [https://www.iis.net/downloads/microsoft/url-rewrite](https://www.iis.net/downloads/microsoft/url-rewrite)

Đây là bắt buộc để React Router hoạt động — nếu thiếu, F5 trên bất kỳ route nào sẽ bị lỗi 404.

### Bước 4: Tạo file web.config

Đặt file này trong thư mục `build/` (ngang hàng với index.html)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>

    <rewrite>
      <rules>
        <rule name="React Router" stopProcessing="true">
          <match url=".*" />
          <conditions logicalGrouping="MatchAll">
            <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
            <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
          </conditions>
          <action type="Rewrite" url="/index.html" />
        </rule>
      </rules>
    </rewrite>

    <staticContent>
      <remove fileExtension=".json" />
      <mimeMap fileExtension=".json" mimeType="application/json" />
      <remove fileExtension=".woff2" />
      <mimeMap fileExtension=".woff2" mimeType="font/woff2" />
    </staticContent>

    <httpProtocol>
      <customHeaders>
        <add name="X-Content-Type-Options" value="nosniff" />
        <add name="X-Frame-Options" value="SAMEORIGIN" />
      </customHeaders>
    </httpProtocol>

  </system.webServer>
</configuration>
```

### Bước 5: Cấu hình IIS

Mở **IIS Manager**, sau đó:

1. Chuột phải vào Sites → Add Website
2. Điền các thông tin:
   - Site name: `myapp`
   - Physical path: `C:\inetpub\wwwroot\myapp`
   - Port: `80` (hoặc port tùy chọn)
3. Chọn Application Pool với `.NET CLR version = No Managed Code` (vì đây là app tĩnh)
4. Nhấn **OK**

### Bước 6: Kiểm tra

```
iisreset
```

Sau đó truy cập `http://localhost` hoặc IP server.
Nếu dùng sub-path (ví dụ http://server/myapp), cần thêm `homepage` vào `package.json`:

```json
"homepage": "/myapp"
```

### 7. Xử Lý Sự Cố Thường Gặp

| Vấn Đề | Giải Pháp |
|--------|----------|
| 403 Forbidden | Kiểm tra quyền thư mục, bật "Directory Browsing" hoặc "Default Document" |
| 404 Not Found | Thêm `web.config` với URL Rewrite |
| CORS Error | Cấu hình CORS trong IIS hoặc backend API |
| File tĩnh không tải | Kiểm tra MIME types trong IIS |

### 8. Tối Ưu Hóa (Tùy Chọn)

#### Bật Compression:
1. Vào IIS Manager → Site → Compression
2. Bật "Enable dynamic content compression"

#### Thêm HTTPS:
1. Cài đặt SSL certificate
2. IIS Manager → Site → Bindings → Add HTTPS binding


Với cả ứng dụng React và máy chủ Node.js đang chạy, trang web của bạn đã được triển khai hoàn chỉnh và sẵn sàng sử dụng. Hy vọng bài viết này hữu ích và ngắn gọn.

Happy Coding 💻😄



---
Tham khảo:
- [Deploying a React & Node.js App to a Windows Server](https://medium.com/@tendekai/deploying-a-react-node-js-app-to-a-windows-server-fa6f27b22c5e)
- [Deploying React Apps with Vite: The Complete Guide](https://dev.to/fab_builder/deploying-react-apps-with-vite-the-complete-guide-49j)
- [Enable IIS and Host nodejs application on IIS](https://medium.com/@unlikelycreator/enable-iis-and-host-nodejs-application-on-iis-a27058e1ca79)
- [Chạy Express (Node.js) dưới dạng dịch vụ trên Windows](https://boxxv.github.io/2024/04/17/run-express-node-js-as-a-service-on-windows/)
- [Công cụ giám sát và kiểm tra hiệu suất mã nguồn mở Node.js](https://boxxv.github.io/2023/01/03/node-js-performance-monitoring-tools/)
- [Videos Học Lập Trình NodeJS Căn Bản](https://boxxv.github.io/2020/01/10/nodejs-tutorials-for-beginners/)
- [Triển khai một web site React trên Windows Server IIS](https://claude.ai/share/e2db890f-d0e0-4338-bb42-d4a2ae21ae6b)
- [Triển khai một web site React trên Windows Server IIS](https://github.com/copilot/share/004842a2-0340-88d6-9101-0e4184904015)