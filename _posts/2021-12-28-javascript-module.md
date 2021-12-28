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

#### 2b. AMD

### 3. UMD

### 4. Native JS


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

