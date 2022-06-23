---
layout: post
title: Cách angular-cli/webpack cấp các CSS của bạn cho client
subtitle: How angular-cli/webpack delivers your CSS styles to the client

tags:
- angular
- webpack
- css
- node
---

![angular](https://boxxv.github.io/img/posts/1_h9J7BAvjmdyBmyXnvytHDg.png "webpack")

Bạn đã bao giờ tự hỏi làm thế nào để có thể nhập CSS vào các tệp JavaScript? Trong bài viết này, tôi sẽ chỉ cho bạn cách Webpack thực hiện điều đó bằng cách chuyển đổi các kiểu CSS của bạn thành JavaScript.

Khi bạn tạo một dự án Angular mới và chạy `ng new myapp`, bạn sẽ có cấu trúc dự án sau:

```bat
src
├─ app
├─ assets
├─ index.html
├─ styles.css
└─ ...
```

Điều khiến chúng tôi quan tâm ở đây là tệp `styles.css` được cho là được sử dụng để khai báo các kiểu toàn cục. Bạn có thể viết trực tiếp các kiểu trong tệp này hoặc nhập bằng cách [imports CSS cụ thể](https://developer.mozilla.org/en-US/docs/Web/CSS/@import). Nếu bạn đặt những thứ sau vào `index.html`:

```html
<body>
    <header>
        <span>I am header span</span>
    </header>
    <span>I am regular span outside of header</span>
</body>
```

Và thêm các kiểu sau vào `styles.css`
```css
@import "header.css";

span {
    color: green;
}
```

và tới `header.css`:
```css
header span {
    color: blue;
}
```

Bạn sẽ thấy bản trình bày sau khi chạy ứng dụng:

![angular](https://boxxv.github.io/img/posts/image-42.png "webpack")

Điều này được mong đợi nhưng câu hỏi thực sự là `Angular-CLI` thực hiện nó như thế nào? Trên thực tế, các styles được đóng gói và giao cho client bằng webpack. Angular-CLI sử dụng webpack và chỉ cấu hình nó.

Trong bài viết này, tôi sẽ trình bày từng bước cách thực hiện bằng cách sử dụng webpack. Thông tin được trình bày ở đây sẽ hữu ích cho bất kỳ ai sử dụng webpack, không chỉ Angular-CLI.


### Cài đặt





-----
Tham khảo:
- [This is how angular-cli/webpack delivers your CSS styles to the client](https://indepth.dev/posts/1176/this-is-how-angular-cli-webpack-delivers-your-css-styles-to-the-client)