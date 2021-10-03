---
layout: post
title: AMD, CommonJS và UMD là gì? 
subtitle: What is AMD, CommonJS, and UMD?
image: "img/js.jpg"
tags:
- AMD
- CommonJS
- UMD
- npm
- JavaScript
- library
- module
---

> ⚠️ Cảnh báo: đây là một bài viết cũ và có thể bao gồm thông tin đã lỗi thời. ⚠️


## Giới thiệu

Trong những năm qua, có một hệ sinh thái ngày càng tăng đều đặn của các thành phần JavaScript để bạn lựa chọn. Số lượng sự lựa chọn tuyệt đối là tuyệt vời, nhưng điều này cũng gây khó khăn khi các thành phần được trộn và kết hợp với nhau. Và không mất quá nhiều thời gian để các nhà phát triển chớm nở phát hiện ra rằng không phải tất cả các thành phần đều được xây dựng để chơi tốt với nhau.

Để giải quyết những vấn đề này, `AMD` và `CommonJS` có thông số kỹ thuật mô-đun cạnh tranh đã xuất hiện tại hiện trường, cho phép các nhà phát triển viết mã của họ theo cách mô-đun hóa và hộp cát đã thỏa thuận, để không “gây ô nhiễm hệ sinh thái”.

## AMD

`Asynchronous Module Definition` (AMD) Định nghĩa mô-đun không đồng bộ đã đạt được sức hút trên giao diện người dùng, với RequestJS là cách triển khai phổ biến nhất.

Đây là mô-đun `foo` với một phụ thuộc duy nhất vào `jquery`:

{% highlight js %}
// filename: foo.js
define(["jquery"], function ($) {
	// methods
	function myFunc() {}

	// exposed public methods
	return myFunc;
});
{% endhighlight %}


-----
Tham khảo:
- [What is AMD, CommonJS, and UMD? ](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
