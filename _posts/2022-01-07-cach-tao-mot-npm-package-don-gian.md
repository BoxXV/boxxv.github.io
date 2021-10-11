---
layout: post
title: Cách tạo một NPM package đơn giản
subtitle: Creating a simple npm library to use in and out of the browser

tags:
- JavaScript
- library
- frontend
- roadmap
- module
- tutorial
---

### Nên biết trước khi đọc bài

- Git cơ bản
- Cấu hình `webpack` cơ bản. Đó là nên biết thì giúp bạn đọc hiểu nhanh hơn, còn không thì cũng chả sao, bạn cứ làm theo command trong bài là sẽ tạo NPM package thành công. Mục đích của chúng ta là tạo được một NPM Package mà. 😄

## Tại sao phải tạo NPM package

NPM (Node Package Manager) là một trình quản lý các gói mã nguồn Javascript được cài đặt kèm theo sẵn với NodeJS. Các gói này được gọi là NPM Package. Các NPM package được phát triển bởi các developer, họ publish ra và package của họ được tải lên server của NPM. Sau này muốn dùng tới package đó, bạn chỉ cần cài đặt nhanh chóng với command:

{% highlight js %}
npm install package-name
{% endhighlight %}

Đơn giản như vậy bạn đã cài đặt xong package có tên là **package-name** vào project của mình.

Trong nhiều dự án sử dụng Javascript bạn gặp phải nhiều vấn đề chung. Bạn lên mạng tìm các package đã có trước đó để giải quyết vấn đề. Tuy nhiên, nhiều trường hợp chớ trêu thay, cái package bạn tìm được nó không làm hài lòng bạn: cái thì nặng, cái thì khó dùng, cái thì phải cài thêm jQuery... Mà chính bạn lại có thể tự giải quyết được vấn đề đó theo một cách riêng gọn lẹ của mình. Bạn muốn cách giải quyết đơn giản đấy có thể dễ dàng áp dụng sang các dự án khác. Nên bạn mở lại project cũ để tìm và bê lại code đó sang dự án mới. Bạn thấy phiền hà khó chịu khi phải lục lọi code như thế. Vậy đây là lúc bạn đọc thêm về bài viết này. Bài viết này sẽ hướng dẫn bạn tạo một NPM package, publish và cài đặt thông qua NPM trong vòng một nốt nhạc.

Bài viết này sẽ tạo mẫu một NPM package đơn giản. Có tên là **Simple Scrollspy**, phục vụ cho việc tạo hiệu ứng ScrollSpy thích hợp cho website dạng landing page, hoặc một số khác bạn muốn 😄. Nếu bạn chưa biết ScrollSpy là gì bạn có thể xem qua bức ảnh mẫu dưới đây. Mô tả hiệu ứng ScrollSpy với package của Bootstrap. Đó chính là hiệu ứng ScrollSpy.

