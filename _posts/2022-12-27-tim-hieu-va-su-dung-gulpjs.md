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

Tối ưu hóa tài sản trang web và thử nghiệm thiết kế trên nhiều trình duyệt khác nhau chắc chắn không phải là một phần thú vị nhất của quá trình thiết kế. Công việc trên gồm các nhiệm vụ lặp đi lặp lại, rất nhàm chán và thiếu tính hiệu quả. May mắn thay, ta có thể dùng các công cụ để giải quyết công việc mang tính lặp đi lặp lại này nhằm tăng hiệu suất công việc. Gulp là một công cụ như thế. Nó thường được sử dụng để làm các tác vụ front end như:
- Tạo ra một web server
- Reload trình duyệt một cách tự động bất cứ khi nào một file được lưu
- Sử dụng các preprocessor giống như Sass hoặc LESS
- Tối ưu hóa các tài nguyên như CSS, JavaScript và hình ảnh

## 1. Gulp là gì?

> `Gulp` là một build system, có nghĩa là bạn có thể sử dụng nó để tự động hóa các công việc thông thường trong quá trình phát triển Website. Nó được xây dựng trên nền Node.js, và cả Gulp source hay Gulp files nơi bạn định nghĩa các task được viết bằng Javascript (hoặc CoffeeScript). Nếu bạn là một front-end developer thì Gulp gần như trở thành một build system hoàn hảo. Bạn có thể viết các tasks cho việc phân tích cú pháp và tự động biên dịch khi các tập tin được chỉ định có sự thay đổi.

`Gulp` là một bộ công cụ JavaScript được dùng như là một trình chạy task, được dựng như là một hệ thống xây dựng trong phát triển web. Biên dịch, thu gọn code, minify CSS, tự động compile lại file (js, css) khi có thay đổi, compile SASS/LESS, tối ưu hình ảnh, unit testing linting là những task lập lại nên được tự động hoá. Gulp giúp quá trình viết task dễ dàng hơn, thậm chí cho những người ít kinh nghiệm với JavaScript.

Gulp sử dụng nguyên tắc `convention over configuration` hay `code over configuration` trong quá trình setup dự án. Với nguyên tắc này thì những vấn đề cụ thể trong lập trình như tổ chức cấu trúc thư mục như thế nào, đặt các tập tin css hay javascript ở đâu... được chuẩn hoá trước khi bất cứ một tập tin, thư mục nào được tạo ra hay đoạn code nào được viết ra. Điều này giúp giảm số lượng các quyết định mà lập trình viên phải đưa ra và giúp cho việc maintain dự án trở nên dễ dàng. Dưới đây là một ví dụ về cách tổ chức một thư mục dự án đặc trưng để có thể sử dụng Gulp.js một cách dễ dàng:

```no-highlight
|- app/
    |- css/
    |- fonts/
    |- images/ 
    |- index.html
    |- js/ 
    |- scss/
|- dist/
|- gulpfile.js
|- node_modules/
|- package.json
```

Gulp sử dụng pipeline để dẫn data từ một plugin sang một plugin khác, và kết quả sau cùng là xuất ra một thư mục đã được chỉ định trước. `Gulp` thực hiện công việc tốt hơn so với `Grunt` bởi vì nó không tạo ra file tạm thời để lưu trữ các kết quả, nó cho kết quả có ít lần gọi I/O hơn.

Bản thân Gulp thì không thực hiện gì nhiều, nhưng với một lượng lớn pulgin có sẵn mà bạn có thể dễ dàng tìm kiếm trên các trang pulgin hoặc tìm với từ khóa `gulpplugin` ngay trên NPM. Ví dụ, các plugins để chạy `JSHint`, biên dịch CoffeeScript, chạy Mocha Tests hay thậm chí cập nhật số phiên bản của bạn.

## 2. Cách cài đặt

