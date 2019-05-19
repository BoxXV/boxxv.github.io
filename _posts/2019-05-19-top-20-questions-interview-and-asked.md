---
layout: post
title: Top 20 câu hỏi phỏng vấn thường gặp & câu trả lời hoàn hảo (Mọi ngành)
subtitle: Vì một tương lai rạng ngời
date: "2019-05-19"
tags:
- Interview
- Questions
- Answers
- Perfect
modified: 2019-05-20
---

1) Có bốn lớp Java liên quan đến việc sử dụng cảm biến trên nền tảng Android. Liệt kê và giải thích mục đích của mỗi lớp.

2) `ContentProvider` là gì và nó thường được sử dụng để làm gì?

3) Trong điều kiện nào code mẫu dưới đây có thể làm crash ứng dụng của bạn? Làm thế nào bạn sẽ sửa đổi mã để tránh vấn đề tiềm năng này? Giải thích câu trả lời của bạn.
```java
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType(HTTP.PLAIN_TEXT_TYPE); // "text/plain" MIME type
startActivity(sendIntent);
```

4) Callback cuối cùng trong vòng đời của một activity là `onDestroy()`. Hệ thống gọi phương thức này trong activity của bạn là tín hiệu cuối cùng cho thấy activity của bạn đang bị xóa hoàn toàn khỏi bộ nhớ hệ thống. Thông thường, hệ thống sẽ gọi `onPause()` và `onStop()` trước khi gọi `onDestroy()`. Tuy nhiên, hãy mô tả một kịch bản, trong đó `onPause()` và `onStop()` sẽ không được gọi.

5) Đoạn mã nào dưới đây là cách chính xác để kiểm tra xem có cảm biến La bàn trên hệ thống không? Giải thích câu trả lời của bạn.

<ins>Câu trả lời 1:</ins>
```java
PackageManager m = getPackageManager();
if (!m.hasSystemFeature(PackageManager.FEATURE_SENSOR_COMPASS)) {
    // This device does not have a compass, turn off the compass feature
}
```

<ins>Câu trả lời 2:</ins>
```java
SensorManager m = getSensorManager();
if (!m.hasSystemFeature(SensorManager.FEATURE_SENSOR_COMPASS)) {
    // This device does not have a compass, turn off the compass feature
}
```

<ins>Câu trả lời 3:</ins>
```java
Sensor s = getSensor();
if (!s.hasSystemFeature(Sensor.FEATURE_SENSOR_COMPASS)) {
    // This device does not have a compass, turn off the compass feature
}
```

6) Mô tả ba trường hợp sử dụng phổ biến để sử dụng một `Intent`.

7) Giả sử rằng bạn đang bắt đầu một service trong Activity như sau:
```java
Intent service = new Intent(context, MyService.class);
startService(service);
```
nơi `MyService` truy cập là máy chủ từ xa thông qua kết nối Internet.

Nếu Activity đang hiển thị một hình động cho biết một số loại tiến bộ, bạn có thể gặp phải vấn đề gì và làm thế nào bạn có thể giải quyết nó?

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

5) Câu trả lời đúng là Câu trả lời số 1, sử dụng PackageManager.

`SensorManager` và `Sensor` là một phần của Android Sensor Framework và được sử dụng để truy cập trực tiếp và thu thập dữ liệu cảm biến thô. Các lớp này không cung cấp bất kỳ phương thức nào như `hasSystemFeature()` được sử dụng để đánh giá các khả năng của hệ thống.

Android định nghĩa tính năng IDs, dưới dạng ENUM, cho bất kỳ tính năng phần cứng hoặc phần mềm nào có thể có trên thiết bị. Chẳng hạn, tính năng ID cho cảm biến la bàn là `FEATURE_SENSOR_COMPASS`.

Nếu ứng dụng của bạn không thể hoạt động mà không có tính năng cụ thể có sẵn trên hệ thống, bạn có thể ngăn người dùng cài đặt ứng dụng của bạn với phần tử `<used-Feature>` trong tệp manifest của ứng dụng của bạn để chỉ định một phụ thuộc không thể thương lượng.

Tuy nhiên, nếu bạn chỉ muốn vô hiệu hóa các thành phần cụ thể của ứng dụng của mình khi thiếu một tính năng, bạn có thể sử dụng lớp `PackageManager`. `PackageManager` được sử dụng để truy xuất các loại thông tin khác nhau liên quan đến các gói ứng dụng hiện đang được cài đặt trên thiết bị.

Để tìm hiểu thêm về [khả năng tương thích và xử lý các loại thiết bị](https://developer.android.com/guide/practices/compatibility.html) hoặc [cảm biến](https://developer.android.com/guide/topics/sensors/sensors_overview.html) khác nhau, vui lòng tham khảo hướng dẫn dành cho nhà phát triển Android.

6) Các trường hợp sử dụng phổ biến để sử dụng `Intent` bao gồm:

- Để bắt đầu một activity: Bạn có thể bắt đầu một phiên bản mới của một Activity bằng cách chuyển một phương thức Intent sang `startActivity()`.
- Để bắt đầu một service: Bạn có thể bắt đầu một service để thực hiện thao tác một lần (chẳng hạn như tải xuống một tệp) bằng cách chuyển một `Intent` đến `startService()`.
- Để truyền broadcast: Bạn có thể truyền broadcast các ứng dụng khác bằng cách chuyển `Intent` đến `sendBroadcast()`, `sendOrderedBroadcast()` hoặc `sendStickyBroadcast()`.

7) Phản hồi từ dịch vụ từ xa qua Internet thường có thể mất một chút thời gian, do độ trễ của mạng hoặc tải trên máy chủ từ xa hoặc thời gian cần thiết để dịch vụ từ xa xử lý và đáp ứng yêu cầu.

Kết quả là, nếu sự chậm trễ như vậy xảy ra, hình ảnh động trong hoạt động (và thậm chí tệ hơn, toàn bộ luồng UI) có thể bị chặn và có thể xuất hiện để người dùng bị đông lạnh trong khi khách hàng chờ phản hồi từ dịch vụ. Điều này là do dịch vụ được bắt đầu trên luồng ứng dụng chính (hoặc luồng UI) trong Hoạt động.

Vấn đề có thể (và nên) tránh được bằng cách đưa bất kỳ yêu cầu từ xa nào vào luồng nền hoặc khi khả thi, sử dụng cơ chế phản hồi không đồng bộ.

Lưu ý rõ: Truy cập mạng từ luồng UI sẽ ném ngoại lệ thời gian chạy trong các phiên bản Android mới hơn khiến ứng dụng bị sập.




Thông tin thêm về [Intent](https://developer.android.com/guide/components/intents-filters.html) có thể được tìm thấy trong hướng dẫn của nhà phát triển Android.


Tham khảo:
- [20 Essential Android Interview Questions and Answers](https://www.toptal.com/android/interview-questions)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 1)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 2)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-2-L4x5xkyglBM)
- [Top 22 câu hỏi thường gặp khi phỏng vấn xin việc (Mọi ngành)](https://timviec365.vn/cau-hoi-tuyen-dung)