![ScrollSpy](https://boxxv.github.io/img/posts/7434635f-7330-4a38-9d66-b395a5611ec3.gif "ScrollSpy")

## Cách tạo NPM package

Package đương nhiên là phải chứa code, vậy đương nhiên bạn phải tạo một thư mục chứa code trên máy tính của bạn để bạn phát triển nó. Mình viết theo chuẩn ES6 nên mình cần một tool để thực hiện compiling mã nguồn. Mình sẽ sử dụng `Webpack`, phiên bản mới nhất hiện tại là Version 4.4.1.

{% highlight js %}
mkdir simple-scrollspy
cd simple-scrollspy
{% endhighlight %}

Bạn đang ở thư mục simple-scrollspy, mình sẽ thực hiện các bước như sau:
- Tạo file package.json mô tả package của bạn với trình quản lý NPM.
- Khởi tạo git repository.
- Tạo file cấu hình cho webpack webpack.config.js.
- Viết code.
- Publish lên server của NPM để có thể cài đặt vào project thông qua NPM.

### Tạo package.json

Tại folder simple-scrollspy, thực hiện:

{% highlight js %}
npm init

# Results:
....

Press ^C at any time to quit.
name: (simple-scrollspy)
{% endhighlight %}

Màn hình khởi tạo package hiện ra như trên bạn điền các thông số theo hướng dẫn. Sau khi điền xong, nó sẽ hỏi `Is this ok? (yes)` để xác nhận, gõ 'yes' để hoàn tất. Trong quá trình nhập, bạn có thể nhấn Ctrl + C để hủy bỏ việc tạo package.json.

> Note:
> - Thuộc tính name của package phải ở dạng viết liền không dấu, và có thể sử dụng - để phân cách.
> - Để trống và nhấn Enter để sử dụng giá trị mặc định. VD: name: (simple-scrollspy), để trống và nhấn Enter tương đương với việc sử dụng tên mặc định là simple-scrollspy.
> - Thuộc tính entry point là đường dẫn trở tới file mã nguồn, điểm chạy đầu tiền của package của bạn.
> - Thông thường, mã nguồn thường được các developer đặt trong thư mục src. Các file sau khi compile thường cho ra thư mục có tên là dist.

Mình thực hiện nhập như sau và tạo thành công file package.json:

{% highlight js %}
[14:57] simple-scrollspy  $ npm init
...
Press ^C at any time to quit.
name: (simple-scrollspy)
version: (1.0.0)
description: ScrollSpy effect for website.
entry point: (index.js) src/index.js
test command:
git repository: git@github.com:huukimit/simple-scrollspy.git
keywords: ScrollSpy, Javascript, umd
author: Nguyen Huu Kim <kimnguyen.ict@gmail.com>
license: (ISC) MIT
About to write to /home/nguyen.huu.kim/projects/simple-scrollspy/package.json:

{
  "name": "simple-scrollspy",
  "version": "1.0.0",
  "description": "ScrollSpy effect for website.",
  "main": "src/index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/huukimit/simple-scrollspy.git"
  },
  "keywords": [
    "ScrollSpy",
    "Javascript",
    "umd"
  ],
  "author": "Nguyen Huu Kim <kimnguyen.ict@gmail.com>",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/huukimit/simple-scrollspy/issues"
  },
  "homepage": "https://github.com/huukimit/simple-scrollspy#readme"
}


Is this ok? (yes) yes
[15:01] simple-scrollspy
{% endhighlight %}

Bây giờ hãy tạo thư mục `src` và file `index.js`.

{% highlight js %}
mkdir src
touch src/index.js
{% endhighlight %}

### Khởi tạo git repository

Mình sẽ làm như sau:

- Khởi tạo git
- Thêm file `README.md`, giới thiệu về package.
- Thêm file .gitignore để ignore những file, folder không cần thiết cần phải thêm vào git. Đặc biệt là 2 folder `node_modules` và `.idea` mình cần phải ignore đầu tiên. Trong đó, `node_modules` thì bạn đã biết. Còn `.idea` là thư mục được tạo ra bởi IDE `PHPStorm` mà mình đang sử dụng, folder chỉ sử dụng tại máy mình, không dùng cho người khác nên chúng ta cần phải ignore.
- Đăng ký/đăng nhập vào Github rồi tạo một repository có tên giống tên package `simple-scrollspy`. Tạo một mối liên kết từ repository trên github với máy tính của mình.

{% highlight js %}
# Khởi tạo git
git init

# Thêm file README.md
touch README.md
echo "# Simple ScrollSpy" > README.md

# Thêm file .gitignore
touch .gitignore
echo "/node_modules\n/.idea\n"
{% endhighlight %}

Tạo git commit đầu tiên:

{% highlight js %}
git add .
git commit -m "Initial commit"
{% endhighlight %}

Tạo mối liên kết với github:

{% highlight js %}
git remote add origin <git_repository_url>
{% endhighlight %}

Git repisitory url, bạn lấy bằng cách nhấn nút `Clone or download` rồi copy url hiển thị ra.

### Tạo file webpack.config.js

Tạo file webpack.config.js để cấu hình cho webpack compile code của mình thừ ES6 sang javascript thuần, để mình có thể chạy thử code trước khi publish. Trước hết, ta phải cài webpack package qua NPM.

{% highlight js %}
npm install webpack webpack-cli uglifyjs-webpack-plugin --save-dev
{% endhighlight %}

Sau đó, tạo file config:

{% highlight js %}
touch webpack.config.js
{% endhighlight %}

Bạn mở file webpack.config.js bằng IDE của bạn, mình dùng PHPStorm. Sau đó bạn lưu lại với nội dung như sau:

{% highlight js %}
// webpack.config.js

const {resolve} = require('path')
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')

module.exports = {
    entry: resolve(__dirname, 'src/index.js'),
    output: {
        path: resolve(__dirname, 'dist'),
        filename: 'simple-scrollspy.js',
        library: 'scrollSpy'
    },
    plugins: [
        new UglifyJsPlugin({
            exclude: [/\.min\.js$/gi] // skip pre-minified libs
        })
    ]
}
{% endhighlight %}

