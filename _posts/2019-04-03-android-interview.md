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

2. `ContentProvider` là gì và nó thường được sử dụng để làm gì?

3. Trong điều kiện nào code mẫu dưới đây có thể làm crash ứng dụng của bạn? Làm thế nào bạn sẽ sửa đổi mã để tránh vấn đề tiềm năng này? Giải thích câu trả lời của bạn.
```java
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType(HTTP.PLAIN_TEXT_TYPE); // "text/plain" MIME type
startActivity(sendIntent);
```

4. Callback cuối cùng trong vòng đời của một activity là `onDestroy()`. Hệ thống gọi phương thức này trong activity của bạn là tín hiệu cuối cùng cho thấy activity của bạn đang bị xóa hoàn toàn khỏi bộ nhớ hệ thống. Thông thường, hệ thống sẽ gọi `onPause()` và `onStop()` trước khi gọi `onDestroy()`. Tuy nhiên, hãy mô tả một kịch bản, trong đó `onPause()` và `onStop()` sẽ không được gọi.

5. Đoạn mã nào dưới đây là cách chính xác để kiểm tra xem có cảm biến La bàn trên hệ thống không? Giải thích câu trả lời của bạn.
Answer 1:

-----
## Gợi ý trả lời

1) Bốn lớp Java liên quan đến việc sử dụng các cảm biến trên nền tảng Android là:
- `Sensor`: Cung cấp các phương pháp để xác định khả năng nào khả dụng cho một cảm biến cụ thể.
- `SensorManager`: Cung cấp các phương pháp để đăng ký lắng nghe sự kiện cảm biến và hiệu chỉnh cảm biến.
- `SensorEvent`: Cung cấp dữ liệu cảm biến thô (raw), bao gồm thông tin liên quan đến độ chính xác.
- `SensorEventListener`: Interfacen định nghĩa phương thức gọi lại (callback) sẽ nhận thông báo sự kiện cảm biến.

Để tìm hiểu thêm về [Sensor](https://developer.android.com/guide/topics/sensors/sensors_overview.html), hãy tham khảo hướng dẫn dành cho nhà phát triển Android.

2) `ContentProvider` là một thành phần để quản lý truy cập dữ liệu. Nó đóng gói dữ liệu và cung cấp các cơ chế để xác định bảo mật dữ liệu. `ContentProvider` là interface chuẩn kết nối dữ liệu trong một quy trình với mã đang chạy trong quy trình khác.

Thông tin thêm về `ContentProvider` có thể được tìm thấy [ở đây](https://developer.android.com/guide/topics/providers/content-providers.html) trong Hướng dẫn dành cho nhà phát triển Android.

3) Chỉ định một intent ngầm là một hành động có thể gọi bất kỳ ứng dụng nào trên thiết bị có thể thực hiện hành động. Sử dụng một intent ngầm rất hữu ích khi ứng dụng của bạn không thể thực hiện hành động, nhưng các ứng dụng khác có lẽ có thể. Nếu có nhiều ứng dụng được đăng ký có thể xử lý yêu cầu này, người dùng sẽ được nhắc chọn cái nào sẽ sử dụng.

Tuy nhiên, có thể không có ứng dụng nào có thể xử lý ý định của bạn. Trong trường hợp này, ứng dụng của bạn sẽ gặp crash khi bạn gọi `startActivity ()`. Để tránh điều này, trước khi gọi `startActivity ()` trước tiên bạn nên xác minh rằng có ít nhất một ứng dụng được đăng ký trong hệ thống có thể xử lý ý định đó. Để thực hiện việc này, hãy sử dụng `resolveActivity()` trên đối tượng intent của bạn:

```java
// Verify that there are applications registered to handle this intent
// (resolveActivity returns null if none are registered)
if (sendIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(sendIntent);
}
```

4) `onPause()` và `onStop()` sẽ không được gọi nếu `finish()` được gọi từ bên trong phương thức `onCreate()`. Điều này có thể xảy ra, ví dụ, nếu bạn phát hiện ra lỗi trong khi `onCreate()` và gọi `finish()`. Tuy nhiên, trong trường hợp như vậy, mọi thao tác dọn dẹp mà bạn dự kiến sẽ được thực hiện trong `onPause()` và `onStop()` sẽ không được thực thi.

Mặc dù `onDestroy()` là callback cuối cùng trong vòng đời của một activity, điều đáng nói là callback này có thể không luôn luôn được gọi và không nên dựa vào để giải phóng tài nguyên. Tốt hơn là có các tài nguyên được tạo trong `onStart()` và `onResume()` và giải phóng chúng tương ứng trong `onStop()` và `onPause()`.

Xem hướng dẫn dành cho nhà phát triển Android để biết thêm [thông tin](https://developer.android.com/guide/components/activities/activity-lifecycle) về vòng đời activity.


Tham khảo:
- [20 Essential Android Interview Questions and Answers](https://www.toptal.com/android/interview-questions)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 1)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb)
- [ Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 2)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-2-L4x5xkyglBM)
