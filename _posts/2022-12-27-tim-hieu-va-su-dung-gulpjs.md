---
layout: post
title: Tìm hiểu và sử dụng Gulp JS
subtitle: Building với Gulp
image: "img/projects-bg.jpg"
tags:
- Gulp
- GulpJs
- Building
---

![Gulp](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Gulp.jpg "Gulp")

Tối ưu hóa tài sản trang web và thử nghiệm thiết kế trên nhiều trình duyệt khác nhau chắc chắn không phải là một phần thú vị nhất của quá trình thiết kế. Công việc trên gồm các nhiệm vụ lặp đi lặp lại, rất nhàm chán và thiếu tính hiệu quả. May mắn thay, ta có thể dùng các công cụ để giải quyết công việc mang tính lặp đi lặp lại này nhằm tăng hiệu suất công việc. Gulp là một công cụ như thế.

## 1. Gulp là gì?

> `Gulp` là một build system, có nghĩa là bạn có thể sử dụng nó để tự động hóa các công việc thông thường trong quá trình phát triển Website. Nó được xây dựng trên nền Node.js, và cả Gulp source hay Gulp files nơi bạn định nghĩa các task được viết bằng Javascript (hoặc CoffeeScript). Nếu bạn là một front-end developer thì Gulp gần như trở thành một build system hoàn hảo. Bạn có thể viết các tasks cho việc phân tích cú pháp và tự động biên dịch khi các tập tin được chỉ định có sự thay đổi.

`Gulp` là một bộ công cụ JavaScript được dùng như là một trình chạy task, được dựng như là một hệ thống xây dựng trong phát triển web. Biên dịch, thu gọn code, minify CSS, tự động compile lại file (js, css) khi có thay đổi, compile SASS/LESS, tối ưu hình ảnh, unit testing linting là những task lập lại nên được tự động hoá. Gulp giúp quá trình viết task dễ dàng hơn, thậm chí cho những người ít kinh nghiệm với JavaScript.

Gulp sử dụng pipeline để dẫn data từ một plugin sang một plugin khác, và kết quả sau cùng là xuất ra một thư mục đã được chỉ định trước. `Gulp` thực hiện công việc tốt hơn so với `Grunt` bởi vì nó không tạo ra file tạm thời để lưu trữ các kết quả, nó cho kết quả có ít lần gọi I/O hơn.

Bản thân Gulp thì không thực hiện gì nhiều, nhưng với một lượng lớn pulgin có sẵn mà bạn có thể dễ dàng tìm kiếm trên các trang pulgin hoặc tìm với từ khóa `gulpplugin` ngay trên NPM. Ví dụ, các plugins để chạy `JSHint`, biên dịch CoffeeScript, chạy Mocha Tests hay thậm chí cập nhật số phiên bản của bạn.

## 2. Các thành phần chính của Gulp

Để chạy được gulp cần một file gulpfile.js trong đó có chứa các thành phần chính là: `gulp.task`, `gulp.src`, `gulp.dest`, `gulp.watch`

### 2.1. gulp.task

Gulp.task đơn giản là các task mà các bạn muốn thực thi, nó có ý nghĩa như 1 function vậy.

```js
gulp.task('task_one', function(){
    // nhiệm vụ
})
```

Bạn cũng có thể bỏ qua task bất kì nếu bạn chỉ muốn chạy một vài các task cần thiết:

```js
gulp.task ('build', ['array', 'of', 'task', 'names']);
```

**Lưu ý:**
1. Các task sẽ chạy song song (tất cả cùng một lúc) chứ không phải các task sẽ chạy theo thứ tự nhé.
2. Mặc định khi chạy lệnh gulp trong command line không kèm theo tham số nào, gulp sẽ tự động chạy task mặc định là default. Khi muốn chạy một task cụ thể nào đó, bạn chỉ cần dùng lệnh:

```js
gulp task_name
```

### 2.2. gulp.src

### 2.3. gulp.dest

### 2.4. gulp.watch


## 3. Cách cài đặt





-----
Tham khảo:

- [Building với Gulp](https://viblo.asia/p/building-voi-gulp-n157G5KBRAje)
- [Tìm hiểu và sử dụng Gulp JS](https://viblo.asia/p/tim-hieu-va-su-dung-gulp-js-aWj53OVo56m)