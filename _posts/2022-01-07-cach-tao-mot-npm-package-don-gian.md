---
layout: post
title: Cách tạo một NPM package đơn giản
subtitle: Creating a simple npm library to use in and out of the browser

tags:
- JavaScript
- library
- frontend
- roadmap
- module
- tutorial
---

### Nên biết trước khi đọc bài

- Git cơ bản
- Cấu hình `webpack` cơ bản. Đó là nên biết thì giúp bạn đọc hiểu nhanh hơn, còn không thì cũng chả sao, bạn cứ làm theo command trong bài là sẽ tạo NPM package thành công. Mục đích của chúng ta là tạo được một NPM Package mà. 😄

### Tại sao phải tạo NPM package

NPM (Node Package Manager) là một trình quản lý các gói mã nguồn Javascript được cài đặt kèm theo sẵn với NodeJS. Các gói này được gọi là NPM Package. Các NPM package được phát triển bởi các developer, họ publish ra và package của họ được tải lên server của NPM. Sau này muốn dùng tới package đó, bạn chỉ cần cài đặt nhanh chóng với command:

{% highlight js %}
npm install package-name
{% endhighlight %}

Đơn giản như vậy bạn đã cài đặt xong package có tên là **package-name** vào project của mình.

Trong nhiều dự án sử dụng Javascript bạn gặp phải nhiều vấn đề chung. Bạn lên mạng tìm các package đã có trước đó để giải quyết vấn đề. Tuy nhiên, nhiều trường hợp chớ trêu thay, cái package bạn tìm được nó không làm hài lòng bạn: cái thì nặng, cái thì khó dùng, cái thì phải cài thêm jQuery... Mà chính bạn lại có thể tự giải quyết được vấn đề đó theo một cách riêng gọn lẹ của mình. Bạn muốn cách giải quyết đơn giản đấy có thể dễ dàng áp dụng sang các dự án khác. Nên bạn mở lại project cũ để tìm và bê lại code đó sang dự án mới. Bạn thấy phiền hà khó chịu khi phải lục lọi code như thế. Vậy đây là lúc bạn đọc thêm về bài viết này. Bài viết này sẽ hướng dẫn bạn tạo một NPM package, publish và cài đặt thông qua NPM trong vòng một nốt nhạc.

Bài viết này sẽ tạo mẫu một NPM package đơn giản. Có tên là **Simple Scrollspy**, phục vụ cho việc tạo hiệu ứng ScrollSpy thích hợp cho website dạng landing page, hoặc một số khác bạn muốn 😄. Nếu bạn chưa biết ScrollSpy là gì bạn có thể xem qua bức ảnh mẫu dưới đây. Mô tả hiệu ứng ScrollSpy với package của Bootstrap. Đó chính là hiệu ứng ScrollSpy.

![ScrollSpy](https://boxxv.github.io/img/posts/7434635f-7330-4a38-9d66-b395a5611ec3.gif "ScrollSpy")

### Cách tạo NPM package

Package đương nhiên là phải chứa code, vậy đương nhiên bạn phải tạo một thư mục chứa code trên máy tính của bạn để bạn phát triển nó. Mình viết theo chuẩn ES6 nên mình cần một tool để thực hiện compiling mã nguồn. Mình sẽ sử dụng `Webpack`, phiên bản mới nhất hiện tại là Version 4.4.1.

{% highlight js %}
mkdir simple-scrollspy
cd simple-scrollspy
{% endhighlight %}

Bạn đang ở thư mục simple-scrollspy, mình sẽ thực hiện các bước như sau:
- Tạo file package.json mô tả package của bạn với trình quản lý NPM.
- Khởi tạo git repository.
- Tạo file cấu hình cho webpack webpack.config.js.
- Viết code.
- Publish lên server của NPM để có thể cài đặt vào project thông qua NPM.

### Tạo package.json

Tại folder simple-scrollspy, thực hiện:

{% highlight js %}
npm init

# Results:
....

Press ^C at any time to quit.
name: (simple-scrollspy)
{% endhighlight %}






-----
Tham khảo:
- [Cách tạo một NPM package đơn giản](https://viblo.asia/p/cach-tao-mot-npm-package-don-gian-3P0lPy3o5ox)