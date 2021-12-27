---
layout: post
title: JavaScript All in One
subtitle: Tất cả các kiến thức cần biết về JavaScript
image: "img/js.jpg"
tags:
- Rollup
- AMD
- CommonJS
- UMD
- npm
- JavaScript
- library
- module
---

### A. Module hóa JavaScript

Mặc dù JavaScript không hỗ trợ các module, nhưng cộng đồng các developer đã cố gắng tìm ra cách để làm việc này. Sau một thời gian phát triển, thì hiện nay có một số phương thức module hóa như sau:

- The Module pattern
- [CommonJS](http://www.commonjs.org)
- [Asynchronous Module Definition (AMD)](https://en.wikipedia.org/wiki/Asynchronous_module_definition)


### 1. The Module pattern

Module pattern không yêu cầu bất cứ một công cụ hay thư viện nào, nó có thể hoạt động ở mọi môi trường JavaScript. Có thể bạn đã sử dụng nó rồi mà không hay biết, nhất là khi bạn thường xuyên code CoffeeScript.

Trong JavaScript, module pattern là cách để đóng gói code, nhằm giảm thiểu những xung đột có thể xảy ra khi định nghĩa tên hàm và biến. Nó đơn giản chỉ là code được đặt trong một hàm vô danh được thực thi ngay. Hàm này sẽ trả kết quả là một đối tượng và đối tượng này sẽ được sử dụng như một module. Mọi code JavaScript để tạo ra đối tượng đó hoàn toàn được đóng gói trong hàm vô danh. Hãy xem qua ví dụ sau, bạn sẽ thấy nó rất quen thuộc.


-----
Tham khảo:
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://manhhomienbienthuy.github.io/2016/05/12/su-dung-amd-requirejs-de-module-hoa-javascript.html)





