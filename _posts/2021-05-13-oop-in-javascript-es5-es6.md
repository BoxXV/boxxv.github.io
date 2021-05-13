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




### Cú pháp ES6



```js
<my-component>

  <!-- layout -->
  <h1>{ props.message }</h1>
  <ul>
    <li>Learn Riot.js</li>
    <li>Build something cool</li>
  </ul>

  <script>
    export default {
      onMounted() {
        const title = this.$('h1') // single element
        const items = this.$$('li') // multiple elements
      }
    }
  </script>

  <style>
    /** other component specific styles **/
    h1 { font-size: 120% }
    /** other component specific styles **/
  </style>

</my-component>
```

### Releases
- v5.3.0  - Feb 13, 2021
- v4.14.0 - Sep 01, 2020
- v3.13.2 - Nov 25, 2018
- v2.6.9  - Feb 15, 2019
- v1.0.4  - Sep 17, 2014


### Những trình duyệt nào được hỗ trợ?

Riot.js 4 hỗ trợ tất cả các trình duyệt hiện đại chính. Các trình duyệt như IE11 không được hỗ trợ: nếu bạn cần hỗ trợ các trình duyệt cũ hơn, bạn có thể cân nhắc sử dụng phiên bản Riot cũ hơn

-----

[https://github.com/riot/riot](https://github.com/riot/riot)  
[https://github.com/riot/examples](https://github.com/riot/examples)  