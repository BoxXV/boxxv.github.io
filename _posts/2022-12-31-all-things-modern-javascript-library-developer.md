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
2. [yarn](#yarn)

### Build Tools
#### Task Runners
3. [npm scripts](#npm-scripts)
4. [Gulp](#gulp)

#### Module Bundlers
5. [Webpack](#webpack)
6. [Rollup](#rollup)
7. [Parcel](#parcel)

-----

# I. Package Managers

### 1. `npm`
`Node Package Manager`, hoặc `npm` (thường được viết bằng chữ thường) là một trong những công cụ tạo và quản lý các thư viện được sử dụng phổ biến nhất trong các dự án JavaScript. Nó được xây dựng trên Node và rất mạnh mẽ nên hầu như tất cả mọi người đều đang sử dụng nó.

Trong cộng đồng Javascript, các lập trình viên chia sẻ hàng trăm nghìn các thư viện với các đoạn code đã thực hiện sẵn một chức năng nào đó. Nó giúp cho các dự án mới tránh phải viết lại các thành phần cơ bản, các thư viện lập trình hay thậm chí cả các framework. Công cụ này cho phép publish các package của bạn lên trang chủ `NPM` và tìm kiếm, cài đặt các module, package do những người khác up lên.

Cộng đồng sử dụng npm rất lớn, hàng nghìn các thư viện được phát hành, hỗ trợ Javascript ES6, React, Express, Grunt, Duo…

`npm` tốt, nhưng nó cũng có một vài thiếu sót của nó. Sau đây là một vài điều trong số đó:
- **Queued install**: khi npm lấy các dependencies từ kho chứa của nó, nó sẽ cài đặt các dependencies từng cái một sau khi một cái khác được cài đặt xong, vì vậy sẽ mất rất nhiều thời gian.
- **Single registry**: Nếu như một package không có trong [NpmJS](https://www.npmjs.com), hãy quên nó đi.
- Không hỗ trợ cài đặt offline

-----

### 2. `Yarn`

Yarn là một sản phẩm mã nguồn mở, được sự hợp tác của Exponent, Google và Tilde. Với Yarn, các lập trình viên vẫn truy cập vào kho cung cấp các gói phần mềm do npm lưu trữ, tuy nhiên chúng ta có thể cài đặt các gói phần mềm này nhanh hơn và đảm bảo tính thống nhất các lập trình viên tham gia cài đúng phiên bản của các gói phần mềm được định nghĩa.

Đây là dự án bắt đầu được viết từ tháng 1/2016, sau quãng thời gian thử nghiệm và hoàn thiện đã được mở ra thành mã nguồn mở, và thật không có gì ngạc nhiên khi với những tính năng nổi trội vượt bậc đã có 10.000 stars chỉ trong 1 ngày tại Github. Chứng tỏ sự thành công và là tín hiệu thay thế rõ ràng NPM.

`Yarn` được đưa ra để thay thế cho `npm` hoặc các công cụ quản lí các gói thư viện khác cũng tương tác với kho cung cấp các gói phần mềm do npm cung cấp. Nó có đầy đủ những tính năng của npm trong khi đó lại nhanh hơn, bảo mật hơn và đáng tin cậy. Vì vậy bạn hoàn toàn có thể yên tâm khi dùng Yarn thay thế cho npm, bower ...

Đặc trưng
- **Tốc độ**: YARN sẽ tạo cache cho tất cả các gói đã được tải về, và tải đồng thời nhiều gói cùng lúc nên tốc độ download rất nhanh.
- **Tin cậy**: sử dụng tập tin lock (tương tự composer) với format chi tiết nhưng ngắn gọn, đảm bảo tính nhất quán khi cài đặt các gói giữa các hệ thống (ví dụ máy dev và máy chủ)
- **Bảo mật**: sử dụng checksum để đảm bảo tính nguyên vẹn của code trước khi nó được thực thi.

Tính năng
- **Offline mode**: khi đã tải về, YARN sẽ cache lại và khi có thể cài đặt lại không cần internet.
- **Deterministic**: các gói thư viện sẽ được cài đặt nhất quán cho dù thứ tự cài đặt khác nhau cho tất cả các máy
- **Network Performance**: sử dụng hiệu quả hàng đợi các request và tránh waterfall các request để tối ưu tốc độ mạng.
- **Multiple Registries**: cài đặt các gói từ các registries như Bower hay NPM đều đảm bảo workflow giống nhau.
- **Network Resilience**: nếu một request bị fail thì nó không làm cho tiến trình bị dừng lại, khác với npm là nếu npm bị lỗi thì bị dừng lại., không những vậy mà còn có khả năng cố gắng thử lại.
- **Flat Mode**: giải quyết việc không đồng nhất phiên bản của các gói thành 1 gói để tránh tạo trùng lặp

Với nhiều cải tiến đáng kể của mình so với npm yarn rất đáng để thử và trải nghiệm với dự án của bạn. Bạn có thể tham khảo thêm các lệnh khi chuyển từ sử dụng npm sang yarn ở đây [migrating from npm](https://classic.yarnpkg.com/en/docs/migrating-from-npm)

Do YARN cũng sử dụng package.json nên nếu dự án đã có thì việc sử dụng YARN cũng không khác mấy, chỉ cần bạn xóa tất cả các thư mục trong `node_modules`, sau đó dùng yarn để cài lại.


-----

# II. Build Tools
## A. Task Runners
### 3. `npm scripts`

### 4. `Gulp`

## B. Task Runners
### 5. `Webpack`

### 6. `Rollup`

### 7. `Parcel`



-----
Tham khảo:
Npm
- [https://viblo.asia/tags/npm](https://viblo.asia/tags/npm)
- [Cách tạo một NPM package đơn giản](https://viblo.asia/p/cach-tao-mot-npm-package-don-gian-3P0lPy3o5ox)
- [Tạo packages trong npm](https://viblo.asia/p/tao-packages-trong-npm-node-packages-manager-YWOZr6dNZQ0)
- [Quản lý các gói phụ thuộc với NPM](https://viblo.asia/p/manage-packages-dependencies-with-npm-YWOZrDLR5Q0)
- [Build và Publish một NPM Typescript package](https://viblo.asia/p/build-va-publish-mot-npm-typescript-package-gDVK2nGnKLj)
- [Publish package đầu tiên lên NPM như thế nào](https://viblo.asia/p/publish-package-dau-tien-len-npm-nhu-the-nao-Do754b7VZM6)
- [The package.json guide](https://viblo.asia/p/the-packagejson-guide-bWrZn0zY5xw)
- [Package-lock.json và những điều có thể bạn chưa biết](https://viblo.asia/p/package-lockjson-va-nhung-dieu-co-the-ban-chua-biet-RQqKL2WOl7z)
- [Tổng quan về NPM](https://viblo.asia/p/tong-quan-ve-npm-4P856dy3ZY3)
- [Mẹo và thủ thuật để làm việc với NPM](https://viblo.asia/p/meo-va-thu-thuat-de-lam-viec-voi-npm-djeZ1epYZWz)
- [Create and setup your Django project with webpack, npm and ReactJS (part1)](https://viblo.asia/p/create-and-setup-your-django-project-with-webpack-npm-and-reactjs-part1-aWj532jpl6m)
- [Sự khác nhau giữa npm và npx?](https://viblo.asia/p/su-khac-nhau-giua-npm-va-npx-bWrZnxM95xw)

-----
- [NPM, Yarn và Javascript](https://viblo.asia/p/npm-yarn-va-javascript-Eb85orNml2G)
- [Cài đặt một số Package trước khi làm dự án Nodejs](https://viblo.asia/p/cai-dat-mot-so-package-truoc-khi-lam-du-an-nodejs-Qpmlejm75rd)
- [Làm cách nào để sửa đổi thư viện trong node module](https://viblo.asia/p/lam-cach-nao-de-sua-doi-thu-vien-trong-node-module-eW65G6AalDO)

-----
- [https://viblo.asia/tags/yarn](https://viblo.asia/tags/yarn)
- [Yarn có gì mới so với npm](https://viblo.asia/p/yarn-co-gi-moi-so-voi-npm-Do754WR4lM6)
- [Yarn - Một cải tiến đáng kể so với NPM](https://viblo.asia/p/yarn-mot-cai-tien-dang-ke-so-voi-npm-yMnKMqRQK7P)
- [Hướng Dẫn Cài Đặt và Sử Dụng Yarn Package Manager](https://viblo.asia/p/huong-dan-cai-dat-va-su-dung-yarn-package-manager-4dbZNgoklYM)
- [Sử dụng Yarn với Rails](https://viblo.asia/p/su-dung-yarn-voi-rails-gDVK2jaAKLj)
- [Sử dụng Yarn trong dự án Laravel](https://viblo.asia/p/su-dung-yarn-trong-du-an-laravel-chuyen-training-php-tai-framgia-education-1Je5EjWAKnL)
- [Ứng dụng Yarn workspaces tạo ra những dự án Monorepo](https://viblo.asia/p/ung-dung-yarn-workspaces-tao-ra-nhung-du-an-monorepo-QpmleyXolrd)
- [Viết Javascript trong Rails 6 có gì khác? (với Webpacker, Yarn và Sprockets)](https://viblo.asia/p/viet-javascript-trong-rails-6-co-gi-khac-voi-webpacker-yarn-va-sprockets-924lJ4e0KPM)

-----
[Sử dụng npm như một Build Tool](https://viblo.asia/p/su-dung-npm-nhu-mot-build-tool-jdWrvwq8Mw38)
[Mở đầu với Gulp](https://viblo.asia/p/mo-dau-voi-gulp-l5XRBVxmRqPe)
[Gulp for beginner](https://viblo.asia/p/gulp-for-beginner-WAyK89knZxX)
[So sánh Gulp và Grunt](https://viblo.asia/p/so-sanh-gulp-va-grunt-157G5oY5RAje)

-----
- [Roadmap to becoming a web developer in 2021](https://github.com/kamranahmedse/developer-roadmap)
- [Những thư viện và framework JavaScript quan trọng bạn cần biết](https://code.tutsplus.com/vi/articles/essential-javascript-libraries-and-frameworks-you-should-know-about--cms-29540)
- [The 40 Best JavaScript Libraries and Frameworks for 2021](https://kinsta.com/blog/javascript-libraries/)
- [Tương lai của JavaScript ra sao trong thế giới Front-End?](https://topdev.vn/blog/tuong-lai-cua-javascript-ra-sao-trong-the-gioi-front-end/)