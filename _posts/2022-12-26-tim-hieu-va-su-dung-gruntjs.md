---
layout: post
title: Tìm hiểu và sử dụng Grunt JS
subtitle: Building với Grunt
image: "img/projects-bg.jpg"
tags:
- Gulp
- GulpJs
- Grunt
- GruntJs
- Building
---

![Grunt](https://boxxv.github.io/img/2022/grunt.png "Grunt")

## Mục lục

- [Mục lục](#mục-lục)
- [1. Grunt là gì?](#1-grunt-là-gì)
- [2. Cài đặt Grunt](#2-cài-đặt-grunt)
- [3. Thiết lập Grunt chạy 1 tác vụ đơn giản](#3-thiết-lập-grunt-chạy-1-tác-vụ-đơn-giản)
  - [Gruntfile.js](#gruntfilejs)
- [4. Thực hiện nhiều tác vụ](#4-thực-hiện-nhiều-tác-vụ)
- [5. Tác vụ watch](#5-tác-vụ-watch)
- [6. Biên dịch SASS thành CSS](#6-biên-dịch-sass-thành-css)
- [7. Biên dịch Javascript](#7-biên-dịch-javascript)
- [Tổng kết](#tổng-kết)


## 1. Grunt là gì?

Grunt là một công cụ Javascript tự động thi hành các tác vụ, Grunt được viết bằng `Node.js` (Viết bởi Ben Alman từ năm 2012) hiện đang phân phối bằng `npm` của Node.js. Các tác vụ mà Grunt cung cấp rất nhiều (cung cấp thông qua các plugin với trên 6000 plugin, cũng là một module Node.js, xem thêm [Grunt Plugins](https://gruntjs.com/plugins)), nếu danh sách cung cấp không đủ bạn cũng có thể tự xây dựng Task riêng của mình.

Rất nhiều công ty, tổ chức đã sử dụng Grunt như: Adobe Systems, jQuery, Twitter, Mozilla, Bootstrap, Cloudant, Opera, WordPress, Walmart, and Microsoft

Tóm lại, nếu bạn có nhiều tác vụ thực hiện thủ công trên một dự án - với nhiều công cụ khác nhau (Ví dụ kiểm tra xem code có lỗi không, code không lỗi thì biên dịch (ví dụ scss -> css), biên dịch xong thì đổi tên file, nén file ...). Thì với Grunt thì các tác vụ đó được mô tả gắn gọn trong 1 file, sau đó bạn ra lệnh cho `Grunt` tự động thực hiện lần lượt các tác vụ đó giúp bạn.

## 2. Cài đặt Grunt

```bat
npm install -g grunt-cli
hoặc
sudo npm install -g grunt-cli
```

## 3. Thiết lập Grunt chạy 1 tác vụ đơn giản

```no-highlight
|- build/
|- src/
    |- hello.js
|- gulpfile.js
|- node_modules/
|- package.json
```

Ví dụ của chúng ta sẽ như sau: trong thư mục dự án node-grunt có 1 file Javascript node-grunt/src/hello.js, trong đó là code JS của bạn hoặc có nội dung như dưới đây cũng được.

```js
/**
 * Một hàm ví dụ
 *
 */
function abc()
{
    var a = 5; //Đây là biến a
    var b = 6;
    console.log(a+b);
}
```

Tác vụ mong muốn là: từ file nguồn đó tạo ra một file loại bỏ tất cả các ký tự thừa (nén), file kết quả lưu tại node-grunt/build/hello.min.js (vì để đơn giản ta chỉ làm 1 tác vụ đó, sau này bạn có thể làm nhiều, rất nhiều tác vụ khác nhau chỉ bằng gọi 1 dòng lệnh grunt)

### Gruntfile.js

Đây là file chứa JavaScript, trong đó nó chứa các thông tin: cấu hình các tác vụ, nạp các Plugin cần thiết để chạy các tác vụ ...

```js
module.exports = function(grunt) {
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        //(1) Mô tả các tác vụ ở đây ...
    });

    //(2) Nạp các plugin cung cấp chức năng của tác vụ

    //(3) Thiết lập tác vụ mặc định khi chạy Grunt
};
```

đoạn `pkg: grunt.file.readJSON('package.json')` là để Grunt đọc thông tin package, bạn để mặc định như vậy

Đầu tiên ta thêm tác vụ làm gọn file có tên `uglify` vào:

```js
module.exports = function(grunt) {
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        // ---------------------------------------------------------
        uglify: {
            options: {
                banner: '/*! Dòng này chèn vào đầu file <%= grunt.template.today("yyyy-mm-dd") %> */\n'
            },
            build: {
                files: {
                    'build/hello.min.js' : ['src/hello.js']
                }
            }
        }
        // ---------------------------------------------------------
    });
    //(2) Nạp các plugin cung cấp chức năng của tác vụ

    //(3) Thiết lập tác vụ mặc định khi chạy Grunt
}
```

Mỗi tác vụ đều có thể thiết lập cho nó qua `options` (mỗi loại task có options cụ thể, bạn thường đọc trong document của nó, ví dụ với uglify đọc tại [uglify](https://www.npmjs.com/package/grunt-contrib-uglify#banner))

## 4. Thực hiện nhiều tác vụ



## 5. Tác vụ watch



## 6. Biên dịch SASS thành CSS



## 7. Biên dịch Javascript



## Tổng kết

Bài viết mình đã hoàn thành, hy vọng có thể giúp bạn hiểu hơn về Grunt. Để tìm hiểu kỹ hơn các bạn có thể vào trang chủ của Grunt.

-----
Tham khảo:

- []()
- []()
- []()
- []()