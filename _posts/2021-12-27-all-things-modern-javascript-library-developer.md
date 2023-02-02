---
layout: post
title: Tổng hợp về Thư viện JavaScript hiện đại
subtitle: The Modern JavaScript Library Tutorial

tags:
- JavaScript
- library
- frontend
- roadmap
- module
- tutorial
---

![Module Javascript](https://boxxv.github.io/img/posts/module-loading.png "Module Javascript")

### [Package Managers](#i-package-managers)
- [npm](#1-npm)
- [yarn](#2-yarn)

### [Build Tools](#ii-build-tools)

#### [Task Runners](#a-task-runners)
- [npm scripts](#3-npm-scripts)
- [Gulp](#4-gulp)
- [Grunt](#5-grunt)

#### [Module Bundlers](#b-module-bundlers) - Module Loaders
- [Webpack](#6-webpack)
- [Rollup](#7-rollup)
- [Parcel](#8-parcel)
- RequireJS, Browserify, SystemJs
- Tiny Loaders: curl, LABjs, almond

-----

# I. Package Managers

### 1. `npm`
`Node Package Manager`, hoặc `npm` (thường được viết bằng chữ thường) là một trong những công cụ tạo và quản lý các thư viện được sử dụng phổ biến nhất trong các dự án JavaScript. Nó được xây dựng trên Node và rất mạnh mẽ nên hầu như tất cả mọi người đều đang sử dụng nó.

Trong cộng đồng Javascript, các lập trình viên chia sẻ hàng trăm nghìn các thư viện với các đoạn code đã thực hiện sẵn một chức năng nào đó. Nó giúp cho các dự án mới tránh phải viết lại các thành phần cơ bản, các thư viện lập trình hay thậm chí cả các framework. Công cụ này cho phép publish các package của bạn lên trang chủ `NPM` và tìm kiếm, cài đặt các module, package do những người khác up lên.

Cộng đồng sử dụng npm rất lớn, hàng nghìn các thư viện được phát hành, hỗ trợ Javascript ES6, React, Express, Grunt, Duo…

`npm` tốt, nhưng nó cũng có một vài thiếu sót của nó. Sau đây là một vài điều trong số đó:
- **Queued install**: khi npm lấy các dependencies từ kho chứa của nó, nó sẽ cài đặt các dependencies từng cái một sau khi một cái khác được cài đặt xong, vì vậy sẽ mất rất nhiều thời gian.
- **Single registry**: Nếu như một package không có trong [NpmJS](https://www.npmjs.com), hãy quên nó đi.
- Không hỗ trợ cài đặt offline

-----

### 2. `Yarn`

Yarn là một sản phẩm mã nguồn mở, được sự hợp tác của Exponent, Google và Tilde. Với Yarn, các lập trình viên vẫn truy cập vào kho cung cấp các gói phần mềm do npm lưu trữ, tuy nhiên chúng ta có thể cài đặt các gói phần mềm này nhanh hơn và đảm bảo tính thống nhất các lập trình viên tham gia cài đúng phiên bản của các gói phần mềm được định nghĩa.

Đây là dự án bắt đầu được viết từ tháng 1/2016, sau quãng thời gian thử nghiệm và hoàn thiện đã được mở ra thành mã nguồn mở, và thật không có gì ngạc nhiên khi với những tính năng nổi trội vượt bậc đã có 10.000 stars chỉ trong 1 ngày tại Github. Chứng tỏ sự thành công và là tín hiệu thay thế rõ ràng NPM.

`Yarn` được đưa ra để thay thế cho `npm` hoặc các công cụ quản lí các gói thư viện khác cũng tương tác với kho cung cấp các gói phần mềm do npm cung cấp. Nó có đầy đủ những tính năng của npm trong khi đó lại nhanh hơn, bảo mật hơn và đáng tin cậy. Vì vậy bạn hoàn toàn có thể yên tâm khi dùng Yarn thay thế cho npm, bower ...

Đặc trưng
- **Tốc độ**: YARN sẽ tạo cache cho tất cả các gói đã được tải về, và tải đồng thời nhiều gói cùng lúc nên tốc độ download rất nhanh.
- **Tin cậy**: sử dụng tập tin lock (tương tự composer) với format chi tiết nhưng ngắn gọn, đảm bảo tính nhất quán khi cài đặt các gói giữa các hệ thống (ví dụ máy dev và máy chủ)
- **Bảo mật**: sử dụng checksum để đảm bảo tính nguyên vẹn của code trước khi nó được thực thi.

Tính năng
- **Offline mode**: khi đã tải về, YARN sẽ cache lại và khi có thể cài đặt lại không cần internet.
- **Deterministic**: các gói thư viện sẽ được cài đặt nhất quán cho dù thứ tự cài đặt khác nhau cho tất cả các máy
- **Network Performance**: sử dụng hiệu quả hàng đợi các request và tránh waterfall các request để tối ưu tốc độ mạng.
- **Multiple Registries**: cài đặt các gói từ các registries như Bower hay NPM đều đảm bảo workflow giống nhau.
- **Network Resilience**: nếu một request bị fail thì nó không làm cho tiến trình bị dừng lại, khác với npm là nếu npm bị lỗi thì bị dừng lại., không những vậy mà còn có khả năng cố gắng thử lại.
- **Flat Mode**: giải quyết việc không đồng nhất phiên bản của các gói thành 1 gói để tránh tạo trùng lặp

Với nhiều cải tiến đáng kể của mình so với npm yarn rất đáng để thử và trải nghiệm với dự án của bạn. Bạn có thể tham khảo thêm các lệnh khi chuyển từ sử dụng npm sang yarn ở đây [migrating from npm](https://classic.yarnpkg.com/en/docs/migrating-from-npm)

Do YARN cũng sử dụng package.json nên nếu dự án đã có thì việc sử dụng YARN cũng không khác mấy, chỉ cần bạn xóa tất cả các thư mục trong `node_modules`, sau đó dùng yarn để cài lại.


-----

# II. Build Tools
## A. Task Runners
### 3. `npm scripts`

### 4. `Gulp`
Gulp là một tool viết bằng Javascript, được sử dụng để tự động hoá các tác vụ giúp các bạn có thể tiết kiệm rất nhiều thời gian trong quá trình làm việc. Biên dịch, thu gọn code, tối ưu hình ảnh, unit testing linting là những task lập lại nên được tự động hoá.

Gulp giúp quá trình viết task dễ dàng hơn, thậm chí cho những người ít kinh nghiệm với JavaScript. Dù bạn có là một developer hay là một designer (người sẽ phải làm quen với HTML wireframes hiện tại hoặc sau này), tôi cũng khuyến khích hãy thử sử dụng Gulp.

Nó thường được dùng để
- Spinning up web server
- Reload browser khi có file được save.
- Sử dụng SASS hoặc LESS
- Optimizing assets như CSS, JS, images

Sử dụng thành thạo Gulp sẽ giúp ta thao tác rất nhanh trong việc development web.

Sử dụng Gulp không khó, chính thế mà nhiều người thích sử dụng Gulp hơn Grunt vì syntax khá đơn giản.

> [Tìm hiểu và sử dụng Gulp JS](https://boxxv.github.io/2022/12/27/tim-hieu-va-su-dung-gulpjs/)

### 5. `Grunt`

Grunt là một task runner (trình chạy task) và một công cụ tự động của JavaScript. Grunt có một giao diện command-line cho phép bạn chạy các task tự chọn được định nghĩa trong một Gruntfile. Grunt có hàng ngàn plugins để chọn lựa, gồm có những task lập đi lập lại mà bạn sẽ gặp phải. Với Grunt, bạn có thể dùng tất cả task bằng một dòng lệnh, làm cuộc sống bạn dễ dàng hơn.

## B. Module Bundlers

Ngày nay, chẳng ai build website với chỉ HTML, CSS, JS cả. Ít nhất ấy, thì cũng có một vài thứ khác bổ trợ như html-inspector, jQuery, React, Angular, .. và còn nhiều loại module javascript khác nữa.

Còn chưa kể app script không chỉ một file là xong logic cho cả trang web được, dev cần tách ra nhiều files để dễ quản lý code hơn, như là theo từng phần của trang web chẳng hạn: script-header.js, script-footer.js, script-about-page.js, …

Và thế là, <script> tags trong cái body hay header hay cả hai bắt đầu xếp hàng dài nối nhau như thế này:

```html
<body>
    <script src="script-header.js"></script>
    <script src="script-footer.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html-inspector/0.8.2/html-inspector.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
</body>
```

Thêm nữa nếu mấy cái script ở trên mà phụ thuộc vào nhau, không được sắp đúng vị trí thì bạn sẽ gặp các lỗi dạng như “Uncaught ReferenceError: $ is not defined“

Lỗi này xảy ra khi bạn viết code jquery trong file script-header.js mà load script jQuery ở sau file này. Thì lúc trình duyệt đọc đến file script-header.js nó sẽ báo lỗi là không tìm thấy jQuery.

Để sửa lỗi này thì các mô-đun được sử dụng ở những loại mô-đun cần được sắp xếp đúng thứ tự. Và thử tưởng tượng nếu có nhiều script thì việc sắp xếp chúng theo đúng thứ tự cần ưu tiên script nào load trước, cái nào load sau là cả một vấn đề, chưa nói chuyện nhìn vào cũng hơi hoa mắt.

Nhiệm vụ chính của bundler là gom hết tất cả các loại script lại cùng nhau theo thứ tự ưu tiên mà bạn đặt cho tụi nó và cho ra một file script duy nhất.

![Nguồn: freecodecamp.org](https://boxxv.github.io/img/posts/module-bundler.png "Nguồn: freecodecamp.org")

– tùy chọn xài javascript hoặc typescript
– tùy chọn xài HTML hoặc React
– tùy chọn xài CSS hoặc SASS

Bao trọn gói các loại modules khác như là lodash, firebase, … 


### 6. `Webpack`
Webpack hiện đang là `module loader` được sử dụng rộng rãi nhất hiện nay với cộng động support to lớn và những chức năng vô cùng mạnh mẽ.

Một cách đơn giản là ngày xưa chúng ta thường add những thư viện (3th parties) như `jquery`, `moment`, `select2`, `dtpicker`, `sticky`,... vào thẻ `script` để khi web load lên xong thì những thư viện này sẽ được `execute` và xử lý. Nhưng không còn như những ngày xưa chỉ vài dòng jquery là đủ dùng, sau này do việc code dưới front-end càng ngày càng phìng to nên việc quản lý code = javascript càng ngày càng tõ rõ sự quan trọng nên từ đó khái niệm `Module loader` ra đời.

Có khá nhiều thư viện từ nhỏ đến to ra đời cho việc này: Tiny Loaders (`curl`, `LABjs`, `almond`), `RequireJS`, `Browserify`, `SystemJs`, `Webpack` và gần đây đang nổi lên là `RollupJs`.

Nếu bạn nào có xài `SystemJs`, `Browserify` rồi thì thấy thật ra `Webpack` ra đời từ thừa hưởng những thành quả và kinh nghiệm từ những thư viện đó và phát triển lền một tầm mới tốt hơn cho công việc `quản lý module`.

Webpack là một trong những câu chuyện thành công nhất của cộng đồng JavaScript với hàng triệu lượt tải mỗi tháng cung cấp cho hàng chục nghìn trang web và ứng dụng. Nó có một hệ sinh thái rộng lớn, hàng chục người đóng góp.

Webpack được Tobias Koppers bắt đầu vào năm 2012 để giải quyết vấn đề khó khăn mà các công cụ hiện tại không giải quyết: xây dựng các ứng dụng phức tạp trên single page application (SPAs). Webpack được sinh ra và đã làm thay đổi nhiều thứ cũ bằng 2 thứ dưới đây:
- Việc tách code làm cho bạn có thể chia nhỏ ứng dụng của mình thành các phần có thể quản lý được load theo yêu cầu, có nghĩa là end-user có trang web tương tác nhanh hơn nếu họ phải đợi tất cả ứng dụng được tải xuống. Bạn có thể làm điều này bằng tay, nhưng... chúc may mắn.
- Các file tĩnh như hình ảnh và CSS có thể được import vào appication của bạn và được xem như một node được xem như một dependency. Webpack cũng có thể băm các tệp cho bạn.

### 7. `Rollup`
`React` đã thay thế `Webpack` bằng `Rollup`, điều này sẽ khiến nhiều người hỏi 'tại sao chọn Rollup thay vì dùng webpack?' Để có thể so sánh, Không chỉ React sử dụng Rollup mà `Vue`, `Ember`, `Preact`, `D3`, `Three.js`, `Moment` và hàng chục thư viện nổi tiếng khác cũng sử dụng `Rollup`. Vì vậy những gì đang xảy ra? Tại sao chúng ta không thể dùng duy nhất 1 gói JavaScript module bundler cho tất cả???

`Rollup` được tạo ra vì một lý do khác: làm phẳng các thư viện hiệu quả nhất, nó cho phép bạn code ứng dụng sử dụng các module `ES2015`, sau đó nó sẽ kết hợp tất cả các module thành một file nhằm giảm số lượng request http và cải thiện thời gian tải trang web. Mục đích của Rollup là trở nên nhanh và tạo các đoạn code rõ ràng và hiệu quả hơn bất kỳ công cụ đóng gói khác.

Các module ES2015 cho phép một cách tiếp cận khác nhau mà Rollup sử dụng. Tất cả code của bạn được đặt trong cùng một vị trí và đánh giá trong một lần gọi, dẫn đến code gọn nhẹ, đơn giản.

Tuy nhiên, có một sự khác biệt: tách code là một vấn đề phức tạp hơn, và tại thời điểm viết, Rollup chưa hỗ trợ việc tách code. Rollup không hỗ trợ việc thay thế nóng các module (Hot Module Replace). Và có thể là điểm trừ lớn nhất đối với những người đến Rollup: hầu hết các tệp CommonJS, một số đó không được biên dịch sang ES2015, trong khi webpack xử lý mọi thứ bạn muốn

#### Vậy tôi nên sử dụng cái gì?

Đến bây giờ, hy vọng rõ ràng là tại sao cả hai công cụ này lại tồn tại và hỗ trợ lẫn nhau - chúng phục vụ các mục đích khác nhau

Sử dụng webpack cho ứng dụng và Rollup cho thư viện

Đó không phải là một quy tắc cứng nhắc - nhiều trang web và ứng dụng được xây dựng bằng rollup, và cũng rất nhiều thư viện được xây dựng bằng webpack. Nhưng đó chỉ là một nguyên tắc nhỏ.

=> Nếu bạn cần tách code, hoặc bạn có file web resource tĩnh, hoặc bạn đang xây dựng một ứng dụng có nhiều phụ thuộc vào CommonJS, Webpack là một lựa chọn tốt.  
=> Nếu mã nguồn của bạn là các module ES2015 và bạn đang làm một cái gì đó để được sử dụng bởi những người khác, bạn có thể muốn Rollup.

Khi sử dụng Rollup, các modules được import vào sẽ được quyết định lúc biên dịch (trước khi thực thi) và bất kì exports nào không sử dụng sẽ được loại bỏ trước khi chương trình chạy. Vì vậy chúng ta sẽ tiết kiệm được dung lượng và giảm sự quá tải của code

Một tính năng tuyệt vời khác là của Rollup là Tree-shaking, sẽ loại bỏ các export không sử dụng trong gói. Do đó, thay vì import nguyên module, Tree-shaking cho phép bạn import phần mà bạn cần sử dụng.

### 8. `Parcel`

Parcel - một bundler nói "không" với config



-----
Tham khảo:

Npm  
- [https://viblo.asia/tags/npm](https://viblo.asia/tags/npm)
- [Cách tạo một NPM package đơn giản](https://viblo.asia/p/cach-tao-mot-npm-package-don-gian-3P0lPy3o5ox)
- [Tạo packages trong npm](https://viblo.asia/p/tao-packages-trong-npm-node-packages-manager-YWOZr6dNZQ0)
- [Quản lý các gói phụ thuộc với NPM](https://viblo.asia/p/manage-packages-dependencies-with-npm-YWOZrDLR5Q0)
- [Build và Publish một NPM Typescript package](https://viblo.asia/p/build-va-publish-mot-npm-typescript-package-gDVK2nGnKLj)
- [Publish package đầu tiên lên NPM như thế nào](https://viblo.asia/p/publish-package-dau-tien-len-npm-nhu-the-nao-Do754b7VZM6)
- [The package.json guide](https://viblo.asia/p/the-packagejson-guide-bWrZn0zY5xw)
- [Package-lock.json và những điều có thể bạn chưa biết](https://viblo.asia/p/package-lockjson-va-nhung-dieu-co-the-ban-chua-biet-RQqKL2WOl7z)
- [Tổng quan về NPM](https://viblo.asia/p/tong-quan-ve-npm-4P856dy3ZY3)
- [Mẹo và thủ thuật để làm việc với NPM](https://viblo.asia/p/meo-va-thu-thuat-de-lam-viec-voi-npm-djeZ1epYZWz)
- [Create and setup your Django project with webpack, npm and ReactJS (part1)](https://viblo.asia/p/create-and-setup-your-django-project-with-webpack-npm-and-reactjs-part1-aWj532jpl6m)
- [Sự khác nhau giữa npm và npx?](https://viblo.asia/p/su-khac-nhau-giua-npm-va-npx-bWrZnxM95xw)

-----
- [NPM, Yarn và Javascript](https://viblo.asia/p/npm-yarn-va-javascript-Eb85orNml2G)
- [Cài đặt một số Package trước khi làm dự án Nodejs](https://viblo.asia/p/cai-dat-mot-so-package-truoc-khi-lam-du-an-nodejs-Qpmlejm75rd)
- [Làm cách nào để sửa đổi thư viện trong node module](https://viblo.asia/p/lam-cach-nao-de-sua-doi-thu-vien-trong-node-module-eW65G6AalDO)

-----
Yarn  
- [https://viblo.asia/tags/yarn](https://viblo.asia/tags/yarn)
- [Yarn có gì mới so với npm](https://viblo.asia/p/yarn-co-gi-moi-so-voi-npm-Do754WR4lM6)
- [Yarn - Một cải tiến đáng kể so với NPM](https://viblo.asia/p/yarn-mot-cai-tien-dang-ke-so-voi-npm-yMnKMqRQK7P)
- [Hướng Dẫn Cài Đặt và Sử Dụng Yarn Package Manager](https://viblo.asia/p/huong-dan-cai-dat-va-su-dung-yarn-package-manager-4dbZNgoklYM)
- [Sử dụng Yarn với Rails](https://viblo.asia/p/su-dung-yarn-voi-rails-gDVK2jaAKLj)
- [Sử dụng Yarn trong dự án Laravel](https://viblo.asia/p/su-dung-yarn-trong-du-an-laravel-chuyen-training-php-tai-framgia-education-1Je5EjWAKnL)
- [Ứng dụng Yarn workspaces tạo ra những dự án Monorepo](https://viblo.asia/p/ung-dung-yarn-workspaces-tao-ra-nhung-du-an-monorepo-QpmleyXolrd)
- [Viết Javascript trong Rails 6 có gì khác? (với Webpacker, Yarn và Sprockets)](https://viblo.asia/p/viet-javascript-trong-rails-6-co-gi-khac-voi-webpacker-yarn-va-sprockets-924lJ4e0KPM)

-----
- [Sử dụng npm như một Build Tool](https://viblo.asia/p/su-dung-npm-nhu-mot-build-tool-jdWrvwq8Mw38)
- [https://viblo.asia/tags/gulp](https://viblo.asia/tags/gulp)
- [Mở đầu với Gulp](https://viblo.asia/p/mo-dau-voi-gulp-l5XRBVxmRqPe)
- [Gulp for beginner](https://viblo.asia/p/gulp-for-beginner-WAyK89knZxX)
- [Grunt - Javascript task runner](https://viblo.asia/p/grunt-javascript-task-runner-eJ1vOmqJMkby)
- [So sánh Gulp và Grunt](https://viblo.asia/p/so-sanh-gulp-va-grunt-157G5oY5RAje)

-----
Webpack  
- [https://viblo.asia/tags/webpack](https://viblo.asia/tags/webpack)
- [Webpack dành cho người mới bắt đầu](https://viblo.asia/p/webpack-danh-cho-nguoi-moi-bat-dau-bJzKmo4Ol9N)
- [Mình đã refactor file js 2500 lines code như thế nào?](https://viblo.asia/p/minh-da-refactor-file-js-2500-lines-code-nhu-the-nao-1VgZvMymKAw)
- [Bạn biết gì về Webpack?](https://viblo.asia/p/ban-biet-gi-ve-webpack-WAyK81wWZxX)
- [Webpack cơ bản. Hướng dẫn build project front-end (React, Redux, Sass) sử dụng Webpack.](https://viblo.asia/p/webpack-co-ban-huong-dan-build-project-front-end-react-redux-sass-su-dung-webpack-m68Z07YAKkG)
- [Tìm hiểu về webpack](https://viblo.asia/p/tim-hieu-ve-webpack-1Je5EPrGlnL)
- [Webpack series - giới thiệu từ cơ bản đến căng cơ](https://viblo.asia/p/webpack-series-gioi-thieu-tu-co-ban-den-cang-co-d-ep1-07LKXEgEZV4)
- [Webpack series - CSS Splitting - Tách css trong Webpack](https://viblo.asia/p/webpack-series-ep2-css-splitting-tach-css-trong-webpack-GrLZDVn25k0)
- [Webpack series - code splitting - chia code trong webpack](https://viblo.asia/p/webpack-series-ep3-code-splitting-chia-code-trong-webpack-yMnKMyRzK7P)
- [Tại sao tôi lại chuyển từ Webpack sang Brunch?](https://viblo.asia/p/tai-sao-toi-lai-chuyen-tu-webpack-sang-brunch-oOVlYykQl8W)
- [Webpack và Rollup](https://viblo.asia/p/webpack-va-rollup-3P0lPvWoKox)

-----
Parcel  
- [module bundler là gì? Parcel – một bundler nói “không” với config](https://viblo.asia/p/module-bundler-la-gi-parcel-mot-bundler-noi-khong-voi-config-gDVK2o9vZLj)


-----
- [Roadmap to becoming a web developer in 2021](https://github.com/kamranahmedse/developer-roadmap)
- [Những thư viện và framework JavaScript quan trọng bạn cần biết](https://code.tutsplus.com/vi/articles/essential-javascript-libraries-and-frameworks-you-should-know-about--cms-29540)
- [The 40 Best JavaScript Libraries and Frameworks for 2021](https://kinsta.com/blog/javascript-libraries/)
- [Tương lai của JavaScript ra sao trong thế giới Front-End?](https://topdev.vn/blog/tuong-lai-cua-javascript-ra-sao-trong-the-gioi-front-end/)