Việc cài đặt Gulp tương đối dễ dàng. Nếu bạn chưa cài Node.js, bạn cần cài Node.js theo hướng dẫn có trên trang chủ của [NodeJs](https://nodejs.org/en/).

Sau khi đã cài đặt Node, bạn có thể cài đặt Gulp bằng cách sử dụng lệnh sau:

```bat
npm install -g gulp
hoặc
sudo npm install --global gulp
```

Chú ý:
- chỉ những người sử dụng Mac mới cần sử dụng từ khóa `sudo`
- **npm install** là lệnh sử dụng Node Package Manager (npm) để cài đặt Gulp trên máy tính của bạn.
- Ở trên chúng ta sử dụng option -g (viết tắt của globally) để thực hiện việc cài đặt toàn cục Gulp trên máy tính.

Tiếp tục di chuyển vào project và install gulp bằng lệnh:

```bat
npm install --save-dev gulp
```

- `npm i` là lệnh sử dụng Node Package Manager (npm) để cài đặt Gulp trên máy tính của bạn.
- `-g` trong lệnh này nói với npm cài Gulp với phạm vi toàn cục trên máy tính của bạn, nó cho phép sử dụng lệnh gulp ở bất kỳ đâu trên hệ thống của bạn.
- `--save-dev` sẽ thêm gulp như một dev dependency trong package.json.
- Bước cài đặt global chỉ cần làm 1 lần duy nhất trên 1 máy tính. Còn bước cài đặt trong thư mục dự án thì bắt buộc cài khi tạo một dự án mới.

Sau khi cài đặt xong bạn có thể kiểm tra phiên bản gulp của bạn bằng việc chạy câu lệnh:
```bat
gulp --version
```

Cửa sổ dòng lệnh sẽ hiển thị thông tin về phiên bản hiện tại của Gulp cho bạn.
```bat
C:\xampp\htdocs\gulpjs>gulp --version
CLI version: 2.3.0
Local version: 4.0.2
```

## 3. Các thành phần chính của Gulp

Để chạy được gulp cần một file gulpfile.js trong đó có chứa các thành phần chính là: `gulp.task`, `gulp.src`, `gulp.dest`, `gulp.watch`

### 3.1. gulp.task

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

### 3.2. gulp.src

Trong gulp.task bạn sẽ cần trỏ src file mà bạn muốn minify chẳng hạn, gulp.src sẽ giúp bạn làm việc đó, tức là file bạn cần đọc hay nói cách khác khi bạn muốn làm gì thì cần biết đường dẫn tới folder hay file.

```js
gulp.task('task_one', function(){
    gulp.src('['./css/*.css']) //lấy tất cả các file có đuôi .css trong folder css
    // or
    gulp.src('./js/*.js') //lấy tất cả các file có đuôi .js trong folder js
    // or
    gulp.src('['!./css/*.css']) //không lấy folder css cùng các file bên trong
})
```

### 3.3. gulp.dest

Tương tự gulp.src bạn cũng cần chỉ ra đường dẫn đích mà bạn muốn gulp trả về file sau khi đã thực hiện gulp.task.

```js
gulp.task('task_one', function() {
  gulp.src('./js/*.js')
    .pipe(gulp.dest('dist/js'));

  gulp.src('./css/*.css')
    .pipe(gulp.dest('dist/css'));
});
```

### 3.4. gulp.watch

gulp.watch sẽ tự động lắng nghe file nếu có sự thay đổi thì bạn không phải chạy lại gulp nhiều lần. Tính năng này hay được sử dụng để live browser hoặc tự động minify các file css, js,...

```js
gulp.task('watch_name', function(){
    gulp.watch('/css/*.css',  ['task_css'])
    gulp.watch('/js/*.js',  ['task_js'])
})
gulp.watch('js/**/*.js', function(event) {
  console.log('File ' + event.path + ' was ' + event.type + ', running tasks...');
});
```

Vậy là đủ đề hiểu cơ bản về cơ chế hoạt động của Gulp rồi. Tiếp đến mình sẽ hướng dẫn các bạn cách dùng nhé.


## 4. Sử dụng Gulp

Việc sử dụng Gulp khá đơn giản, để bắt đầu ta tạo một file với tên là `gulpfile.js` lưu trong thư mục gốc của dự án. Chúng ta sẽ định nghĩa các task của Gulp ở đây, và chúng sẽ được chạy bởi gulp command. Đặt đoạn code dưới đây vào trong file `gulpfile.js`:

```js
var gulp = require('gulp');

gulp.task('default', function(){
   // Default task code
});
```

Để chạy file gulpfile.js chúng ta dùng lệnh:
```bat
gulp
```

Mặc định khi chạy gulp command không có tham số, Gulp sẽ ngầm thực thi task default, nếu muốn chạy với một task nào đó, chúng ta dùng cú pháp:
```bat
gulp {task_name}
```

Như ví dụ bên trên bạn có thể thấy, để định nghĩa một task ta có thể sử dụng `gulp.task()`

Yêu cầu viết task minify với mục đích minify các file Javascript. Chúng ta cần cài đặt gulp-uglify plugin:
```bat
npm install --save-dev gulp-uglify
```

NPM sẽ tự động cài đặt và chúng ta chỉ cần sử dụng plugin đó với một định nghĩa như một object bằng cú pháp:
```js
var gulp = require('gulp'),
  uglify = require('gulp-uglify');
```

Chúng ta sẽ định nghĩa một task có tên là minify, khi chạy sẽ gọi đến function ở argument thứ hai:
```js
gulp.task('minify', function () {

});
```

Cuối cùng chúng ta sẽ định nghĩa những gì mà task của chúng ta sẽ thực hiện ở trong function đó:

```js
gulp.src('js/app.js')
   .pipe(uglify())
   .pipe(gulp.dest('build'))
```

Cập nhật file gulpfile.js:
```js
var gulp = require('gulp'),
  uglify = require('gulp-uglify');

gulp.task('minify', function () {
    gulp.src('js/*.js')
       .pipe(uglify())
       .pipe(gulp.dest('build'))
});
```

Sau đó chúng ta dùng lệnh:
```bat
gulp minify
```

Và kiểm tra trong thư mục build, các file javascript đã được minify. Rất đơn giản phải không các bạn?

Trừ phi bạn đã quen với streams, nếu không đoạn code trên không có ý nghĩa nhiều với bạn. Sau đây tôi sẽ giải thích về streams trong Gulp.

### Streams

Streams cho phép bạn vượt qua một số dữ liệu thông qua một số function nhỏ, ở đó sẽ sửa đổi các dữ liệu và sau đó chuyển các dữ liệu đã sửa đổi đến các function tiếp theo. Trong ví dụ ở trên, function `gulp.src()` sẽ cần một string dẫn đến một file hoặc nhiều files mà chúng ta cần buil. Tạo một stream đại diện cho các objects của files, sau đó thông qua hoăc pipep tới function `uglify()`, function này sẽ sử dụng files với src ở trên và tạo ra các object files mới với code đã được thu nhỏ. Files đầu ra sẽ được tạo ra ở function `gulp.dest()`. Dưới đây là sơ đồ mô tả những gì đã diễn ra:

![Gulp](https://boxxv.github.io/img/2022/8ade1d33-074f-4707-840b-9e4dcc82591c.webp "Gulp")

Khi sử dụng duy nhất 1 task, function trên dường như là không đủ. Xem tiếp đoạn code dưới đây:

```js
gulp.task('js', function () {
    return gulp.src('js/*.js')
        .pipe(jshint())
        .pipe(jshint.reporter('default'))
        .pipe(uglify())
        .pipe(concat('app.js'))
        .pipe(gulp.dest('build'));
});
```
Để chạy function trên bạn cần cài đặt `gulp`, `gulp-jshint`, `gulp-uglify`, và `gulp-concat`. Task trên sẽ lấy tất cả các file có đuôi js ở trong thư mục `js/`, chạy JSHint trên chúng in ra output, thu nhỏ chúng rồi ghép chúng với nhau lưu vào một file `build/app.js`

![Gulp](https://boxxv.github.io/img/2022/f0cef8d5-9494-406b-83e2-45295632932b.webp "Gulp")


### Gulp.src()

Function `gulp.src()` sẽ lấy một hoặc nhiều file trùng khớp với điều kiện trong `src()` và trả về một stream có thể piped tới các plugins.

Gulp sử dụng [Node-glob](https://github.com/isaacs/node-glob) để lấy file từ glob hoặc globs đã được chỉ định. Cách sử dụng rất dễ dàng:

- `js/app.js` Tìm chính xác file.
- `js/*.js` Tìm kiếm tất các file kết thúc bằng `.js` và nằm trong thư mục js.
- `js/**/*.js` Tìm kiếm tất cả các file kết thúc bằng .js ở trong thư mục js/ và tất cả thư mục con của nó.
- `!js/app.js` Tìm kiếm tất cả các file trong thư mục ngoại trừ file `app.js`
- `*.+(js|css)` Tìm kiếm tất cả các file trong thư mục root có đuôi là `.js` và `.css`.

Những ví dụ trên là những ví dụ thông thường nhất được sử dụng trong Gulp. Nếu bạn muốn sử dụng nhiều hơn, tham khảo [Minimatch](https://github.com/isaacs/minimatch). Nếu muốn thêm điều kiện để lấy files, chỉ cần kết hợp các điều kiện bên trong một mảng:

```js
gulp.src(['js/**/*.js', '!js/**/*.min.js'])
```

### Defining Tasks

Để định nghĩa 1 task, sử dụng function `gulp.task()`. Khi định nghĩa một task đơn giản, function này cần 2 thuộc tính: tên của task và một function dùng để chạy.

```js
gulp.task('greet', function () {
   console.log('Hello world!');
});
```

Khi chạy `gulp greet` sẽ nhận được kết quả là `Hello world!` được in ra trong console.

Một task cũng có thể gồm nhiều task khác. Khi muốn định nghĩa một task nhằm chạy 3 task khác `css`, `js`, `imgs`, chúng ta có thể quy định một mảng các tasks:

```js
gulp.task('build', ['css', 'js', 'imgs']);
```

Chú ý là các task trên sẽ chạy không đồng bộ, có nghĩa là bạn không thể chắc chắn rằng task `css` sẽ chạy xong khi task `js` bắt đầu được. Để đảm bảo rằng một task được chạy sau khi một task khác chạy xong chúng ta có thể làm như sau:

```js
gulp.task('css', ['greet'], function () {
   // Deal with CSS here
});
```

Task `css` sẽ được chạy ngay sau khi task `greet` hoàn thành.

### Default tasks

Bạn có thể định nghĩa một task mặc định khi chạy `gulp` với task name là `default`:

```js
gulp.task('default', function () {
   // Your default task
});
```

### Plugins
Chúng ta có thể sử dụng một số plugins (hơn 600) với Gulp. Chúng có thể được tìm thấy tại [Plugin page](https://gulpjs.com/plugins/) hoặc bẳng cách tìm kiếm với từ khóa `gulpplugin` trong npm.

### Gulp-load-plugins

Một module rất hữu ích cho việc tự động load bất kỳ plugins nào từ `package.json` và gắn chúng vào một object.

```js
var gulpLoadPlugins = require('gulp-load-plugins'),
    plugins = gulpLoadPlugins();
```

**Package.json**
```js
{
    "devDependencies": {
        "gulp-concat": "~2.2.0",
        "gulp-uglify": "~0.2.1",
        "gulp-jshint": "~1.5.1",
        "gulp": "~3.5.6"
    }
}
```

Sau khi chạy `gulp-load-plugins`, chúng ta có thể sử dụng plugins với tên dạng camelCase ví dụ, sử dụng plugin `gulp-ruby-sass` bằng cú pháp `plugins.rubySass` sử dụng như dạng require thông thường.

```js
var gulp = require('gulp'),
    gulpLoadPlugins = require('gulp-load-plugins'),
    plugins = gulpLoadPlugins();

gulp.task('js', function () {
    return gulp.src('js/*.js')
        .pipe(plugins.jshint())
        .pipe(plugins.jshint.reporter('default'))
        .pipe(plugins.uglify())
        .pipe(plugins.concat('app.js'))
        .pipe(gulp.dest('build'));
});
```

### Watching files

Gulp có khả năng kiểm soát sự thay đổi của file và chạy một task hoặc nhiều task khi phát hiện sự thay đổi của file đó. Tính năng này rất tiện dụng, bạn có thể tưởng tượng rằng, khi bạn lưu một LESS file hoặc SASS file, Gulp sẽ đưa những thay đổi đó vào trong file CSS và tự động cập nhật nó trên trình duyệt. Bạn không cần phải reload lại trang hay làm gì cả.

```js
gulp.task('watch', function () {
    gulp.watch('templates/*.tmpl.html', ['build']);
});
```

khi ta thay đổi một file file template, task `build` sẽ được chạy và file html sẽ được tạo ra. Bạn cũng có thể đặt function `watch` trong một function callback:

```js
gulp.watch('templates/*.tmpl.html', function (event) {
    console.log('Event type: ' + event.type); // added, changed, or deleted
    console.log('Event path: ' + event.path); // The path of the modified file
});
```

## 5. Tự động refresh browser

### LiveReload

[LiveReload](http://livereload.com) liên kết với browswer extensions (bao gồm cả Chrome extensions) sẽ reload browswer mỗi khi phát hiện thấy sự thay đổi của một file. Nó có thể sử dụng với [gulp-watch](https://www.npmjs.org/package/gulp-watch) plugin hoặc với `gulp.watch()`. Ví dụ:

```js
var gulp = require('gulp'),
    less = require('gulp-less'),
    livereload = require('gulp-livereload'),
    watch = require('gulp-watch');

gulp.task('less', function() {
    gulp.src('less/*.less')
        .pipe(watch())
        .pipe(less())
        .pipe(gulp.dest('css'))
        .pipe(livereload());
});
```

Đoạn code trên sẽ xác định sự thay đổi của bất kỳ file .less nào trong thư mục less/, khi phát hiện thấy sự thay đổi, nó sẽ tạo ra CSS sau đó tự động reload lại browser.

### BrowserSync

Tương tự với LiveReload, BrowserSync cũng tự động hiện thị những thay đổi trên browser, nhưng nó có nhiều chức năng hơn. Khi bạn tạo ra một thay đổi trong code, Browser hoặc là reload page, hoặc nếu file thay đổi là css sẽ injects css, điều đó có nghĩa là sẽ không cần refresh lại page.

![Gulp](https://boxxv.github.io/img/2022/ce31cb07-e5a5-4bd8-b50e-88c408ec1df9.gif "Gulp")

Để cài đặt BrowserSync, chúng ta sẽ sử dụng npm:

```bat
npm install --save-dev browser-sync
```

Sử dụng như các plugins khác trong Gulp:

```js
var gulp = require('gulp'),
    browserSync = require('browser-sync');

gulp.task('browser-sync', function () {
    var files = [
        'app/**/*.html',
        'app/assets/css/**/*.css',
        'app/assets/imgs/**/*.png',
        'app/assets/js/**/*.js'
    ];

    browserSync.init(files, {
        server: {
            baseDir: './app'
        }
    });
});
```

Chạy `gulp browser-sync` sẽ kiểm soát tất cả thay đổi của file và sẽ bắt đầu một server trong thư mục `app/`.

### Minify css, js

Để minify các file css, js ở đây mình dùng các pagekage này:

```bat
npm install gulp-minify-css --save-dev
npm install gulp-minify --save-dev
```

- gulp-minify: minify các file js
- gulp-minify-css: minify các file css

Tiếp đến, tạo ra một task mới, đặt tên là compress với nội dung như sau:

```js
gulp.task('compress', function() {
  //cấu hình minify js
  gulp.src('assets/js/*.js') //đường dẫn đến thư mục chứa các file js
    .pipe(minify({
        exclude: ['tasks'],
        ignoreFiles: ['-min.js'] //những file không muốn nén
    }))
    .pipe(gulp.dest('dist/js')); //thư mục dùng để chứa các file js sau khi nén
  //cấu hình minify css
  gulp.src('assets/css/*.css') //đường dẫn đến thư mục chứa các file css
    .pipe(minifyCss({compatibility: 'ie8'}))
    .pipe(gulp.dest('dist/css')); //thư mục dùng để chứa các file css sau khi nén
});
```

Để thực thi task này (chỉ nên thực thi sau khi đã hoàn tất project), chúng ta gõ lệnh: `gulp compress` Trong thư mục project của bạn sẽ xuất hiện thêm một thư mục dist (chứa các file đã được nén) như hình dưới.

Như vậy hoàn chỉnh file gulpfile.js của mình gồm có nội dung sau:

```js
var gulp = require('gulp');
var browserSync = require('browser-sync').create();
var minify = require('gulp-minify');
var minifyCss = require('gulp-minify-css');

gulp.task('serve', [], function () {
    browserSync.init({
        server: {
            baseDir: '.'
        }
    });
    gulp.watch("*.html").on('change', browserSync.reload);
    gulp.watch(['assets/js/*.js'], browserSync.reload);
    gulp.watch(['assets/css/*.css'], browserSync.reload);
});

gulp.task('compress', function() {
  gulp.src('assets/js/*.js') //đường dẫn đến thư mục chứa các file js
    .pipe(minify({
        exclude: ['tasks'],
        ignoreFiles: ['-min.js'] //những file không muốn nén
    }))
    .pipe(gulp.dest('dist/js')); //thư mục dùng để chứa các file js sau khi nén

  gulp.src('assets/css/*.css') //đường dẫn đến thư mục chứa các file css
    .pipe(minifyCss({compatibility: 'ie8'}))
    .pipe(gulp.dest('dist/css')); //thư mục dùng để chứa các file css sau khi nén
});

gulp.task('default', ['serve']);
```

Tương tự các bạn có thể cài package của sass để combine css nhé 😃


## Tổng kết

Như vậy, sử dụng Gulp sẽ rất tiện lợi, tăng hiệu suất và giúp công việc lập trình thuận tiện hơn. Hơn nữa với những hệ thống sử dụng nhiều CSS, JS đặc biệt là ReactJs (hoặc tương tự) thì việc sử dụng Gulp càng bộc lộ những yếu tố cần thiết và quan trọng của một build system. Một [demo](https://github.com/tranluan91/laravel) nhỏ, sử dụng Gulp để build CoffeeScript, Sass với Laravel 4.2

-----
Tham khảo:

- [Building với Gulp](https://viblo.asia/p/building-voi-gulp-n157G5KBRAje)
- [Tìm hiểu về Gulp.js](https://viblo.asia/p/tim-hieu-ve-gulpjs-naQZRw2jlvx)
- [Tìm hiểu và sử dụng Gulp JS](https://viblo.asia/p/tim-hieu-va-su-dung-gulp-js-aWj53OVo56m)
- [Mở đầu với Gulp](https://viblo.asia/p/mo-dau-voi-gulp-l5XRBVxmRqPe)
- [Gulp for beginner](https://viblo.asia/p/gulp-for-beginner-WAyK89knZxX)
- [So sánh Gulp và Grunt](https://viblo.asia/p/so-sanh-gulp-va-grunt-157G5oY5RAje)
- [Làm sao để gulp (đặc biệt là gulp watch) không crash khi gặp lỗi](https://viblo.asia/p/lam-sao-de-gulp-dac-biet-la-gulp-watch-khong-crash-khi-gap-loi-WEMkBYOLeQK)
- [https://github.com/gulpjs/gulp/blob/v3.9.1/docs/API.md](https://github.com/gulpjs/gulp/blob/v3.9.1/docs/API.md)
- [Sử dụng Gulp để viết Sass hiệu quả](https://kipalog.com/posts/Su-dung-Gulp-de-viet-Sass-hieu-qua)
- [Gulp minify](https://zetcode.com/gulp/minify/)
- [HTML includes with Gulp.js](https://dev.to/caiojhonny/html-includes-with-gulp-js-2def)
- [How To Build And Develop Websites With Gulp](https://www.smashingmagazine.com/2014/06/building-with-gulp/)
- [Gulp: A Web Developer's Secret Weapon for Maximizing Site Speed](https://www.toptal.com/javascript/optimize-js-and-css-with-gulp)