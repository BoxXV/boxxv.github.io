---
layout: post
title: Module Javascript
subtitle: Hướng dẫn cho người mới
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

Nếu bạn là người mới học Javascript, những từ như "`module bundlers` với `module loaders`", "`Webpack` với `Browserify`" và "`AMD` với `CommonJS`" có thể nhanh chóng trở nên choáng ngợp.

Hệ thống module của Javascript có thể hơi đáng sợ, nhưng hiểu được nó là một điều quan trọng đối với lập trình viên web.

## A. Tại sao lại sử dụng module?
- Dễ bảo trì: Một module được thiết kế tốt nhắm tới việc làm giảm sự phụ thuộc của các phần trong codebase càng nhiều càng tốt để nó có thể phát triển một cách độc lập.
- Phân chia không gian tên: Chia sẻ các biến toàn cục giữa các đoạn code không liên quan là một việc rất tệ trong quá trình phát triển.
- Tính tái sử dụng: Sẽ không dễ dàng hơn sao nếu có một module mà chúng ta có thể dùng đi dùng lại?

### 1. Mẫu module - The Module pattern

Mẫu module được sử dụng để bắt chước khái niệm class (do bản thân Javascript không hỗ trợ class) để chúng ta có thể lưu trữ cả các phương thức và biến public và private trong một đối tượng độc lập - tương tự cách class được sử dụng trong các ngôn ngữ lập trình khác như Java hay Python. Điều đó cho phép chúng ta tạo ra một API public cho các phương thức chúng ta muốn để lộ ra ngoài, trong khi vẫn đóng gói các biến và phương thức private trong một closure scope.

Có một vài cách để đạt được mẫu module.
- Closure vô danh
- Import toàn cục
- Object interface
- Mẫu revealing module

#### 1a. Closure vô danh
```javascript
(function () {
  // We keep these variables private inside this closure scope

  var myGrades = [93, 95, 88, 0, 55, 91];

  var average = function() {
    var total = myGrades.reduce(function(accumulator, item) {
      return accumulator + item}, 0);

      return 'Your average grade is ' + total / myGrades.length + '.';
  }

  var failing = function(){
    var failingGrades = myGrades.filter(function(item) {
      return item < 70;});

    return 'You failed ' + failingGrades.length + ' times.';
  }

  console.log(failing());

}());

// ‘You failed 2 times.’
```

Với cấu trúc này, hàm vô danh của chúng ta có không gian tính toán của riêng nó hay "closure", và sau đó chúng ta thực thi nó ngay lập tức. Điều này giúp chúng ta giấu các biến khỏi không gian tên cha (toàn cục).

