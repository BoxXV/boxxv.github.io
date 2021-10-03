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

> ⚠️ Cảnh báo: đây là bài viết cũ, có thể bao gồm thông tin đã lỗi thời. ⚠️


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

Và một ví dụ phức tạp hơn một chút với nhiều phụ thuộc và nhiều phương thức được tiếp xúc:

{% highlight js %}
// filename: foo.js
define(["jquery", "underscore"], function ($, _) {
	// methods
	function a() {}		// private because it's not returned (see below)
	function b() {}		// public because it's returned
	function c() {}		// public because it's returned

	// exposed public methods
	return {
		b: b,
		c: c,
	};
});
{% endhighlight %}




-----
Tham khảo:
- [What is AMD, CommonJS, and UMD?](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
- [Cách viết JavaScript hiện đại: Phần 2: CommonJS module](https://viblo.asia/p/cach-viet-javascript-hien-dai-phan-2-commonjs-module-5WQvzgeXRk3E)
- [JavaScript modules](https://viblo.asia/p/javascript-modules-3P0lPEMn5ox)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Tìm hiểu về module system, CommonJS và require](https://viblo.asia/p/tim-hieu-ve-module-system-commonjs-va-require-QpmleL3mZrd)

