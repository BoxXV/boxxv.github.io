---
layout: post
title: Chạy Express (Node.js) dưới dạng dịch vụ trên Windows
subtitle: Run Express (Node.js) as a service on Windows
image: "img/home-bg.jpg"
tags:
- Node
- Express
- service
---

`Express` là khung ứng dụng web Node.js tối giản và linh hoạt, cung cấp một bộ tính năng mạnh mẽ cho các ứng dụng web và thiết bị di động. API.

Thông thường, chúng tôi triển khai các dịch vụ web của mình trên máy chủ linux, nhưng đôi khi chúng tôi cần triển khai Express trên máy tính Windows để thử nghiệm hoặc sản xuất.

Trong bài viết này tôi sẽ nói về một cách đơn giản để chạy máy chủ tốc hành của chúng tôi như một dịch vụ Windows.

Để làm được điều này, trước tiên chúng ta cần chuyển đổi ứng dụng express thành một tệp thực thi duy nhất bằng cách sử dụng [pkg](https://www.npmjs.com/package/pkg) và sau đó sử dụng [nssm](https://nssm.cc) Non-Sucking Service Manager, chúng ta sẽ chạy tệp thực thi dưới dạng dịch vụ

## Chạy một ví dụ đơn giản

Tôi đã sử dụng windows 10 (x64) để chạy ví dụ này nhưng bạn có thể sử dụng bất kỳ phiên bản windows x64 nào khác.

Tạo ứng dụng [express](https://expressjs.com) đơn giản của chúng tôi. `express` là một khung công tác nút js nên chúng tôi cần cài đặt nút js trên máy tính Windows của mình, chúng tôi có thể tải xuống nút js từ trang web chính thức của họ.

Sau đó mở `cmd` trong thư mục bạn muốn đặt ứng dụng của mình và chạy

```bat
mkdir express-app
cd express-app
```

Cài đặt express trong thư mục này

```bat
npm install --save express
```

Tạo tệp app.js:

```javascript
const express = require('express')
const app = express()
const port = 3000
app.get('/', (req, res) => {
res.send('Hello From Windows Service !!')
})
app.listen(port, () => {
console.log(`App is running http://localhost:${port}`)
})
```

Kiểm tra ứng dụng của bạn bằng cách chạy lệnh này trong cmd trong cùng thư mục

```bat
node app.js
App is running http://localhost:3000
```

## Bước 2

Bây giờ chúng tôi sẽ chuyển đổi mã của mình thành một tệp thực thi duy nhất bằng cách sử dụng pkg

Chúng ta cần cài đặt [pkg](https://github.com/vercel/pkg) trên toàn cầu bằng cách sử dụng

```bat
npm install -g pkg
```

Sau đó chúng ta cần chạy cmd trong thư mục ứng dụng để chạy

```bat
pkg app.js -t  node10-win-x64
```

Và sau đó chúng ta sẽ tìm thấy một tập tin thực thi: `app.exe `

Tệp này cho phép chúng tôi chạy trực tiếp ứng dụng express của mình trên bất kỳ máy tính Windows (x64) nào mà không cần cài đặt node.js và mã nguồn của chúng tôi bị ẩn.

## Bước 3

Chuyển đổi tệp exe của chúng tôi thành dịch vụ windows bằng cách sử dụng `nssm`.

nssm là trình quản lý dịch vụ, bạn có thể tải xuống từ [liên kết](http://nssm.cc/download) này. sau đó giải nén nó vào win64 và chạy cmd với tư cách quản trị viên trong thư mục và chạy

```bat
nssm install
```

![nssm](https://boxxv.github.io/img/2024/1_Ct9u8nR236MhSk8UpIurSA.webp "nssm")

Trong Đường dẫn bạn sẽ đặt đường dẫn của app.exe của chúng tôi

Trong tên dịch vụ, bạn sẽ đặt tên dịch vụ mà bạn sẽ thấy trong các dịch vụ windows.

Sau đó bắt đầu dịch vụ của bạn:

```bat
nssm start app-service
```

Dịch vụ sẽ tự động khởi động sau khi khởi động lại.

Bạn cũng có thể xóa và dừng dịch vụ:

```bat
nssm stop app-service
nssm remove app-service
```

Và bạn có thể thấy dịch vụ từ Task manager trong tab services.

Cảm ơn bạn đã đọc bài viết này của tôi, hy vọng rằng nó sẽ hữu ích và giúp bạn hiểu rõ hơn để lựa chọn tốt nhất trong công việc của mình.

-----
- [Run Express (Node.js) as a service on Windows](https://medium.com/@yazanuneisi/run-express-node-js-as-a-service-on-windows-5356cdab66ac)
- [Express/Node introduction](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction)
- [How to broadcast your Nodejs server across your LAN](https://medium.com/@ashaymurceilago/how-to-broadcast-your-nodejs-server-across-your-lan-2ae93af01626)
- []()