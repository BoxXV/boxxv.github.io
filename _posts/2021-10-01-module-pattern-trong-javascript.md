---
layout: post
title: Closures, IIFEs, module pattern trong Javascript
subtitle: Module Pattern in Javascript
image: "img/js.jpg"
tags:
- IIFE
- AMD
- CJS
- CommonJS
- UMD
- ESM
- npm
- JavaScript
- library
- module
---

## Các tính chất của Module Pattern

- Dựa trên Closure và HOF (Hight Order Function), IIFE (hàm được chạy ngay lập tức).
- Dùng để khởi tạo một Object giấu dữ liệu không thể truy xuất từ bên ngoài (private data).
- Có thể phát triển thành Revealing Module Pattern.
- Tính đóng gói dữ liệu (Encapsulation).


## Ví dụ về Module Pattern

### IIFE (Immediately Invoked Function Expression)

{% highlight js %}
(function helloModulePattern(name) {
    console.log(`module pattern chào ${name}`) // print console: module pattern chào viblo
})('viblo')
{% endhighlight %}

Câu lệnh trên được gọi là IIFE (Immediately Invoked Function Expression) sẽ được khởi tạo và thực thi ngay lập tức, nó không giống như một function bình thường ở ví dụ bên dưới khi chúng ta gọi nó mới được thực thi cùng xem ví dụ về một function không phải là một IIFE.

{% highlight js %}
function helloFunction(name) {
    console.log(`function chào ${name}`) // print console: function chào viblo
}
helloFunction('viblo')
{% endhighlight %}

Tóm lại:
- Function đầu tiên được khởi tạo và thực thi ngay lập tức.
- Function thứ 2 nếu ta không gọi helloFunction('viblo') thì nó sẽ không được thực thi mà chỉ được khởi tạo.



#### Ví dụ chi tiết về Module Pattern






-----
Tham khảo:
- [Closures, IIFEs, module pattern trong Javascript](https://viblo.asia/p/closures-iifes-module-pattern-trong-javascript-4P856jYG5Y3)
- [Module Pattern trong Javascript](https://viblo.asia/p/module-pattern-trong-javascript-Qpmle1wolrd)
- [What is AMD, CommonJS, and UMD?](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
- [What are CJS, AMD, UMD, and ESM in Javascript?](https://dev.to/iggredible/what-the-heck-are-cjs-amd-umd-and-esm-ikm)
- [The Evolution of JavaScript Module Patterns](https://www.kevinleary.net/javascript-module-patterns-evolution/)
- [ES6 - Từ cơ bản tới nâng cao (Phần 3)](https://viblo.asia/p/es6-tu-co-ban-toi-nang-cao-phan-3-6J3ZgxELlmB)
- [Cách mà Google & Amazon quét sạch hàng ngàn JS developers xấu số chỉ bởi 1 câu interview đơn giản!](https://viblo.asia/p/cach-ma-google-amazon-quet-sach-hang-ngan-js-developers-xau-so-chi-boi-1-cau-interview-don-gian-1VgZveBRKAw)
- [Cách viết JavaScript hiện đại: Phần 2: CommonJS module](https://viblo.asia/p/cach-viet-javascript-hien-dai-phan-2-commonjs-module-5WQvzgeXRk3E)
- [JavaScript modules](https://viblo.asia/p/javascript-modules-3P0lPEMn5ox)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://manhhomienbienthuy.github.io/2016/05/12/su-dung-amd-requirejs-de-module-hoa-javascript.html)
- [Tìm hiểu về module system, CommonJS và require](https://viblo.asia/p/tim-hieu-ve-module-system-commonjs-va-require-QpmleL3mZrd)

