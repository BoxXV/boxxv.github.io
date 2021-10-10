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





-----
Tham khảo:
- [What is AMD, CommonJS, and UMD?](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
- [Cách viết JavaScript hiện đại: Phần 2: CommonJS module](https://viblo.asia/p/cach-viet-javascript-hien-dai-phan-2-commonjs-module-5WQvzgeXRk3E)
- [JavaScript modules](https://viblo.asia/p/javascript-modules-3P0lPEMn5ox)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://manhhomienbienthuy.github.io/2016/05/12/su-dung-amd-requirejs-de-module-hoa-javascript.html)
- [Tìm hiểu về module system, CommonJS và require](https://viblo.asia/p/tim-hieu-ve-module-system-commonjs-va-require-QpmleL3mZrd)

