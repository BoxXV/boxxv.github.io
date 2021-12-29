---
layout: post
title: AMD, CommonJS và UMD là gì? 
subtitle: Sự phát triển của các mẫu mô-đun JavaScript
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

![The Evolution of JavaScript Module Patterns](https://boxxv.github.io/img/posts/javascript-module-patterns.png "The Evolution of JavaScript Module Patterns")

## Giới thiệu

Trong những năm qua, có một hệ sinh thái ngày càng tăng đều đặn của các thành phần JavaScript để bạn lựa chọn. Số lượng sự lựa chọn tuyệt đối là tuyệt vời, nhưng điều này cũng gây khó khăn khi các thành phần được trộn và kết hợp với nhau. Và không mất quá nhiều thời gian để các nhà phát triển chớm nở phát hiện ra rằng không phải tất cả các thành phần đều được xây dựng để chơi tốt với nhau.

Để giải quyết những vấn đề này, `AMD` và `CommonJS` có thông số kỹ thuật mô-đun cạnh tranh đã xuất hiện tại hiện trường, cho phép các nhà phát triển viết mã của họ theo cách mô-đun hóa và hộp cát đã thỏa thuận, để không “gây ô nhiễm hệ sinh thái”.


## IIFE (Immediately-Invoked Function Expression)

Tất cả bắt đầu ở đây, đây là dạng mô-đun lâu đời nhất trong JavaScript.

Biểu thức hàm được gọi ngay lập tức (IIFE) là một hàm ẩn danh được gọi khi nó được khai báo. Nó không thực sự là một mẫu mô-đun, nó là một mẫu bao bọc giúp đóng gói mã và giữ nó cách ly với các phần khác của ứng dụng.

#### TẠO MODULE
{% highlight js %}
// Module
(function(){
    console.info( 'Hi my name is Kevin.' );
})()
{% endhighlight %}

#### SỬ DỤNG PHỤ THUỘC  
Bao gồm “mô-đun” IIFE trong tài liệu HTML của bạn dưới dạng <script>. Đây là mẫu cũ hơn nhưng vẫn được sử dụng cho đến ngày nay.

{% highlight html %}
<script src="module.js"></script>
{% endhighlight %}

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

#### Sử dụng phụ thuộc
{% highlight js %}
require(['module'], function( module ) {
	module.log();
});
{% endhighlight %}


## CommonJS

Mẫu này phát triển từ mẫu AMD dựa trên trình duyệt để sử dụng trong Node.js ở phía máy chủ. Nó sử dụng `module.exports` để xác định các mô-đun và `require('...')` bao gồm chúng như một phần phụ thuộc.

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

#### Sử dụng phụ thuộc

{% highlight js %}
const module = require('./module');
module.log();
{% endhighlight %}


## UMD: Universal Module Definition
Vì phong cách CommonJS và AMD đều phổ biến như nhau, nên có vẻ như vẫn chưa có sự đồng thuận. Điều này đã tạo ra sự thúc đẩy cho một mẫu "phổ quát" hỗ trợ cả hai kiểu, điều này đưa chúng ta đến không gì khác ngoài Định nghĩa Mô-đun Chung.

Mô hình này được thừa nhận là xấu, nhưng cả AMD và CommonJS đều tương thích, cũng như hỗ trợ định nghĩa biến "toàn cầu" kiểu cũ:

{% highlight js %}
(function (root, factory) {
	if (typeof define === "function" && define.amd) {
		// AMD
		define(["jquery"], factory);
	} else if (typeof exports === "object") {
		// Node, CommonJS-like
		module.exports = factory(require("jquery"));
	} else {
		// Browser globals (root is window)
		root.returnExports = factory(root.jQuery);
	}
})(this, function ($) {
	// methods
	function myFunc() {}

	// exposed public method
	return myFunc;
});
{% endhighlight %}

Và giữ nguyên mẫu như các ví dụ trên, trường hợp phức tạp hơn với nhiều phụ thuộc và nhiều phương thức được tiếp xúc:

{% highlight js %}
(function (root, factory) {
	if (typeof define === "function" && define.amd) {
		// AMD
		define(["jquery", "underscore"], factory);
	} else if (typeof exports === "object") {
		// Node, CommonJS-like
		module.exports = factory(require("jquery"), require("underscore"));
	} else {
		// Browser globals (root is window)
		root.returnExports = factory(root.jQuery, root._);
	}
})(this, function ($, _) {
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

#### Sử dụng phụ thuộc  
Có 3 cách để làm việc với mô-đun UMD:

{% highlight js %}
// AMD
require(['module'], function( module ) {
  module.log();
});

// CommonJS
const module = require('./module');
module.log();

// Browser globals
const module = window.module;
module.log();
{% endhighlight %}


## SystemJS & ES6 module’s

Giai đoạn tiếp theo trong quá trình phát triển và mẫu mô-đun trường hợp hiện đại nhất và tốt nhất để sử dụng ngày nay, tính đến năm 2020, được gọi là Hệ thống, System.registerhoặc đơn giản là mô-đun ES6. Điều này làm cho việc sử dụng cú pháp import ... from './module'. Nó được thiết kế để hỗ trợ cú pháp mô-đun ES6 trong môi trường JavaScript ES5. Cú pháp về cơ bản giống với cú pháp của mô-đun ES6, vì vậy tôi đã gộp các ví dụ này lại với nhau ở đây để đơn giản hóa. Mẫu này thường được sử dụng làm tiêu chuẩn vàng trong một ứng dụng được xây dựng bằng TypeScript.

#### Tạo mô-đun
{% highlight js %}
// Module
export default {
	log: function() {
		return console.log( 'Hi my name is Kevin.' );
	}
}
{% endhighlight %}

#### Sử dụng phụ thuộc
{% highlight js %}
import { log } from "./module";
log();
{% endhighlight %}


-----
Tham khảo:
- [What is AMD, CommonJS, and UMD?](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
- [What are CJS, AMD, UMD, and ESM in Javascript?](https://dev.to/iggredible/what-the-heck-are-cjs-amd-umd-and-esm-ikm)
- [The Evolution of JavaScript Module Patterns](https://www.kevinleary.net/javascript-module-patterns-evolution/)
- [Cách viết JavaScript hiện đại: Phần 2: CommonJS module](https://viblo.asia/p/cach-viet-javascript-hien-dai-phan-2-commonjs-module-5WQvzgeXRk3E)
- [JavaScript modules](https://viblo.asia/p/javascript-modules-3P0lPEMn5ox)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://manhhomienbienthuy.github.io/2016/05/12/su-dung-amd-requirejs-de-module-hoa-javascript.html)
- [Tìm hiểu về module system, CommonJS và require](https://viblo.asia/p/tim-hieu-ve-module-system-commonjs-va-require-QpmleL3mZrd)

