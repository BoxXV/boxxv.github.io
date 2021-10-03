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

Phần đầu tiên của định nghĩa là một mảng các phần phụ thuộc, trong khi phần thứ hai về cơ bản là hàm gọi lại chỉ được thực thi khi các phần phụ thuộc có sẵn (các trình tải tập lệnh như RequestJS đảm nhiệm phần đó, bao gồm cả việc tìm ra vị trí của các tệp) .

Lưu ý rằng sự phụ thuộc vào thứ tự biến là quan trọng (ví dụ: jquery-> $, underscore->_).

Cũng lưu ý rằng chúng ta có thể ánh xạ các phụ thuộc vào bất kỳ biến tùy ý nào mà chúng ta muốn ở đây. Nếu chúng tôi thay đổi $ thành $$ trong đoạn mã trên, tất cả các tham chiếu jQuery trong khối chức năng của chúng tôi sẽ $$ thay vì $.

Và lưu ý, quan trọng nhất, bạn không thể tham chiếu các biến `$` và `_` bên ngoài hàm, vì nó được đóng hộp cát từ mã khác. Đó là mục tiêu ở đây!


## CommonJS
CommonJS là một phong cách bạn có thể quen thuộc nếu bạn viết bất cứ điều gì bằng Node (sử dụng một biến thể nhỏ). Nó cũng đang đạt được sức hút trên giao diện người dùng với Browserify.

Sử dụng định dạng tương tự như trước đây, đây là foomô-đun của chúng tôi trông như thế nào trong CommonJS:

{% highlight js %}
// filename: foo.js

// dependencies
var $ = require("jquery");

// methods
function myFunc() {}

// exposed public method (single)
module.exports = myFunc;
{% endhighlight %}

Và ví dụ phức tạp hơn của chúng tôi, với nhiều phụ thuộc và nhiều phương thức được hiển thị:

{% highlight js %}
// filename: foo.js
var $ = require("jquery");
var _ = require("underscore");

// methods
function a() {}		// private because it's omitted from module.exports (see below)
function b() {}		// public because it's defined in module.exports
function c() {}		// public because it's defined in module.exports

// exposed public methods
module.exports = {
	b: b,
	c: c,
};
{% endhighlight %}





-----
Tham khảo:
- [What is AMD, CommonJS, and UMD?](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
- [Cách viết JavaScript hiện đại: Phần 2: CommonJS module](https://viblo.asia/p/cach-viet-javascript-hien-dai-phan-2-commonjs-module-5WQvzgeXRk3E)
- [JavaScript modules](https://viblo.asia/p/javascript-modules-3P0lPEMn5ox)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://manhhomienbienthuy.github.io/2016/05/12/su-dung-amd-requirejs-de-module-hoa-javascript.html)
- [Tìm hiểu về module system, CommonJS và require](https://viblo.asia/p/tim-hieu-ve-module-system-commonjs-va-require-QpmleL3mZrd)

