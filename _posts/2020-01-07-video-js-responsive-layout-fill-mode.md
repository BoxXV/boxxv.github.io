---
layout: post
title: Responsive Layout and Fill Mode on Video.js
---

> Video.js release v7.3.0 brings a long wanted feature: Responsive Layout. In addition, Fill Mode has been promoted to a first-class feature

Phát hành Video.js v7.3.0 mang đến một tính năng mong muốn từ lâu: Giao diện đáp ứng. Ngoài ra, Chế độ điền đã được thăng cấp lên tính năng hạng nhất

### Responsive Mode

Chế độ Responsive sẽ giúp người chơi điều chỉnh các thành phần UI theo kích thước của trình phát. Nó sử dụng sự kiện playerresize đã được thêm vào v6.7.0 của Video.js, cho phép chúng tôi biết khi nào trình phát thay đổi kích thước.

Chế độ Responsive sẽ thiết lập và thay đổi các lớp điểm dừng nhất định như `vjs-layout-small` khi kích thước trình phát thay đổi. Đây có thể được cấu hình. Tùy thuộc vào lớp nào hiện đang có trên trình phát, thanh điều khiển và các thành phần UI khác có thể thích ứng.
Ví dụ: với `vjs-layout-small`, các điều khiển thời gian sẽ không hiển thị vì các công cụ thời gian trên thanh tiến trình có sẵn và nút chú thích quan trọng hơn. Ở kích thước lớn hơn, cả hai có thể được hiển thị mà không có vấn đề.

Bạn có thể tìm hiểu cách bật `Responsive Mode` và hơn thế nữa trong trang [tài liệu](https://docs.videojs.com/tutorial-layout.html#responsive-mode) của chúng tôi. Ngoài ra còn có một [example playground](https://github.com/videojs/video.js/blob/master/sandbox/responsive.html.example) trong thư mục sandbox trong repo.


### Fill Mode
[Fill Mode](https://docs.videojs.com/tutorial-layout.html#fill-mode) cho phép trình phát Video.js thay đổi kích thước linh hoạt, nhưng vẫn nằm trong giới hạn của vùng chứa chính. Điều này tương tự với [Fluid Mode](https://docs.videojs.com/tutorial-layout.html#fluid-mode), nhưng đôi khi, hộp chứa của bạn đã được đặt đúng kích cỡ.

Fill Mode không phải là một chế độ hoàn toàn mới, lớp `vjs-fill` đã có sẵn trong Video.js khá lâu. Điều này cuối cùng làm cho nó trở thành một tính năng hạng nhất đi cùng với Chế độ Fluid.

{% highlight js %}
> npm start
{% endhighlight %}




-----
Reference
- [Tutorial: layout | Video.js Documentation](https://docs.videojs.com/tutorial-layout.html)
- [Video.js 7.3: Responsive Layout, Fill Mode, createLogger](https://blog.videojs.com/video-js-7-3-responsive-layout-fill-mode-createlogger/)
