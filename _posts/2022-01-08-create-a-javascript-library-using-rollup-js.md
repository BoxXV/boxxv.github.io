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

**`main.js`**
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

**`bundle.js`**
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

**`index.html`**
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

Trong trường hợp bạn không muốn dùng command `rollup` global, thì có thể cài local và chỉ sử dụng được trong scope của project.

{% highlight js %}
$ npm install rollup --save-dev
# hoặc dùng yarn
$ yarn add rollup -D
{% endhighlight %}

Sau khi cài đặt thì bạn có thể sử dụng giống như global. Nhưng lúc này bạn phải khai báo Rollup trong npm scripts hoặc dùng lệnh [npx](https://12bit.vn/references/npx/) :

{% highlight js %}
$ npx rollup -h
{% endhighlight %}


## 3. Rollup format

Rollup hỗ trợ chung ta bundle code lại với nhiều format như: `amd`, `cjs`, `esm`, `iife`, `umd`. Đây chính là sức mạnh để Rollup được dùng trong việc build library có thể chạy trên nhiều môi trường như Node.js, browser, ES.

Như ví dụ trên, mình đã bundle code lại với format là [iife](https://12bit.vn/articles/tim-hieu-ve-immediately-invoked-function-expression-iife-trong-javascript/) để có thể chạy trên môi trường browser.

Để bundle code với những format khác nhau, các bạn có thể dùng flag

`--format [format]`

{% highlight js %}
# build library dùng trên browser.
$ rollup --main --file bundle.js --format iife

# build library dùng trong môi trường Node.js
$ rollup --main --file bundle.js --format cjs
{% endhighlight %}

Để hiểu về các formats: amd, cjs, esm, iife, umd. Bạn có thể đọc bài viết [JAVASCRIPT: What the heck are CJS, AMD, UMD, and ESM?](https://dev.to/iggredible/what-the-heck-are-cjs-amd-umd-and-esm-ikm) trên dev.to


## 4. Rollup plugin

Việc một bundler hỗ trợ plugin đã điều rất cần thiết, vì một bundler không thể nào tích hợp tất cả mọi thứ dạng `built-in` được và cũng không phải ai cũng muốn dùng những tính năng giống nhau. Vì vậy việc dùng plugin sẽ rất linh hoạt và có khả năng mở rộng đối với những app / library phức tạp.

Rollup hỗ trợ rất nhiều plugins ví dụ như transpile ES6/7 -> ES5, compile CSS preprocessor, minify JS,…

Mình sẽ lấy một ví dụ sử dụng plugin [rollup-plugin-babel](https://github.com/rollup/rollup-plugin-babel) để chuyển đổi code JS dạng ES6 thành ES5.

Chúng ta tiếp tục sử dụng ví dụ đầu tiên. Nhưng bây giờ trong file `main.js` sẽ được viết lại một chút, sử dụng [spead syntax trong ES6](https://12bit.vn/articles/spread-operator-trong-es6/)

{% highlight js %}
const helloWithSpread = name => `Hello ${[...name].join('-')}`

export default helloWithSpread;
{% endhighlight %}

Nếu chưa dùng plugin để transpile ES6 -> ES5, thì file `bundle.js` sau khi build sẽ như sau:

{% highlight js %}
var helloWithSpread = (function () {
	'use strict';

	const helloWithSpread = name => `Hello ${[...name].join('-')}`;

	return helloWithSpread;
}());
{% endhighlight %}

Bạn thấy đó! code vẫn vậy, điều này sẽ khiến cho những trình duyệt không [hỗ trợ spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#browser_compatibility) báo lỗi. Chúng ta sẽ sửa lại bằng cách cài thêm plugin babel.

{% highlight js %}
$ yarn add -D rollup-plugin-babel@latest @babel/core @babel/preset-env
{% endhighlight %}

Chúng ta cần phải cài thêm `@babel/core` và `@babel/preset-env` thì plugin mới hoạt động được.


## 5. File config

Khi đã dùng plugin, chúng ta cần phải khai báo plugin trong file config riêng cho Rollup (cũng giống như `webpack.config.js` vậy).

Các bạn sẽ tạo một file tên là `rollup.config.js`, với nội dung như sau:

**`rollup.config.js`**
{% highlight js %}
import babel from 'rollup-plugin-babel'

export default {
  input: 'main.js',
  output: {
    file: 'bundle.js',
    name: 'helloWithSpread',
    format: 'iife'
  },
  plugins: [
    babel({
      exclude: 'node_modules/**'
    })
  ]
}
{% endhighlight %}

Đơn giản phải không nào! Tiếp theo các bạn khai báo script trong `package.json`

{% highlight js %}
...
"scripts": {
  "build": "rollup --config"
},
...
{% endhighlight %}

Rollup sẽ tự động detect file `rollup.config.js` trong root folder nếu bạn không truyền đường dẫn tới file config cho `--config`.

Trường hợp bạn muốn dùng nhiều file config cho những ngữ cảnh khác nhau thì có thể khai báo như sau:

{% highlight js %}
...
"scripts": {
  "build:es": "rollup --config path/to/rollup.config.es.js",
  "build:iife": "rollup --config path/to/rollup.config.iife.js",
  "build:umd": "rollup --config path/to/rollup.config.umd.js"
},
...
{% endhighlight %}

Sau khi build với plugin babel. Chúng ta sẽ được file `bundle.js` như sau:

{% highlight js %}
var helloWithSpread = (function () {
  'use strict';

  function _toConsumableArray(arr) {
    return _arrayWithoutHoles(arr) || _iterableToArray(arr) || _nonIterableSpread();
  }

  function _arrayWithoutHoles(arr) {
    if (Array.isArray(arr)) {
      for (var i = 0, arr2 = new Array(arr.length); i < arr.length; i++) arr2[i] = arr[i];

      return arr2;
    }
  }

  function _iterableToArray(iter) {
    if (Symbol.iterator in Object(iter) || Object.prototype.toString.call(iter) === "[object Arguments]") return Array.from(iter);
  }

  function _nonIterableSpread() {
    throw new TypeError("Invalid attempt to spread non-iterable instance");
  }

  var helloWithSpread = function helloWithSpread(name) {
    return "Hello ".concat(_toConsumableArray(name).join('-'));
  };

  return helloWithSpread;

}());
{% endhighlight %}




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

