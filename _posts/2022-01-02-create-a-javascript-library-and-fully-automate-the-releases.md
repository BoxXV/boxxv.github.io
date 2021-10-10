---
layout: post
title: Tạo thư viện JavaScript 2021
subtitle: Tự động hóa hoàn toàn các bản phát hành
image: "img/javascript-mastery.png"
tags:
- module
- npm
- JavaScript
- library
---

## 0. Giới thiệu

Trong hướng dẫn này, tôi sẽ chia sẻ kinh nghiệm của mình trong việc tạo thư viện JavaScript UMD có thể được sử dụng ở mọi nơi, thư viện tương thích với hệ sinh thái AMD (Định nghĩa mô-đun không đồng bộ) và CommonJS và cũng có thể được tải trong thẻ <script>.

Để biết thêm thông tin về AMD, CommonJS và UMD, [David Calhoun](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/) đã viết một blog tuyệt vời để so sánh chúng, rất nên đọc.

Được rồi, hãy bắt đầu!


## Tạo một thư viện JavaScript

Chúng tôi sẽ tạo ra một máy tính cầm tay siêu đơn giản :) 

### Tạo một kho lưu trữ (repository) mới

Truy cập [Github](https://github.com) và tạo một dự án mới có tên là `calculator`, khởi tạo kho lưu trữ bằng README, `.gitignore` và chọn giấy phép. 

![repository](https://boxxv.github.io/img/posts/1*iWRF_3Dpj05_K4Pp-iDK8Q.png "repository")

Sao chép kho lưu trữ mới được tạo và nhập vào thư mục: 

{% highlight js %}
git clone git@github.com:<GH_USERNAME>/calculator.git && cd calculator
{% endhighlight %}


### Khởi tạo gói NPM và cài đặt các phụ thuộc Node.js

Chúng tôi sẽ sử dụng `Webpack` để đóng gói thư viện để phân phối và sử dụng `babel` để giúp xử lý cú pháp `ES6` để thư viện của chúng tôi hoạt động trên hầu hết các trình duyệt. 

{% highlight js %}
npm init -y

npm i -D webpack webpack-cli babel-loader @babel/core @babel/preset-env
{% endhighlight %}








-----
Tham khảo:
- [Tạo thư viện JavaScript và tự động hóa hoàn toàn các bản phát hành vào năm 2020 ](https://medium.com/@jeantimex/create-a-javascript-library-and-fully-automate-the-releases-ccce93153dbb)
