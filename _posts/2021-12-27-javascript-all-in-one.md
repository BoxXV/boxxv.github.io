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

```javascript
var loginModule = (function() {
    "use strict";

    var module = {};

    module.myConstant = 1984;

    module.login = function(userNameValue, userPasswordValue) {
        privateLogin(userNameValue, userPasswordValue);
        console.log("login implementation omitted");
    };

    module.logout = function() {
        console.log("logout implementation omitted");
    };

    return module;
})();
```

Module pattern hoạt động tốt với những ứng dụng nhỏ. Nó rất dễ dàng để cài đặt và không cần thư viện nào cả. Tuy nhiên, khi ứng dụng phức tạp hơn, cách làm này không còn phù hợp nữa.

### 2. Asynchronous Module Definition (AMD)

AMD API có những hàm sau:
- `define` để định nghĩa module.
- `require` để load module và các thành phần phụ thuộc.

```javascript
define(
    module_id,
    [dependencies],
    function {}
);

require(["main"], function() {
    console.log("module main is loaded");
});
```

Ưu điểm:
- API rất đơn giản, chi cần 2 hàm require và define.
- Có rất nhiều cách để load khác nhau. Chúng ta sẽ xem xét một ví dụ ở phần sau.
- AMD không khó để debug.
- Khi module hóa ứng dụng, bạn dễ dàng tìm ra phần code nào bị lỗi.
- Performance: các module được load khi cần, do đó ứng dụng khi khởi tạo rất nhẹ nhàng.

Nhược điểm:
- Danh sách thành phần phụ thuộc sẽ rất dài khi ứng dụng trở nên phức tạp.
- Một lỗi bất cẩn của lập trình viên có thể khiến ứng dụng hoạt động sai. Ví dụ sau, việc danh sách các thành phần phụ thuộc và tham số hàm callback không khớp không phải lỗi cú pháp và nó sẽ khiến ứng dụng hoạt động theo cách mà không ai hiểu được.

### 3. [RequireJS](https://requirejs.org)

RequireJS là một file JavaScript và một `module loader`. Nó được tối ưu hóa cho môi trường trình duyệt nhưng cũng có thể sử dụng trong các môi trường JavaScript khác, như Rhino hoặc Node. Sử dụng các module loader như RequireJS sẽ giúp tăng tốc độ và chất lượng code của bạn. 

Tất nhiên, đây là một định nghĩa có hơi hướng quảng cáo. Chúng ta có thể hiểu đơn giản RequireJS là một thư viện cho phép chúng ta module hóa code JavaScript theo quy chuẩn của AMD.



-----
Tham khảo:
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://manhhomienbienthuy.github.io/2016/05/12/su-dung-amd-requirejs-de-module-hoa-javascript.html)





