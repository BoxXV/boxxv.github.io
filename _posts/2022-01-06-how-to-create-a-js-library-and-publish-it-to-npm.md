---
layout: post
title: Build Javascript library và publish lên NPM
subtitle: How to create a JavaScript library and publish it to npm
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

Chào các bạn,

Nói về NPM thì chắc nó quá quen thuộc với chúng ta rồi nhỉ.

NPM là viết tắt của NodeJS Package Manager, là một nơi để ta quản lý toàn bộ về library của chúng ta trên NPM thông qua version cũng như là nơi ta có thể publish các library để chia sẻ cho các developers khác trên thế giới cài và sử dụng dc :D, đại loại là vậy 😀

Và mình đánh tới phần library Javascript chuyên cho web nhé, cụ thể là cài cho project Webpack 😀

Ở chuyên mục này, mình sẽ hướng dẫn cụ thể 2 bước như sau:

- Chuẩn bị library và cấu hình packages
- Publish lên NPM

Trước khi bắt đầu, nếu bạn nào chưa có NodeJS thì lên trang chủ tải về nhé, khi cài NodeJS nó sẽ cài luôn cả NPM, ta chỉ việc next, next,… thui 


## I/ Chuẩn bị Library của bạn

Vì sao ta nên sử dụng `Webpack` để build ra library?

- Vì Webpack hỗ trợ ta package lại toàn bộ dependencies (js, css, img,…) và build ra 1 file bundle JS duy nhất và minified lại nó ở size nhỏ nhất. Và từ file bundle đó, ta có thể đem đi import vào html bình thường hoặc import vào trong project Webpack nào nữa tùy ý :D.
- Không chỉ vậy, ta có thể dùng được syntax `ES6` và Webpack vẫn build ra được full JS `ES5` và có thể sử dụng ở mọi browser (trong đó có IE).

Quá ngon phải ko nào 😀

Với starter Webpack, ta có thể sử dụng template sau để viết library ra cho riêng mình

### 1/ Tạo 1 project Webpack

Chúng ta sẽ sử dụng template này để tạo ra project Webpack nhé: [https://github.com/sethsandaru/webpack-js-library-simple](https://github.com/sethsandaru/webpack-js-library-simple)

Chạy lệnh sau để clone project về

{% highlight js %}
git clone https://github.com/lifenautjoe/webpack-starter-basic PROJECT-NAME

cd PROJECT-NAME
{% endhighlight %}

Sau khi clone về xong, ta vào thư mục project Webpack của bạn, chạy tiếp lệnh:
{% highlight js %}
npm install
{% endhighlight %}

Đợi cho npm cài các dependencies cần thiết đi nhé, mất tầm 2~10p tùy theo mạng của các bạn 😀


### 2/ Bắt đầu viết library

Theo structure của project template, thì tất cả file js, code này nọ ta sẽ để trong thư mục `src` nhé. Và trong thư mục src đó, ta có thể

Ví dụ, mình sẽ viết ra một library để lấy thời gian hiện tại và alert lên màn hình.

**src/utility/DateLibrary.js**
{% highlight js %}
var DateLibrary = {};

DateLibrary.showCurrentTime = function() {
	alert(new Date());
};

export {
	DateLibrary
}
{% endhighlight %}

Các bạn lưu ý, khi ta viết library trong webpack, ta khai báo var này nọ nhưng nó sẽ ko như JS mà ta khai báo ở ngoài browser, internal hết. Vậy nên ta sẽ dùng index để tạo đầu ra cho library của bạn như sau:

**src/index.js**
{% highlight js %}
import {DateLibrary} as './utility/DateLibrary'

window.DateLibrary = DateLibrary;
{% endhighlight %}

Vậy là phần code ta đã chuẩn bị đầy đủ 😀

Lưu ý nhỏ: với Webpack config của project template kia, nó chỉ có thể load được các file .js thôi nhé các bạn :D, để load được thêm css hay các file khác chắc các bạn cần tìm hiểu thêm về Webpack nữa, ở bài viết sau 😀


### 3/ Sửa lại file package.json

File này khá là quan trọng, nó chứa thông tin để npm truy xuất cũng như là các thông tin dependencies, library của bạn,…

Mình sẽ đi từng các property nhé, lưu ý ta cần tuân thủ theo **JSON** file nếu ko sẽ bị lỗi đó.

**`name`**
Là tên của library của bạn, đại loại như “your-library”, “libraryABC”,… Lưu ý là ko có space (khoảng trắng) là được 😀

Tên này sẽ là tên unique, các bạn cần tìm 1 tên đẹp cho tên library nhé 😀

Khi publish lên, ta sẽ truy xuất vào dc url như sau: http://npmjs.com/package/library-cua-ban

`**version**`
Là version stable hiện tại dành cho library của bạn.

`**description**`
Mô tả về library này

`**keywords**`
Là một mảng keyword dành cho library của bạn (như cái tag) hỗ trợ các users có thể tìm ra dc library của bạn 😀

`**author**`
Là người phát triển ra library này, ta có thể nhập như sau:

Mẫu bình thường, chỉ tên bạn: “Phat Tran”

Mẫu có tên và email của bạn: “Phat Tran <phat@gmail.com>”

Mẫu có tên, email và website của bạn: “Phat Tran <phat@gmail.com> (https://sethphat.com)”

Nếu library của bạn có nhiều người phát triển, bạn có thể nhập một mảng người phát triển tùy ý 😀

`**license**`
Là loại license dành cho library của bạn, thường thì mình hay để MIT 😀

`**private**`
Để true nếu đây là một library private, false thì sẽ là public

`**main**`
Là đầu vào library của bạn dành cho các project Webpack khi các developers khác import vào project riêng của họ.

Ta có thể trỏ vào 1 file bundle nhất định hoặc 1 thư mục,… Mà best practice thì ta nên trỏ vào 1 file nhất định 😀

`**repository**`
Property này sẽ chứa thông tin của repo của bạn, trong template project sẽ ko có property này, các bạn tự thêm vào nhé 😀

Mẫu như sau:




-----
Tham khảo:
- [What is AMD, CommonJS, and UMD?](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
- [Cách viết JavaScript hiện đại: Phần 2: CommonJS module](https://viblo.asia/p/cach-viet-javascript-hien-dai-phan-2-commonjs-module-5WQvzgeXRk3E)
- [JavaScript modules](https://viblo.asia/p/javascript-modules-3P0lPEMn5ox)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://manhhomienbienthuy.github.io/2016/05/12/su-dung-amd-requirejs-de-module-hoa-javascript.html)
- [Tìm hiểu về module system, CommonJS và require](https://viblo.asia/p/tim-hieu-ve-module-system-commonjs-va-require-QpmleL3mZrd)

