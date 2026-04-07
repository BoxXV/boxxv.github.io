---
layout: post
title: Triển khai ứng dụng React & Node.js lên máy chủ Windows
subtitle: Deploying a React & Node.js App to a Windows Server
image: "img/2026/gtp1ukda88hjpf3qoski.png"
date: 2026-02-03 10:11:12
tags:
- React
- Node.js
- Windows Server
---

Tay cầm cốc cà phê gần cạn, tim đập thình thịch vì hồi hộp… vẻ mặt bạn hiện lên vẻ tự mãn (tôi cho rằng hầu hết các lập trình viên đều biết cảm giác này). Bạn nhấp một ngụm cà phê trong khi ngắm nhìn ứng dụng web vừa hoàn thành. Bạn đã dành hàng ngày, hàng tháng, thậm chí hàng năm trời để làm việc với nó, và cuối cùng, nó đã xong rồi 🍾😄.

- [Bước 1: Triển khai ứng dụng máy chủ NodeJs](#bước-1-triển-khai-ứng-dụng-máy-chủ-nodejs)
  - [1. Cài đặt Node.js trên máy chủ Windows](#1-cài-đặt-nodejs-trên-máy-chủ-windows)
  - [2. Cài đặt pm2](#2-cài-đặt-pm2)
  - [3. Khởi động ứng dụng máy chủ của bạn bằng lệnh pm2.](#3-khởi-động-ứng-dụng-máy-chủ-của-bạn-bằng-lệnh-pm2)
- [Bước 2: Triển khai ứng dụng React](#bước-2-triển-khai-ứng-dụng-react)
  - [1. Tạo bản dựng tối ưu hóa ứng dụng của bạn cho môi trường sản xuất bằng cách chạy lệnh sau:](#1-tạo-bản-dựng-tối-ưu-hóa-ứng-dụng-của-bạn-cho-môi-trường-sản-xuất-bằng-cách-chạy-lệnh-sau)
  - [2. Kết quả của lệnh build](#2-kết-quả-của-lệnh-build)
  - [3. Triển khai ứng dụng lên Internet Information Services (IIS)](#3-triển-khai-ứng-dụng-lên-internet-information-services-iis)


Tuy nhiên, vẫn còn một thử thách cuối cùng bạn cần vượt qua để hoàn thành hành trình này: ứng dụng chỉ hoạt động trên máy tính của bạn 😥. Điều khó khăn nhất trong chặng cuối này là yêu cầu triển khai ứng dụng trên máy chủ Windows cục bộ do khách hàng của bạn cung cấp. Mục đích của bài viết này là biến nhiệm vụ khó khăn này thành dễ dàng hơn và hy vọng sẽ tiết kiệm thời gian cho người đọc.

---

### Bước 1: Triển khai ứng dụng máy chủ NodeJs

#### 1. Cài đặt Node.js trên máy chủ Windows

#### 2. Cài đặt pm2

Cài đặt pm2 từ npm trong ứng dụng máy chủ của bạn. PM2 là trình quản lý tiến trình sản xuất cho các ứng dụng Node.js với bộ cân bằng tải tích hợp. Nó cho phép bạn duy trì các ứng dụng hoạt động liên tục, tải lại chúng mà không cần thời gian ngừng hoạt động và hỗ trợ các tác vụ quản trị hệ thống thông thường.

```bat
npm install pm2 -g
```

#### 3. Khởi động ứng dụng máy chủ của bạn bằng lệnh pm2.

```bat
pm2 start server.js
```

Ứng dụng máy chủ của bạn hiện đã được chạy ngầm (ở chế độ nền), được giám sát và duy trì hoạt động liên tục. Trạng thái máy chủ sẽ được hiển thị trong cửa sổ dòng lệnh như hình bên dưới.

![PM2](https://boxxv.github.io/img/2026/1_xyiMeOKVClh1XdzgFZFbtA.webp "PM2")

Giờ bạn có thể nhập địa chỉ máy chủ và cổng vào thanh địa chỉ trình duyệt để truy cập máy chủ. Để thử nghiệm, tôi gửi văn bản đến trình duyệt từ đường dẫn trang chủ của máy chủ bằng đoạn mã sau.

```bat
pm2 start server.js
```

Giờ bạn có thể nhập địa chỉ máy chủ và cổng vào thanh địa chỉ trình duyệt để truy cập máy chủ. Để thử nghiệm, tôi gửi văn bản đến trình duyệt từ đường dẫn trang chủ của máy chủ bằng đoạn mã sau.

```typescript
app.get('/', (req, res) => {
    res.send('Hello World :)');
});
```

Nhập `ip_address`:`port_number` vào thanh địa chỉ URL, ví dụ: `localhost:4000`, sẽ cho ra kết quả sau trong trình duyệt.

![Node](https://boxxv.github.io/img/2026/1_3-aTFA4pw2Bkl92wQOtGdA.webp "Node")

Vậy là xong. Quá trình thiết lập máy chủ đã hoàn tất. Tiếp theo, chúng ta sẽ triển khai ứng dụng React.


### Bước 2: Triển khai ứng dụng React

#### 1. Tạo bản dựng tối ưu hóa ứng dụng của bạn cho môi trường sản xuất bằng cách chạy lệnh sau:

```bat
npm run build
```

#### 2. Kết quả của lệnh build

Kết quả của lệnh build sẽ tạo một thư mục build mới bên trong dự án React App của bạn, chứa bản build dành cho sản xuất. Bạn có thể thấy thư mục build này bên trong ứng dụng của mình trong Solution Explorer của IDE.

![Node](https://boxxv.github.io/img/2026/1_BXxoLwnu3eCBYasLDp7-YQ.webp "Node")

#### 3. Triển khai ứng dụng lên Internet Information Services (IIS)

Triển khai ứng dụng lên Internet Information Services (IIS). Để triển khai ứng dụng lên IIS, trước tiên hãy tạo một Application Pool mới bằng cách nhấp chuột phải vào Application Pool và chọn Add Application Pool.

![Node](https://boxxv.github.io/img/2026/1_m2bUUVO6KyhNwQv89lkjpQ.webp "Node")

Đặt tên cho Nhóm ứng dụng và nhấn OK.

![Node](https://boxxv.github.io/img/2026/1_qszl5_deI8d3WkFWiPcKbA.webp "Node")

Mở Cài đặt nâng cao cho Nhóm ứng dụng và đảm bảo rằng định danh được đặt thành Định danh nhóm ứng dụng.

![Node](https://boxxv.github.io/img/2026/1_qz6_cTWExmnTX_j0hNpc8A.webp "Node")


Nhấp chuột phải vào Sites, sau đó nhấp vào Add Website và điền đầy đủ thông tin cấu hình ứng dụng của bạn như hình bên dưới.

- `Application Pool`: nhóm ứng dụng đã tạo ở bước trước.
- `Physical Path`: địa chỉ thư mục build của ứng dụng React của bạn
- `Port`: cổng của ứng dụng React của bạn

![Node](https://boxxv.github.io/img/2026/1_yFjw6YjzwqLrZMDtdSZL7g.webp "Node")

Nhấp vào OK và truy cập địa chỉ ứng dụng React trong trình duyệt để kiểm tra chức năng.

Với cả ứng dụng React và máy chủ Node.js đang chạy, trang web của bạn đã được triển khai hoàn chỉnh và sẵn sàng sử dụng. Hy vọng bài viết này hữu ích và ngắn gọn.

Happy Coding 💻😄



---
Tham khảo:
- [Deploying a React & Node.js App to a Windows Server](https://medium.com/@tendekai/deploying-a-react-node-js-app-to-a-windows-server-fa6f27b22c5e)
- [Deploying React Apps with Vite: The Complete Guide](https://dev.to/fab_builder/deploying-react-apps-with-vite-the-complete-guide-49j)
- []()
- [Chạy Express (Node.js) dưới dạng dịch vụ trên Windows](https://boxxv.github.io/2024/04/17/run-express-node-js-as-a-service-on-windows/)
- [Công cụ giám sát và kiểm tra hiệu suất mã nguồn mở Node.js](https://boxxv.github.io/2023/01/03/node-js-performance-monitoring-tools/)
- [Videos Học Lập Trình NodeJS Căn Bản](https://boxxv.github.io/2020/01/10/nodejs-tutorials-for-beginners/)
- []()