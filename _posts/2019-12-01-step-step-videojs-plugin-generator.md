---
layout: post
title: Các bước để tạo plugin cho video.js
---

Trong chủ đề này, chúng ta sẽ tìm hiểu cách sử dụng generator-videojs-plugin để tạo và kiểm tra plugin cho video.js.

Trình tạo plugin video.js tạo các tệp và thư mục cần thiết để tạo một plugin thông thường. Nó bao gồm một môi trường thử nghiệm để bạn có thể dễ dàng thấy những thay đổi của mình khi bạn phát triển plugin. Nó thậm chí còn tạo các tệp plugin cuối cùng mà bạn có thể sử dụng khi bạn sẵn sàng phát hành nó.

### Tổng quan

Trong chủ đề này, bạn sẽ thực hiện các tác vụ sau:
- Setup your environment
- Create the plugin foundation
- View the source files
- Test your plugin
- Edit the JavaScript file
- Edit the CSS file
- Build your plugin
- Pass data to your plugin
- Recommendations
- Resources

### I. Thiết lập môi trường

Để thiết lập môi trường của bạn để chạy trình tạo plugin, hãy làm theo các bước sau:

#### 1) Install Node.js - https://nodejs.org
Nếu bạn chưa có nó, hãy tải xuống và cài đặt Node.js JavaScript runtime. Điều này bao gồm npm, là một hệ sinh thái trọn gói bao gồm một bộ sưu tập lớn các thư viện nguồn mở.

Để kiểm tra xem việc cài đạt đã thành công hay chưa, hãy sử dụng các lệnh sau:
{% highlight js %}
> node -v
v10.16.0

> npm -v
6.9.0
{% endhighlight %}

#### 2) Tạo một thư mục cục bộ trên máy tính của bạn.
Trong ví dụ này, chúng tôi sẽ tạo một thư mục có tên là **test**. Đây là nơi tạo ra các tệp và plugin của bạn sẽ sinh ra.

#### 3) Read README
Xem lại thông tin **README** cho [video.js plugin generator.](https://github.com/videojs/generator-videojs-plugin). Trong thư mục **docs**, mở và xem lại các quy ước Plugin video.js. Tài liệu này nói về các quy tắc được đề xuất để tạo plugin của bạn.

#### 4) Open Terminal
Mở ứng dụng Terminal trong thư mục bạn đã tạo ở bước trước. Trong ví dụ này, hãy mở ứng dụng Terminal trong thư mục **test**.

#### 5) Cài đặt plugin generator cùng với Yeoman:
{% highlight js %}
> npm install -g yo generator-videojs-plugin
{% endhighlight %}