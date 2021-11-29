---
layout: post
title: Tổng hợp về Thư viện JavaScript hiện đại
subtitle: The Modern JavaScript Library Tutorial

tags:
- JavaScript
- library
- frontend
- roadmap
- module
- tutorial
---

### Package Managers
1. [npm](#npm)
2. yarn

### Build Tools
#### Task Runners
3. npm scripts
4. Gulp

#### Module Bundlers
5. Webpack
6. Rollup
7. Parcel

-----

### Npm
`Node Package Manager`, hoặc `npm` (thường được viết bằng chữ thường) là một trong những công cụ tạo và quản lý các thư viện được sử dụng phổ biến nhất trong các dự án JavaScript. Nó được xây dựng trên Node và rất mạnh mẽ nên hầu như tất cả mọi người đều đang sử dụng nó.

Công cụ này cho phép publish các package của bạn lên trang chủ `NPM` và tìm kiếm, cài đặt các module, package do những người khác up lên.

`npm` tốt, nhưng nó cũng có một vài thiếu sót của nó. Sau đây là một vài điều trong số đó:
- **Queued install**: khi npm lấy các dependencies từ kho chứa của nó, nó sẽ cài đặt các dependencies từng cái một sau khi một cái khác được cài đặt xong, vì vậy sẽ mất rất nhiều thời gian.
- **Single registry**: Nếu như một package không có trong [NpmJS](https://www.npmjs.com), hãy quên nó đi.
- Không hỗ trợ cài đặt offline


-----
Tham khảo:
Npm
- [Quản lý các gói phụ thuộc với NPM](https://viblo.asia/p/manage-packages-dependencies-with-npm-YWOZrDLR5Q0)
- [Publish package đầu tiên lên NPM như thế nào](https://viblo.asia/p/publish-package-dau-tien-len-npm-nhu-the-nao-Do754b7VZM6)
- [Create and setup your Django project with webpack, npm and ReactJS (part1)](https://viblo.asia/p/create-and-setup-your-django-project-with-webpack-npm-and-reactjs-part1-aWj532jpl6m)
- [Yarn có gì mới so với npm](https://viblo.asia/p/yarn-co-gi-moi-so-voi-npm-Do754WR4lM6)

- [Roadmap to becoming a web developer in 2021](https://github.com/kamranahmedse/developer-roadmap)
- [Những thư viện và framework JavaScript quan trọng bạn cần biết](https://code.tutsplus.com/vi/articles/essential-javascript-libraries-and-frameworks-you-should-know-about--cms-29540)
- [The 40 Best JavaScript Libraries and Frameworks for 2021](https://kinsta.com/blog/javascript-libraries/)
- [Tương lai của JavaScript ra sao trong thế giới Front-End?](https://topdev.vn/blog/tuong-lai-cua-javascript-ra-sao-trong-the-gioi-front-end/)