Bạn có thể hiểu nội dung file cấu hình trên rằng mình đang nói chuyện với webpack với nội dung sau:

- Webpack ơi, chú mày sẽ tìm đến entry point của anh, có địa chỉ là `src/index.js` và compile code trong đó cho anh.
- Sau đó, nội dung được biên dịch ra file và đặt nó vào địa chỉ `dist/simple-scrollspy.js (output)`. Nội dung file này của anh chú cần đặt tên cho nó là `scrollSpy` nhé (`library`). Để sau này anh có thể thêm file này vào HTML qua thẻ `<script src="/dist/simple-scrollspy.js"></script>` mà anh vẫn dùng được.
- À, anh cho chú mày thêm một cuốn bí kíp võ công `UglifyJsPlugin` để chú minify file đấy cho nó có dung lượng bé nhất.

Sau khi nói như vậy, webpack sẽ hiểu và làm đúng như trên. Để kiểm tra cơ bản, bạn sửa file `package.json`, tìm `"scripts"` và sửa một chút như sau:

{% highlight js %}
"scripts": {
    "dev": "node_modules/webpack/bin/webpack.js --mode production --watch --progress --hide-modules",
    "build": "node_modules/webpack/bin/webpack.js --mode production --progress --hide-modules"
},
{% endhighlight %}

Như vậy, chúng ta đã bảo với NPM rằng chúng ta có 2 script có tên là `build` và `dev` để thuận tiện cho việc compile với webpack. Khi đó ta có thể chạy 2 lệnh trên bằng cách:

{% highlight js %}
npm run build
{% endhighlight %}

hoặc

{% highlight js %}
npm run dev
{% endhighlight %}

Giờ hãy test thử nào! Bạn sẽ thấy webpack làm đúng như lời mình bảo ở trên. Chúng ta sẽ chuyển qua phần tiếp theo là viết code.

### Viết code

- Mình tạo file `demo/index.html` để mình dùng thử xem code hoạt động đúng không. Nếu không sẽ sửa lại code.
- Sử dụng lệnh `build` và `dev` mình cấp ở trên để webpack thực hiện compile code sang javascript thuần. Trong đó, `build` đơn thuần là build ra file `dist/simple-scrollspy.js` còn `dev`, ngoài việc `build` như trên thì nó sẽ theo dõi file, cứ mỗi khi code trong `src/index.js` thay đổi thì nó sẽ thực hiện build lại.

{% highlight js %}
npm run build
npm run dev
{% endhighlight %}


## Publish NPM package

Để publish, trước hết bạn cần:

- Cập nhật nội dung documentation cho package vào file README.md.
- Tăng version trong file package.json.
- Commit và push toàn bộ code mới lên nhánh master của Github.
- Login vào NPM server và publish

Hai bước đầu bạn đã hiểu, bước thứ 3 bạn làm như sau để commit và push toàn bộ code mới lên github:

{% highlight js %}
git add .
git commit -m "Release version 1.0.0"
git push origin master -f
{% endhighlight %}

Cuối cùng, bạn truy cập [npm website](https://www.npmjs.com) đăng ký tài khoản, xác nhận email và đăng nhập vào website thử. Bạn phải đảm bảo bạn đăng nhập thử được. Rồi tại thư mục `simple-scrollspy`, bạn làm như sau để login vào NPM:

{% highlight js %}
[15:58] simple-scrollspy  $ npm login
Username: kimnguyen.ict
Password:
Email: (this IS public) kimnguyen.ict@gmail.com
Logged in as kimnguyen.ict on https://registry.npmjs.org/.
{% endhighlight %}

Cùng publish nào!

{% highlight js %}
npm publish
{% endhighlight %}

> Note:
> Sử dụng file .npmignore tương tự .gitignore để ignore những file mà bạn không muốn đẩy lên theo NPM.

Bây giờ, bạn truy cập lại website của npm để kiểm tra package của bạn đã xuất hiện trên đó chưa nhé. Chúc các bạn thành công! ^-^

Một số link hữu ích
- [Source code: Simple Scrollspy](https://github.com/huukimit/simple-scrollspy)
- [simple-scrollspy package đã được publish](https://www.npmjs.com/package/simple-scrollspy)
- [Demo sử dụng simple-scrollspy](https://huukimit.github.io/simple-scrollspy/demo/)


-----
Tham khảo:
- [Cách tạo một NPM package đơn giản](https://viblo.asia/p/cach-tao-mot-npm-package-don-gian-3P0lPy3o5ox)