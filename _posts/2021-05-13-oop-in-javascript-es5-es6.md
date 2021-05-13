---
layout: post
title: Object-Oriented Programming in Javascript(ES5 & ES6) EXPLAINED
subtitle: Lập trình hướng đối tượng với ES5 và ES6
image: "img/projects-bg.jpg"
---

Nói chung, OOP - Lập trình hướng đối tượng rất hữu ích. Nó giúp các nhà phát triển mô hình hóa những thứ trong thế giới thực mà chúng tôi muốn thể hiện bên trong mã của mình và / hoặc cung cấp một cách đơn giản để truy cập vào chức năng mà nếu không sẽ khó hoặc không thể sử dụng được.

Hiểu đầy đủ về cách OOP hoạt động trong javascript là một chút khó khăn, đặc biệt là trong cú pháp ES5, lớp ES6 đã làm cho việc sử dụng hàm tạo đối tượng dễ dàng hơn rất nhiều nhưng với tư cách là nhà phát triển, chúng tôi sẽ gặp phải mã nguyên mẫu đối tượng ES5 trong quá trình của chúng tôi và trong trường hợp bạn làm không biết, lớp ES6, hoạt động như nguyên mẫu đối tượng dưới mui xe.

Bài viết này sẽ giải thích object  javascript trong cú pháp ES5 và ES6. Hãy theo dõi!

### Cú pháp ES5

`Prototype` Nguyên mẫu và Kế thừa nguyên mẫu:
Chúng ta đã xem xét cách thức tạo đối tượng được viết theo cú pháp ES5, bây giờ hãy xem nguyên mẫu đối tượng là gì. Cú pháp:

```js
function Dog(name, age){
  // Properties
  this.name = name;
  this.age = age;

  // Method
  this.canBark = function(){
    if(this.age => '180 days'){
       return 'YES';
    } else{
      return 'NO';
    }
  }
}
```

Phương thức trong hàm khởi tạo tốt hơn có thể được viết bằng javascript bằng cách viết nó dưới dạng một nguyên mẫu như sau: 

```js
function Dog(name, age){
  // Properties
  this.name = name;
  this.age = age;
}

  // Object Prototype
Dog.prototype.canBark = function(){
  if(this.age => '180 days'){
     return 'YES';
  } else{
    return 'NO';
  }
}
```



### Cú pháp ES6





### Releases
- ES1 - ECMAScript 1 (1997)
- ES2 - ECMAScript 2 (1998)
- ES3 - ECMAScript 3 (1999)
- ES4 - ECMAScript 4
- ES5 - ECMAScript 5 (2009)
- ES6 - ECMAScript 2015, ECMAScript 2016, ECMAScript 2017, ECMAScript 2018


### Những trình duyệt nào được hỗ trợ?

http://kangax.github.io/compat-table/es5/

http://kangax.github.io/compat-table/es6/

-----
[Object-Oriented Programming in Javascript(ES5 & ES6) EXPLAINED.](https://dev.to/orighoprecious/object-oriented-programming-in-javascript-es5-es6-explained-4jbk)  
