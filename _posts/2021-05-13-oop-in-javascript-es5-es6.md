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

Phương thức trong hàm khởi tạo tốt hơn có thể được viết bằng javascript bằng cách viết nó dưới dạng một nguyên mẫu prototype như sau: 

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

Bây giờ, `Object Prototype` Nguyên mẫu Đối tượng là gì? Nguyên mẫu đối tượng là một đối tượng được liên kết với mọi phiên bản của đối tượng theo mặc định trong JavaScript. Nguyên mẫu cho phép bạn dễ dàng xác định các phương thức cho tất cả các trường hợp của một đối tượng cụ thể. Điều này rất hữu ích vì phương thức được áp dụng cho nguyên mẫu, vì vậy nó chỉ được lưu trữ trong bộ nhớ một lần, nhưng mọi thể hiện của đối tượng đều có quyền truy cập vào nó.

Chúng tôi cũng có thể thêm một thuộc tính vào đối tượng bằng cách sử dụng một nguyên mẫu, điều này không thể thực hiện được bình thường sau khi khai báo một hàm khởi tạo, nhưng nó chỉ nên được sử dụng cho các thuộc tính mà chúng tôi muốn tất cả các phiên bản chia sẻ:

```js
Dog.prototype.breed = 'German shepherd'
```

Điều gì sẽ xảy ra nếu chúng ta có một đối tượng khác mà chúng ta muốn có tất cả các thuộc tính và phương thức của đối tượng đầu tiên cũng như các thuộc tính và / hoặc phương thức đặc biệt của riêng chúng, chúng ta sẽ làm gì khi ghi nhớ DRY?

Câu trả lời cho điều đó được cung cấp bởi `prototypes inheritance`, đơn giản có nghĩa là một đối tượng kế thừa các thuộc tính và phương thức của đối tượng khác. ví dụ: chúng tôi muốn một nhóm dog khác kế thừa một số thuộc tính của nhóm đầu tiên cộng với các thuộc tính đặc biệt của chúng (dog weight):

```js
// Group 1
function GroupDog1(dogName, dogAge){
 // Properties
  this.dogName = dogName;
  this.dogAge = dogAge;
}

// Object Prototype
GroupDog1.prototype.canBark = function(){
  if(this.dogAge => '180 days'){
     return 'YES';
  } else{
    return 'NO';
  }
}

// Group 2
function GroupDog2(dogName, dogAge, dogWeight){
  GroupDog1.call(this, dogName, dogAge);
  this.dogWeight = dogWeight;
}
```

Để kế thừa các thuộc tính từ nhóm đầu tiên, chúng tôi đã sử dụng phương thức `call()` được sử dụng để gọi nhà thầu mà chúng tôi muốn kế thừa các thuộc tính của nó và nó lấy đây làm tham số đầu tiên và sau đó là các tham số sẽ được kế thừa từ phương thức khởi tạo đó (trong trường hợp này: - dogName và dogAge). Sau đó, chúng ta đặt thuộc tính đặc biệt của đối tượng (trong trường hợp này là: dogWeight)

Điều này chỉ kế thừa các thuộc tính chứ không phải nguyên mẫu. Để kế thừa các nguyên mẫu, chúng tôi sẽ nói:

```js
Group2.prototype = object.create(Group1.prototype);
```

Với điều này, chúng ta đã làm cho nhóm 2 những con chó sở hữu tất cả các tài sản và đồ vật của nhóm 1.


### Cú pháp ES6





### Releases
- ES1 - ECMAScript 1 (1997)
- ES2 - ECMAScript 2 (1998)
- ES3 - ECMAScript 3 (1999)
- ES4 - ECMAScript 4 (2008)
- ES5 - ECMAScript 5 (2009 - 2014)
- ES6 - ECMAScript 6 (2015 - 2018)


### Những trình duyệt nào được hỗ trợ?

http://kangax.github.io/compat-table/es5/

http://kangax.github.io/compat-table/es6/

-----
[Object-Oriented Programming in Javascript(ES5 & ES6) EXPLAINED.](https://dev.to/orighoprecious/object-oriented-programming-in-javascript-es5-es6-explained-4jbk)  
[https://www.w3schools.com/js/js_versions.asp](https://www.w3schools.com/js/js_versions.asp)  
[https://www.w3schools.com/js/js_history.asp](https://www.w3schools.com/js/js_history.asp)  
