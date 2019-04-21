---
layout: post
title: 22+ Câu hỏi phỏng vấn Android và gợi ý trả lời
subtitle: Vì một tương lai lương Android cao hơn iOS
date: "2019-04-03"
tags:
- Android
- Interview
- Questions
- Answers
modified: 2019-04-21
---

1. Có bốn lớp Java liên quan đến việc sử dụng cảm biến trên nền tảng Android. Liệt kê và giải thích mục đích của mỗi lớp.

2. ContentProvider là gì và nó thường được sử dụng để làm gì?

3. Under what condition could the code sample below crash your application? How would you modify the code to avoid this potential problem? Explain your answer.

3. Trong điều kiện nào code mẫu dưới đây có thể làm crash ứng dụng của bạn? Làm thế nào bạn sẽ sửa đổi mã để tránh vấn đề tiềm năng này? Giải thich câu trả lời của bạn.
```java
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType(HTTP.PLAIN_TEXT_TYPE); // "text/plain" MIME type
startActivity(sendIntent);
```

## Gợi ý trả lời

1. Bốn lớp Java liên quan đến việc sử dụng các cảm biến trên nền tảng Android là:
- Sensor: Cung cấp các phương pháp để xác định khả năng nào khả dụng cho một cảm biến cụ thể.
- SensorManager: Cung cấp các phương pháp để đăng ký lắng nghe sự kiện cảm biến và hiệu chỉnh cảm biến.
- SensorEvent: Cung cấp dữ liệu cảm biến thô (raw), bao gồm thông tin liên quan đến độ chính xác.
- SensorEventListener: Interfacen định nghĩa phương thức gọi lại (callback) sẽ nhận thông báo sự kiện cảm biến.

Để tìm hiểu thêm về [Sensor](https://developer.android.com/guide/topics/sensors/sensors_overview.html), hãy tham khảo hướng dẫn dành cho nhà phát triển Android.

2. ContentProvider là một thành phần để quản lý truy cập dữ liệu. Nó đóng gói dữ liệu và cung cấp các cơ chế để xác định bảo mật dữ liệu. ContentProvider là interface chuẩn kết nối dữ liệu trong một quy trình với mã đang chạy trong quy trình khác.

Thông tin thêm về các nhà ContentProvider có thể được tìm thấy [ở đây](https://developer.android.com/guide/topics/providers/content-providers.html) trong Hướng dẫn dành cho nhà phát triển Android.

Tham khảo:
- [20 Essential Android Interview Questions and Answers](https://www.toptal.com/android/interview-questions)