Chú ý rằng cặp ngoặc bao quanh hàm vô danh là bắt buộc, vì các lệnh bắt đầu với từ khóa function luôn được coi là khai báo hàm (nhớ rằng, bạn không thể khai báo một hàm không có tên trong Javascript). Do vậy, cặp ngoặc bao quanh tạo ra một biểu thức hàm thay vào đó. Nếu bạn tò mò, bạn có thể đọc thêm [ở đây](https://stackoverflow.com/questions/1634268/explain-the-encapsulated-anonymous-function-syntax).

#### 1b. Import toàn cục

Một cách phổ biến khác được sử dụng bởi những thư viện như jQuery là import toàn cục. Cách này tương tự với closure vô danh như ta đã thấy, ngoại trừ việc chúng ta truyền biến toàn cục vào như một tham số:

```javascript
(function (globalVariable) {

  // Keep this variables private inside this closure scope
  var privateFunction = function() {
    console.log('Shhhh, this is private!');
  }

  // Expose the below methods via the globalVariable interface while
  // hiding the implementation of the method within the
  // function() block

}(globalVariable));
```

Trong ví dụ này, globalVariable là biến toàn cục duy nhất. Lợi ích của phương pháp này so với closure vô danh là bạn khai báo một biến toàn cục trước, giúp mọi người dễ đọc code của bạn hơn.

#### 1c. Object interface

```javascript
var myGradesCalculate = (function () {

  // Keep this variable private inside this closure scope
  var myGrades = [93, 95, 88, 0, 55, 91];

  // Expose these functions via an interface while hiding
  // the implementation of the module within the function() block

  return {
    average: function() {
      var total = myGrades.reduce(function(accumulator, item) {
        return accumulator + item;
        }, 0);

      return 'Your average grade is ' + total / myGrades.length + '.';
    },

    failing: function() {
      var failingGrades = myGrades.filter(function(item) {
          return item < 70;
        });

      return <You failed < + failingGrades.length + times.;
    }
  }
})();

myGradesCalculate.failing(); // <You failed 2 times.
myGradesCalculate.average(); // 'Your average grade is 70.33333333333333.'
```


### 2. CommonJS và AMD

#### 2a. CommonJS
CommonJS là một nhóm tiên phong thiết kế và triển khai Javascript API để khai báo module.

Một module CommonJS có bản chất là một nhóm code Javascript có thể tái sử dụng mà chỉ xuất ra các object riêng biệt, khiến chúng sẵn có để các module khác require. Nếu bạn đã lập trình Node.js, bạn sẽ rất quen với định dạng này.

Với CommonJS, mỗi file Javascript chứa các module trong module context độc nhất của chúng (giống như gói chúng trong một closure). Trong scope này, chúng ta sử dụng đối tượng module.exports để lộ ra các module, và require để import chúng.

```javascript
function myModule() {
  this.hello = function() {
    return <hello!<;
  }
}

module.exports = myModule;
```

Có 2 lợi ích rõ ràng của phương pháp này so với mẫu module mà chúng ta đã thảo luận ở trước:
- Tránh ô nhiễm không gian tên toàn cục.
- Làm cho sự phụ thuộc trở nên rõ ràng.

Một chú ý nữa là CommonJS hướng tới `phía server` và nạp các module một cách đồng bộ. Điều này ảnh hưởng vì nếu chúng ta có 3 module cần require, nó sẽ nạp từng cái một.

Nó hoạt động tốt trên server nhưng không may là nó khiến cho việc viết Javascript cho phía trình duyệt trở nên khó khăn hơn. Việc đọc module từ web mất rất nhiều thời gian hơn so với việc đọc từ đĩa. Chừng nào việc nạp các module còn chạy, trình duyệt sẽ bị ngưng chạy bất cứ thứ gì khác cho đến khi kết thúc nạp. Trình duyệt hoạt động như vậy vì luồng Javascript ngừng cho đến khi code đã nạp xong. (Tôi sẽ nói tới cách giải quyết vấn đề này ở phần 2 khi chúng ta thảo luận đến việc đóng gói module. Hiện tại, đó là tất cả những gì chúng ta cần biết).

#### 2b. AMD

CommonJS rất tốt, nhưng nếu chúng ta muốn nạp các module một cách bất đồng bộ thì sao? Câu trả lời là thứ gọi là `Asynchronous Module Definition`, hay ngắn gọn là AMD.

```javascript
define([<myModule<, <myOtherModule<], function(myModule, myOtherModule) {
  console.log(myModule.hello());
});
```

Thứ diễn ra ở đây là hàm define nhận tham số đầu tiên của nó là một mảng chứa các phụ thuộc của module hiện tại. Các phụ thuộc này được nạp ở background (theo cách non-blocking), và khi đã nạp xong hàm define sẽ gọi hàm callback được chỉ định.

Kế tiếp, hàm callback nhận các tham số là các phụ thuộc đã được nạp - trong trường hợp của chúng ta là myModule và myOtherModule - và hàm này được phép sử dụng các phụ thuộc này. Cuối cùng, bản thân các phụ thuộc cũng phải được khai báo bằng cách dùng từ khóa define.

```javascript
define([], function() {

  return {
    hello: function() {
      console.log(<hello<);
    }
  };
});
```

Một lần nữa, không giống như CommonJS, AMD hướng tới phía `trình duyệt` và sử dụng bất đồng bộ để hoàn thành công việc. (Chú ý, có rất nhiều người tin rằng việc nạp các tệp theo từng phần khi bắt đầu chạy code là không tốt, chúng ta sẽ khám phá thêm khi đến phần xây dựng module).

Bên cạnh tính bất đồng bộ, một lợi ích khác của AMD là module của bạn có thể là object, hàm, constructor, string, JSON và rất nhiều kiểu khác, trong khi CommonJS chỉ hỗ trợ object.

AMD không tương thích với io, filesystem và các tính năng hướng server như CommonJS, và cú pháp hàm đóng gói có chút rườm ra so với một lệnh require đơn giản.

### 3. UMD

Với các dự án yêu cầu bạn hỗ trợ cả AMD và CommonJS, sẽ có một định dạng khác là: `Universal Module Definition` (UMD).

Về cơ bản UMD tạo ra một cách sử dụng một trong hai cách trên, trong khi vẫn hỗ trợ định nghĩa biến toàn cục. Kết quả là module UMD có thể hoạt động trên cả client và server.

```javascript
(function (root, factory) {
  if (typeof define === <function< && define.amd) {
      // AMD
    define([<myModule<, <myOtherModule<], factory);
  } else if (typeof exports === <object<) {
      // CommonJS
    module.exports = factory(require(<myModule<), require(<myOtherModule<));
  } else {
    // Browser globals (Note: root is window)
    root.returnExports = factory(root.myModule, root.myOtherModule);
  }
}(this, function (myModule, myOtherModule) {
  // Methods
  function notHelloOrGoodbye(){}; // A private method
  function hello(){}; // A public method because it<s returned (see below)
  function goodbye(){}; // A public method because it<s returned (see below)

  // Exposed public methods
  return {
      hello: hello,
      goodbye: goodbye
  }
}));
```

Để xem nhiều ví dụ hơn về định dạng UMD, hãy xem repo hướng dẫn này trên GitHub: [https://github.com/umdjs/umd](https://github.com/umdjs/umd).

### 4. Native JS

Như bạn có thể đã nhận thấy, không một module nào phía trên là tự nhiên đối với Javascript. Chúng ta tạo ra các cách để giả lập một hệ thống module bằng cách sử dụng mẫu module, CommonJS hay AMD.

ES6 cung cấp rất nhiều cách import và export module mà những người khác đã giải thích rất tốt - dưới đây là một số tài nguyên trong số đó:
    jsmodules.io
    [exploringjs.com](https://exploringjs.com/es6/ch_modules.html)

Điều tuyệt vời về module ES6 liên quan đến CommonJS và AMD là cách nó quản lý để đạt tới những thứ tốt nhất của cả 2: chặt chẽ và cú pháp biểu đạt và nạp bất đồng bộ, cộng thêm các lợi ích như hỗ trợ tốt hơn các các phụ thuộc lặp vòng.

```javascript
// lib/counter.js

var counter = 1;

function increment() {
  counter++;
}

function decrement() {
  counter--;
}

module.exports = {
  counter: counter,
  increment: increment,
  decrement: decrement
};
```

```javascript
// src/main.js

var counter = require('../../lib/counter');

counter.increment();
console.log(counter.counter); // 1
```

Mặt khác, ES6 tạo ra một tham chiếu chỉ đọc hoạt động thực sự của module mà ta import:
```javascript
// lib/counter.js
export let counter = 1;

export function increment() {
  counter++;
}

export function decrement() {
  counter--;
}
```

```javascript
// src/main.js
import * as counter from '../../counter';

console.log(counter.counter); // 1
counter.increment();
console.log(counter.counter); // 2
```


## B. Đóng gói module

Để giải quyết vấn đề thời gian chờ tải trang, chúng ta đóng gói, hay "ghép" tất cả các file của mình thành một file lớn (hay một vài file nếu cần) để giảm số lượng request. Khi bạn nghe các lập trình viên nói về `"build step"` hay `"build process"`, thì đây là điều mà họ nói đến.

Nếu bạn tuân theo các hệ thống module không tự nhiên mà trình duyệt không thể thông dịch như CommonJS hay AMD (hay thậm chí là dạng module tự nhiên ES6), bạn sẽ cần đến một công cụ chuyên dùng để chuyển đổi các module của mình thành những đoạn code đúng thứ tự và hoạt động được với trình duyệt. Đó là lúc mà `Browserify`, `RequireJS`, `Webpack` và các "chương trình đóng gói module" `module bundlers` hay "chương trình nạp module" `module loaders` được dùng đến.

Ngoài việc đóng gói và/hoặc nạp các module của bạn, các chương trình đóng gói module còn cung cấp một đống các tính năng đi kèm như tự biên dịch ngược code khi bạn thay đổi hay sinh source map để debug.


### Đóng gói CommonJS bằng Browserify

CommonJS nạp các module một cách đồng bộ, điều này ổn ngoại trừ việc nó không tốt đối với trình duyệt. Tôi đã nói rằng có một cách giải quyết - đó là việc sử dụng một chương trình đóng gói tên là `Browserify`. Browserify là một công cụ biên dịch các module CommonJS cho trình duyệt.

Browserify thực hiện việc này bằng cách phân tích AST với mỗi lời gọi require để đi qua toàn bộ đồ thị phụ thuộc trong dự án của bạn. Một khi nó tìm ra cấu trúc của các phụ thuộc, nó sẽ đóng gói chúng theo đúng thứ tự vào một file duy nhất. Đến lúc này, tất cả những việc bạn cần làm là thêm một thẻ <script> dành cho file "bundle.js" của bạn vào file html để đảm bảo rằng tất cả mã nguồn của bạn được tải trong một HTTP request.

Sản phẩm cuối cùng: các file được đống gói đã được chuẩn bị và sẵn sàng cho các công cụ như Minify-JS để làm nhỏ code đã được đóng gói.

### Đóng gói AMD

Nếu bạn dùng AMD, bạn sẽ muốn sử dụng một chương trình nạp AMD như `RequireJS` hay `Curl`. Một chương trình nạp module (khác với một chương trình đóng gói) nạp các module mà chương trình của bạn cần để chạy một cách động.

Nhắc lại rằng, một trong những điểm khác biệt chính của AMD so với CommonJS là nó nạp các module một cách bất đồng bộ. Trong trường hợp này, với AMD, bạn không thực sự cần bước đóng gói các module của mình thành một file do bạn nạp các module một cách bất đồng bộ - nghĩa là bạn dần dần tải các file cần thiết để chạy chương trình thay vì tải toàn bộ các file cùng một lúc khi người dùng lần đầu tiên ghé thăm trang của bạn.

Tuy nhiên trên thực tế, chi phí của những request khối lượng lớn theo thời gian với mỗi hành động của người dùng không có nhiều ý nghĩa ở production. Hầu hết các lập trình viên web vẫn sử dụng công cụ để đóng gói và làm nhỏ các module AMD của họ để tối ưu hiệu năng với các công cụ như chương trình tối ưu hóa RequireJS, `r.js`.

Tóm lại, sự khác biệt giữa AMD và CommonJS khi đóng gói là: trong quá trình phát triển, các ứng dụng AMD có thể tránh được build step. Khi bạn cho code chạy thật, các công cụ tối ưu hóa như r.js có thể xử lý việc đó.

### Webpack

Các chương trình đóng gói đã đi một chặng đường dài, còn Webpack thì chỉ là lính mới. Nó được thiết kế để không phân biệt hệ thống module mà bạn sử dụng, cho phép lập trình viên dùng CommonJS, AMD hay ES6 theo nhu cầu.

Bạn có thể tự hỏi rằng tại sao chúng ta cần Webpack khi mà đã có các chương trình đóng gói như Browserify và RequireJS làm được việc và làm rất tốt. Chà, Webpack cung cấp một số tính năng hữu ích như "phân tách code" - một cách chia code của bạn thành nhiều "mảnh" được tải theo nhu cầu.

Ví dụ, nếu bạn có một ứng dụng web với nhiều khối code chỉ cần ở những hoàn cảnh nhất định, việc đưa toàn bộ code vào một file được đóng gói lớn sẽ trở nên không hiệu quả. Trong trường hợp này, bạn có thể sử dụng tính năng phân tách code để trích xuất code thành nhiều mảnh đóng gói được tải khi cần, tránh rắc rối với việc tải một lượng lớn code trong khi hầu hết người dùng chỉ cần phần lõi của ứng dụng.

Việc chia tách code chỉ là một trong rất nhiều tính năng hấp dẫn mà Webpack cung cấp, và trên mạng có rất nhiều quan điểm mạnh mẽ về việc đánh giá xem Webpack hay Browserify tốt hơn. Dưới đây chỉ là một ít trong số những thảo luận ở trình độ cao mà tôi thấy hữu ích khi xem xét vấn đề này:

    https://gist.github.com/substack/68f8d502be42d5cd4942
    http://mattdesl.svbtle.com/browserify-vs-webpack
    http://blog.namangoel.com/browserify-vs-webpack-js-drama

### Module ES6

Sự khác biệt quan trọng nhất giữa các định dạng module JS hiện tại (CommonJS, AMD) và module ES6 là module ES6 được thiết kế với ý tưởng phân tích tĩnh. Nghĩa là khi bạn import các module, việc import được thực hiện lúc biên dịch - trước khi script bắt đầu chạy. Điều này cho phép chúng ta loại bỏ các phần export không được dùng bởi các module khác trước khi chúng ta chạy chương trình. Loại bỏ các phần export không cần thiết giúp giảm rất nhiều không gian cần để lưu trữ và giảm tải ở phía trình duyệt.

Điều khiến module ES6 khác là sự khác biệt ở cách loại bỏ code dư thừa của nó, được gọi là "tree shaking". Tree shaking cơ bản là ngược lại của sự loại bỏ code dư thừa. Module ES6 chỉ include code mà phiên bản code đóng gói cần để chạy thay vì loại bỏ code mà phiên bản đóng gói không cần đến.

### Build module ES6

Module ES6 vẫn cần phải được xử lý thêm, do vẫn chưa có triển khai chính thức của cách nạp module ES6 trên trình duyệt

Dưới đây là một số tùy chọn cho việc build/chuyển đổi module ES6 để có thể hoạt động trên trình duyệt, cách #1 là cách phổ biến nhất ở thời điểm hiện tại:

1. Dùng một chương trình dịch (như Babel hay Traceur) để dịch code ES6 thành ES5 dưới định dạng CommonJS, AMD hay UMD. Sau đó đưa code được dịch vào một chương trình đóng gói như Browserify hay Webpack để tạo một hay nhiều file đóng gói.
2. Dùng Rollup.js, thứ rất tương đồng với tùy chọn #1 ở trên ngoại trừ việc Rollup mang theo sức mạnh của module ES6 trong việc phân tích tĩnh code ES6 và các phụ thuộc trước khi đóng gói. Nó sử dụng "tree shaking" để include lượng code ít nhất vào code đóng gói. Tóm lại, lợi ích chính của Rollup.js so với Browserify hay Webpack khi bạn dùng module ES6 là tree shaking sẽ giúp code đóng gói của bạn nhỏ hơn. Cảnh báo rằng Rollup cung cấp một vài định dạng để đóng gói code, bao gồm ES6, CommonJS, AMD, UMD hay IIFE. Code đóng gói dưới dạng IIFE và UMD cso thể hoạt động trên trình duyệt, nhưng nếu bạn chọn đóng gói theo định dạng AMD, CommonJS hay ES6 thì bạn cần thêm một bước chuyển đổi code sang một định dạng mà trình duyệt có thể hiểu được (ví dụ như sử dụng Browserify, Webpack, RequireJS, v..v..).


-----
Tham khảo:
- [JavaScript Modules: A Beginner’s Guide](https://www.freecodecamp.org/news/javascript-modules-a-beginner-s-guide-783f7d7a5fcc/)
- [JavaScript Modules Part 2: Module Bundling](https://www.freecodecamp.org/news/javascript-modules-part-2-module-bundling-5020383cf306/)
- [JavaScript modules](https://viblo.asia/p/javascript-modules-3P0lPEMn5ox)
- [JS Modules - Bao nhiêu kiểu khai báo, làm sao nhớ hết?](https://viblo.asia/p/js-modules-bao-nhieu-kieu-khai-bao-lam-sao-nho-het-gGJ59AY15X2)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://viblo.asia/p/su-dung-requirejs-va-amd-de-module-hoa-code-javascript-znVGLY6jvZOe)
- [Sử dụng RequireJS và AMD để module hóa code JavaScript](https://manhhomienbienthuy.github.io/2016/05/12/su-dung-amd-requirejs-de-module-hoa-javascript.html)

-----
[CommonJS](https://viblo.asia/tags/commonjs)
- [Tìm hiểu về module system, CommonJS và require](https://viblo.asia/p/tim-hieu-ve-module-system-commonjs-va-require-QpmleL3mZrd)
- [Promises, Classes, ES6 Modules and CommonJS](https://viblo.asia/p/javascript-promises-classes-es6-modules-and-commonjs-07LKX48DKV4)
- [Module Javascript: Hướng dẫn cho người mới](https://viblo.asia/p/module-javascript-huong-dan-cho-nguoi-moi-OeVKBgVMZkW)
- [Module Javascript phần 2: Đóng gói module](https://viblo.asia/p/module-javascript-phan-2-dong-goi-module-GrLZDVve5k0)

Grunt, Flux, Parcel, RequireJS/AMD, Browserify

