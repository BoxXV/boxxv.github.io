---
layout: post
title: Viết thư viện cho JavaScript với Rollup
subtitle: Bundling your own JS library with Rollup
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

## 1. Giới thiệu

Có lẽ chúng ta đã rất quen thuộc với Webpack - một module bundler được dùng rất nhiều trong việc xây dựng JavaScript application. **Rollup** cũng vậy, nó là một module bundler dành cho JavaScript. Có tác dụng đóng gói những phần code nhỏ thành một gói. Bạn có thể xem hình minh họa bên dưới để hiểu bản chất của module bundler.

![Nguồn: freecodecamp.org](https://boxxv.github.io/img/posts/module-bundler.png "Nguồn: freecodecamp.org")

## 2. Cài đặt

### Global

{% highlight js %}
$ npm install -g rollup
{% endhighlight %}

Sau khi cài đặt, các bạn có thể gõ `rollup --help` trên command-line để xem những option, parameter mà `rollup` hỗ trợ.

Bây giờ chúng ta sẽ bundle thử một ví dụ nhỏ sau để xem cách Rollup hoặc động.

![simple-build](https://boxxv.github.io/img/posts/simple-build.png "simple-build")

**main.js**
{% highlight js %}
const hello = function(name) {
  return 'Hello ' + name
};

export default hello;
{% endhighlight %}

Đoạn code trên sẽ export một function `hello`, trả về kết quả là `Hello [name]`.

Chúng ta sẽ build thử với Rollup.

{% highlight js %}
$ rollup main.js --file bundle.js --format iife --name hello
{% endhighlight %}

Sau khi build, file `bundle.js` của chúng ta sẽ như sau:

**bundle.js**
{% highlight js %}
var hello = (function() {
  'use strict';

  const hello = function(name) {
    return 'Hello ' + name
  };

  return hello;
})();
{% endhighlight %}

Mình sẽ include file `bundle.js` và gọi function `hello('12bit.vn')`

**index.html**
{% highlight js %}
...
<script src="./bundle.js"></script>
<script>
  console.log(hello('12bit.vn'))
</script>
...
{% endhighlight %}

Kết quả console trên trình duyệt đã output `Hello 12bit.vn`

![simple-build-result](https://boxxv.github.io/img/posts/simple-build-result.png "Kết quả như mong muốn :tada:")

Và đương nhiên nếu bạn include `main.js` thì trình duyệt sẽ báo lỗi, vì nó không hiểu được `export`.

![simple-build-error](https://boxxv.github.io/img/posts/simple-build-error.png "hello is not defined")


### Local



-----
Tham khảo:
- [Bundling your own JS library with Rollup](https://cagline.medium.com/bundling-your-own-js-library-with-rollup-5db82e89ab9)
- [How to Bundle JavaScript With Rollup — Step-by-Step Tutorial](https://www.learnwithjason.dev/blog/learn-rollup-js)
- [Create a JavaScript library. Configure Dev Build using Rollup.js](https://dev.to/alexandrshy/create-a-javascript-library-configure-dev-build-using-rollup-js-3p6c)
- [**How to Publish a JS and CSS Library to NPM Using Rollup**](https://medium.com/geekculture/how-to-publish-a-js-and-css-library-to-npm-using-rollup-5406dbee51fa)
- [Authoring a JavaScript library that works everywhere using Rollup](https://adostes.medium.com/authoring-a-javascript-library-that-works-everywhere-using-rollup-f1b4b527b2a9)
- [How I set-up a React component library with Rollup](https://medium.com/grandata-engineering/how-i-set-up-a-react-component-library-with-rollup-be6ccb700333)
- [Creating a React library using Rollup & Gulp](https://giladlevari.medium.com/creating-a-react-library-using-rollup-gulp-d0463103fcf6)
- [Making a modern JS library in 2020](https://pitayan.com/posts/modernest-lib-hello-world/)

