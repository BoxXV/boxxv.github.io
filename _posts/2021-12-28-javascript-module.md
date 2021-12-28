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

### Tại sao lại sử dụng module?
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

var counter = require(<../../lib/counter<);

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

-----
Tham khảo:
- [JavaScript Modules: A Beginner’s Guide](https://www.freecodecamp.org/news/javascript-modules-a-beginner-s-guide-783f7d7a5fcc/)
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

