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

![repository](https://boxxv.github.io/img/posts/1 iWRF_3Dpj05_K4Pp-iDK8Q.png "repository")

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


### Xếp lớp (Scaffold) thư viện

Webpack có một hướng dẫn tuyệt vời về [cách tạo thư viện](https://webpack.js.org/guides/author-libraries/), hãy mượn cấu trúc thư mục của nó.

{% highlight js %}
mkdir -p {src,dist,examples/browser,examples/node}

touch src/index.js examples/browser/index.html examples/node/example.js
{% endhighlight %}

Bây giờ cấu trúc thư mục sẽ giống như sau:

{% highlight js %}
.
├── dist
├── examples
│   ├── browser
│   │   └── index.html
│   └── node
│       └── example.js
└── src
    └── index.js
{% endhighlight %}


### Triển khai thư viện
Đã đến lúc triển khai thư viện!

**src/index.js**
{% highlight js %}
module.exports = {
  add: (num1, num2) => num1 + num2,
  sub: (num1, num2) => num1 - num2,
};
{% endhighlight %}

Như bạn có thể thấy, máy tính của chúng tôi rất đơn giản.

**examples/node/example.js**
{% highlight js %}
const {add, sub} = require('./calculator.js');
console.log('1 + 2 = ' + add(1, 2));
console.log('2 - 1 = ' + sub(2, 1));
{% endhighlight %}

**examples/browser/index.html**
{% highlight js %}
<html>
<head>
  <title>Test Calculator</title>
</head>
<body>
  <script src='./calculator.js'></script>
  <script>
    const {add, sub} = calculator;
    console.log('1 + 2 = ' + add(1, 2));
    console.log('2 - 1 = ' + sub(2, 1));
  </script>
</body>
</html>
{% endhighlight %}

Hai tệp trên được sử dụng chủ yếu để thử nghiệm cục bộ.


### Kết hợp (Bundle) thư viện

Chúng tôi cần cấu hình `Webpack` và `Babel` để làm cho chúng hoạt động cho chúng tôi.

{% highlight js %}
touch webpack.config.js .babelrc
{% endhighlight %}

**webpack.config.js**
{% highlight js %}
const path = require('path');module.exports = {
  mode: 'production',
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'calculator.js',
    library: 'calculator',
    libraryTarget: 'umd',
    globalObject: 'this',
  },
  module: {
    rules: [{
      test: /\.js$/,
      exclude: /(node_modules)/,
      use: 'babel-loader',
    }],
  },
};
{% endhighlight %}

**.babelrc**
{% highlight js %}
{
  "presets": ["@babel/preset-env"]
}
{% endhighlight %}

Và chúng ta cần cập nhật `package.json`. Phần quan trọng nhất ở đây là thay đổi thuộc tính `main` để nó trỏ tới `dist/calculator.js`.

**package.json**
{% highlight js %}
"main": "dist/calculator.js",
"scripts": {
  "build:browser": "webpack && cp dist/calculator.js examples/browser",
  "build:node": "webpack && cp dist/calculator.js examples/node/ && node examples/node/example.js",
  "build": "webpack"
}
{% endhighlight %}

Ồ, hãy đảm bảo rằng thư mục `dist` được bao gồm trong bản phân phối cuối cùng, chỉ cần bỏ ghi chú dòng `dist` nếu bạn thấy.

{% highlight js %}
...
# Nuxt.js build / generate output
.nuxt
# dist
{% endhighlight %}


### Thử nghiệm thư viện

Hãy thực hiện một số thử nghiệm cục bộ nhanh theo cách thủ công để đảm bảo thư viện có thể hoạt động với Node.js và trình duyệt. 

{% highlight js %}
> npm run build:node1 + 2 = 3
2 - 1 = 1

> npm run build:browser
{% endhighlight %}

![Test the library](https://boxxv.github.io/img/posts/1 Bh62kEBEFrGAq3i0kKA51A.png "Test the library")

Xuất sắc! Chúng tôi vừa hoàn thành cột mốc đầu tiên của mình, đã đến lúc phát hành!


## 2. Tự động hóa các bản phát hành

Tôi đã từng sử dụng bản [release-it](https://github.com/release-it/release-it) để phát hành thư viện theo cách thủ công và tôi cần quyết định xem đó là bản vá, bản phát hành nhỏ hay chính.

[semantic-release](https://github.com/semantic-release/semantic-release) sử dụng các thông điệp commit để quyết định kiểu phát hành miễn là các thông báo commit tuân theo kiểu [commit thông thường](https://www.conventionalcommits.org/en/v1.0.0/). Và phát hành ngữ nghĩa có một số plugin để tạo bảng thay đổi, xuất bản lên Github và NPM với ghi chú phát hành, vì vậy hãy sử dụng nó.


### Cài đặt phần phụ thuộc Node.js

{% highlight js %}
> npm i -D husky @semantic-release/{changelog,git,github,npm,commit-analyzer,release-notes-generator} @commitlint/{cli,config-conventional}
{% endhighlight %}

Chúng tôi sử dụng `husky` để kết nối với các lệnh git, về cơ bản, chúng tôi cần đảm bảo rằng các thông báo cam kết tuân theo kiểu cam kết thông thường, bạn sẽ thấy nó được định cấu hình như thế nào sau này. 

### Cấu hình cục bộ

Có một số thứ chúng ta cần phải cấu hình.

{% highlight js %}
> touch commitlint.config.js .releaserc
{% endhighlight %}

**commitlint.config.js**
{% highlight js %}
module.exports = {
  extends: [
    '@commitlint/config-conventional'
  ]
};
{% endhighlight %}

Điều này được sử dụng để lint các thông điệp cam kết của chúng tôi.

**.releaserc**
{% highlight js %}
{
  "plugins": [
    "@semantic-release/commit-analyzer",
    "@semantic-release/release-notes-generator",
    ["@semantic-release/changelog", {
      "changelogFile": "docs/CHANGELOG.md",
    }],
    "@semantic-release/npm",
    ["@semantic-release/git", {
      "assets": ["dist/**/*.{js,css}", "docs", "package.json"],
      "message": "chore(release): ${nextRelease.version} [skip ci]\n\n${nextRelease.notes}"
    }],
    "@semantic-release/github"
  ]
}
{% endhighlight %}

Đây là cấu hình của semantic-release. Có một điều rất quan trọng cần biết rằng tất cả các plugin đều được thực thi theo thứ tự như đã định nghĩa!

Cập nhật package.json, chúng tôi sẽ đặt tên cho gói của mình bằng cách làm theo [kiểu đặt tên gói có phạm vi của NPM](https://docs.npmjs.com/cli/v7/using-npm/scope). Đặt lại số phiên bản thành `0.0.0`, định cấu hình `husky`, thêm tập lệnh để thực hiện phát hành ngữ nghĩa sau này.

Nhận thấy rằng chúng tôi cũng có một `publishConfig` và đặt thuộc tính `access` thành “public”, điều này được sử dụng vì chúng tôi sử dụng tên gói phạm vi.

{% highlight js %}
"name": "@jeantimex/calculator",
"version": "0.0.0",
"husky": {
  "hooks": {
    "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
  }
},
"publishConfig": {
  "access": "public"
},
"scripts": {
  ...
  "semantic-release": "semantic-release"
}
{% endhighlight %}

Được rồi, cấu hình cục bộ đã hoàn tất, hãy chuyển sang phần điều khiển từ xa.

Chúng tôi sẽ sử dụng [Travis CI](https://travis-ci.org) để giúp tự động hóa việc phát hành.

### Cấu hình từ xa: thiết lập Travis

Đầu tiên, kích hoạt kho lưu trữ, nhấp vào nút `Sync account` để Travis chọn kho lưu trữ mới tạo từ Github.

![Remote configurations: set up Travis](https://boxxv.github.io/img/posts/1 scEyeW4Oe7DNhwLdSEKEGg.png "Remote configurations: set up Travis")





-----
Tham khảo:
- [Tạo thư viện JavaScript và tự động hóa hoàn toàn các bản phát hành vào năm 2020 ](https://medium.com/@jeantimex/create-a-javascript-library-and-fully-automate-the-releases-ccce93153dbb)
