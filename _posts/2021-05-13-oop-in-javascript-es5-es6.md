---
layout: post
title: Object-Oriented Programming in Javascript(ES5 & ES6) EXPLAINED
subtitle: Lập trình hướng đối tượng với ES5 và ES6
image: "img/projects-bg.jpg"
---



### Một số tính năng

- Riot.Js cho phép người dùng áp dụng các thẻ HTML tùy chỉnh trên tất cả các trang và ứng dụng web. Bạn cũng có thể sử dụng lại các thẻ đó.
- Framework này tương tự như polymer và Reac.js. Tuy nhiên, so với hai framework kia, Riot.Js có tổ chức và nhỏ gọn hơn.
- Framekwork này tập trung cao độ vào các chức năng vi mô cho phép bạn làm việc cá nhân với các ứng dụng khác nhau cùng một lúc.


### Sample code

index.html
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Riot App</title>
</head>
<body>
  <!-- place the custom component anywhere inside the body -->
  <my-component></my-component>

  <!-- include riot.js -->
  <script src="riot.min.js"></script>
  <script src="my-component.js"></script>
  <script>
    riot.compile().then(function() {
      riot.mount('my-component', { message: 'Hello world!' })
    })
  </script>
</body>
</html>
```

my-component.riot
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

### Syntax - Cú pháp

Riot component  là sự kết hợp layout của HTML và logic của JavaScript. Dưới đây là các quy tắc cơ bản: 
- Mỗi tệp `.riot` chỉ có thể chứa logic cho một component duy nhất
- HTML được định nghĩa đầu tiên và logic được bao bọc bên trong thẻ `<script>`
- Các component tùy chỉnh có thể để trống, chỉ có HTML hoặc chỉ có JavaScript 



### Lifecycle
```js
<my-component>
  <script>
    export default {
      onBeforeMount(props, state) {
        // before the component is mounted
      },
      onMounted(props, state) {
        // right after the component is mounted on the page
      },
      onBeforeUpdate(props, state) {
        // allows recalculation of context data before the update
      },
      onUpdated(props, state) {
        // right after the component template is updated after an update call
      },
      onBeforeUnmount(props, state) {
        // before the component is removed
      },
      onUnmounted(props, state) {
        // when the component is removed from the page
      }
    }
  </script>
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