---
layout: post
title: Thư Viện Và Framework Javascript quan trọng bạn cần biết
subtitle: Essential JavaScript Libraries and Frameworks You Should Know About

tags:
- JavaScript
- library
- frontend
- roadmap
- module
- tutorial
- React
- Angular
- Vue
- Frameworks
- jQuery
- Tools & Tips
- Gulp.js
- Web Development
---

# Tóm tắt

### [I. Thư viện](#i-thư-viện)
- [React](#react)
- [jQuery](#jquery)
- [D3.js](#d3js-data-driven-documents)

### [II. Frameworks](#ii-frameworks)
- [Angular](#angular)
- [Vue.js](#vuejs)
- [Ember.js](#emberjs)

### [III. Tools](#iii-các-công-cụ)
#### [General-purpose](#tools-trình-chạy-task-có-mục-đích-tổng-thể)
- [Gulp](#gulp)
- [Grunt](#grunt)
- [npm](#npm)

#### [Testing](#tools-testing)
- [Jest](#jest)
- [Mocha](#mocha)
- [Jasmine](#jasmine)

-----

JavaScript đã tồn tại hơn 20 năm, và là một trong những ngôn ngữ không ngừng phát triển. Ngôn ngữ này gần đây trải qua giai đoạn tăng trưởng rất nhanh, điều này làm tôi tự hỏi: liệu các kỹ thuật JavaScript cho front-end nổi bật hiện nay sau vài năm nữa có còn được chú ý nữa không.

Tuy nhiên, quan trong là luôn dẫn đầu cuộc chơi bằng cách sử dụng những công nghệ những công cụ và framework mới nhất cho việc phát triển tốt hơn. Bài viết này khám phá những thư viên, framework JavaScript khác nhau và các công cụ bạn nên cân nhắc học ngay bây giờ.

# Giới thiệu

Môi trường JavaScript đã trở nên khổng lồ. Nó có hệ sinh thái của riêng nó với thư viện, frameworks, công cụ, các quản lý package và các ngôn ngữ mới để biên dịch ra JavaScript. Thật thú vị, npm, là một trình quản lý package thực thụ cho JavaScript, cũng là một software registry lớn nhất của thế giới. Đây là một đoạn trích từ một bài viết xuất bản trên Linux.com vào tháng 1 2017.

> Với hơn 350,000 packages, npm registry chứa gần như hơn gấp đôi package registry phổ biến tiếp theo (Apache Maven). Thực tế, hiện thời nó là package registry lớn nhất thế giới.

8 tháng nhanh chóng trôi qua, và hiện giờ có 500,000 packages trong npm registry. Là một sự tăng trưởng khủng khiếp so với những package repo khác. 

![npm](https://boxxv.github.io/img/posts/Essential-JavaScript-Libraries-Frameworks-npm-stats-01.jpg "Front End")

Là một nhà phát triển front-end JavaScript, bắt kịp với những công cụ và thư viện JavaScript thực sự rất quan trọng. Khi một công nghệ trở nên phổ biến, nhu cầu sẽ tăng cao, lần lượt nó sẽ làm xuất hiện nhiều công việc lập trình hơn với mức lương cao hơn trong ngành công nghiệp. Vì vậy tôi tập hợp một danh sách những kỹ thuật JavaScript tôi nghĩ rằng bạn nên lưu tâm.

# I. Thư viện

Một thư viện là các code có thể sử dụng lại để thực hiện những chắc năng cụ thể. Nó là một tập hợp những hàm, đối tượng, và class bạn có thể dùng trong ứng dụng của bạn. Một thư viện tách ra những layer khác nhau vì thế bạn không phải quan tâm đến các chi tiết khi triển khai.

Và bạn có thể gọi một hàm từ thư viện và đưa các tham số, và thư viện xử lý nó và trả về quyền điều khiển cho bạn. Tuy nhiên, nó không đặt để bất kỳ quy tắc nào giới hạn cách bạn sử dụng thư viện đó. Thư viện JavaScript phổ biến gồm có:


## [React](https://reactjs.org)

React là một thư viện được xây dựng cho các nhà phát triển của Facebook và Instagram. React được bầu chọn là một công nghệ được yêu thích nhất của các nhà phát triển, dựa theo khảo sát của Stack Overflow 2017. React cũng có uy tín trở thành một dự án JavaScript phổ biến nhất dựa trên số sao đếm được từ GitHub.

Vậy tại sao React được toàn thể chú ý như vậy? Với React, hoàn toàn có thể tạo ra một ứng dụng tương tác sử dụng phương pháp declarative, ở đó bạn có thể kiểm soát trạng thái của ứng dụng bằng cách nói "view nên trông giống như vậy nè" Nó sử dụng model component-based, các component là những thành phần UI được tái sử dụng và mỗi component có trạng thái riêng.

![React](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-React.jpg "React")

React sử dụng Virtual DOM do đó bạn không cần phải quan tâm đến việc trực tiếp thao tác DOM. Tính năng đáng chú ý khác của React bao gồm các luồng dữ liệu một chiều (one-way data flow), tùy chọn cú pháp JSX và công cụ command-line cho việc tạo ra một dự án React mà không cần cấu hình ban đầu. 


## [jQuery](https://jquery.com)

jQuery là một thư viện làm cho JavaScript dễ tiếp cận hơn và thao tác với DOM trở nên dễ dàng hơn bao giờ. Quá trịnh học nhẹ nhàng và cú pháp dễ dàng của jQuery đã hình thành một thế hệ nhà phát triển client-side mới. Một vài năm trước đây, jQuery đã được xem là một giải pháp vững chãi để xây dựng các website mạnh mẽ, với hỗ trợ đa trình duyệt. Các tính năng cốt yếu của jQuery như xử lý DOM dựa trên CSS selectors, event handling và gọi AJAX đã thúc đẩy sự phổ biến của nó.

![jQuery](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-jQuery.jpg "jQuery")

Tuy nhiên, sự việc đã thay đổi, và môi trường JavaScript đã phát triển nhanh chóng. Vài điểm nổi bật của jQuery đã được tích hợp vào chuẩn ECMAScript mới đây. Hơn nữa, những framework và thư viện mới được dùng ngày nay có cách riêng để gắn kết DOM, và vì thế các kỹ thuật thao tác DOM truyền thống không còn được yêu cầu nữa. Đột phổ biến của jQuery đang giảm dần, nhưng tôi thấy nó sẽ không biến mất sớm đâu.


## [D3.js](https://d3js.org) Data-Driven Documents

D3 hoặc D3.js là một thư viện JavaScript mạnh mẽ để tạo ra những hình ảnh có tính tương tác sử dụng chuẩn mực web như SVG, HTML và CSS. Không giống với những thư viện hình ảnh trực quan khác, D3 cung cấp sự điểu khiển tốt hơn cho các kết quả hình ảnh được tạo ra.

D3 hoạt động bằng cách gắn kết data với DOM và sau đó thực hiện công tác chuyển đổi cho phần document. Nó cũng sở hữu một hệ sinh thái, gồm có các plugin và thư viện để thêm các chức năng mở rộng. Thư viện này đã xuất từ năm 2011, và có cả tấn tài liệu và bài hướng dẫn có thể giúp bạn bắt đầu ngay.

![D3](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-d3.jpg "D3")


# II. Frameworks

Một framework là một kiến trúc kiểm soát luồng đi của data trong ứng dụng của bạn. Framework hình thành cấu trúc cơ bản và cho bạn biết mọi thứ nên được tổ chức ra sao. Chức năng cơ bản để giúp ứng dụng lập tức vận hành cũng được cung cấp. Hơn thế nữa, bạn bị ràng buộc phải tuân theo các pattern và quy luật mà framwork thiết kế. Sự khác biệt giữa framework và thư viên là bạn gọi một thư viện thì framework sẽ gọi bạn.

Một framework chứa đựng nhiều thư viện và có hình thái cấp độ cao hơn. Chức năng như event binding, gọi AJAX, template và data binding, và testing được xây dựng bên trọng framework.

## [Angular](https://angular.io)

AngularJS là một trong những công nghệ JavaScript phổ biến nhất trong giới phát triển Front-End. Nó được hậu thuẫn bởi Google và một cộng đồng gồm nhiều cá nhân và tổ chức khác. Mặc cho sự phổ biến, AngularJS cũng từng có những sai sót của nó. Nhóm Angular đã bỏ ra 2 năm làm ra một phiên bản mới, cuối cùng đã ra mắt và tháng 9 2016.

![Angular](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Angular.jpg "Angular")

Angular 2 xuất xưởng là một phiên bản viết lại từ đầu của AngularJS. Một vài tính năng của Angular 2 gồm có:

- TypeScript thay cho JavaScript làm ngôn ngữ mặc định
- kiến trúc component-based
- cái thiện hiệu năng trên nền tảng web và mobile
- chọn lựa tốt hơn cho tooling và scaffolding

Tuy nhiên, nâng cấp từ Angular 1.x sang Angular 2.x khá là xa xỉ vì Angular 2 là một con thú hoàn toàn khác biệt. Đó là lý do cho việc tại sao Angular 2 chưa có tỉ lệ thực nghiệm cao như người tiền nhiệm của nó. Nhưng Angular và AngularJS vẫn tiếp tục là một công nghệ phổ dụng nhất dựa theo Stack Overflow 2017. Dự án Angular nhận được 28,000 sao trên GitHub.

## [Vue.js](https://vuejs.org)

Vue.js là một framework JavaScript nhỏ gọn đã xuất hiện theo xu thế năm nay. Nó là một framework JavaScript phổ biến trên GitHub tính theo lượng sao trên GitHub. Vue tuyên bố là một framework không quá cứng nhắc và do đó giúp nhà phát triển dễ dàng nắm bắt. Các mẫu cú pháp HTML của Vue gắn kết phần DOM đã render với giá trị của dữ liệu.

![Vue](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Vuejs.jpg "Vue")

Framework này cung cấp trải nghiệm như React với những Virtual DOM của nó và các component có thể tái sử dụng giúp bạn tạo ra cả widgets và toàn bộ ứng dụng web. Hơn nữa, bạn cũng có thể dùng cú pháp JSX để viết phần chức năng render trực tiếp. Khi trang thái thay đổi, Vue,js sẽ một hệ thống phản ứng để xác định rằng điều gì đã thay đổi và render só lượng nhỏ nhất các component. Vue.js cũng hỗ trợ tích hợp những thư viện khác vào framework mà không cần tốn công sức nhiều.

## [Ember.js](https://emberjs.com)

Ember.jsj là một framework front-end vân hành trên mô hình Model-View-ViewModel - cấu trúc MVVM. Nó tuân theo nguyên tắc hơn là phương pháp cấu hình, nó lạ sự phở biến giữa những franework sever-si server side khác như Ruby on Rail hoặc Laravel. Ember.js tổng hợp với những câu thành ngữ và thực tiễn nhất vào trong framework vì thế bạn có thể khởi động một ứng dụng chẳng mất nhiều công sức. 

![Ember](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Emberjs.jpg "Ember")

Ember thông thường gồm có:

- Ember CLI: cung cấp chọn lựa tạo khuôn mẫu cơ bản (scaffolding) và hỗ trợ hàng trăm add-ons.
- Ember Data: một thư viện data vững chắc có thể được cấu hình để làm việc với bất kỳ server back-end nào.
- Ember Inspector: Một extension (phần mở rộng) cho Chrome và Firefox.
- Liquid Fire: Một add-on cho việc chuyển đổi và hoạt hình.


# III. Các công cụ

Một công cụ là một tập hợp các công việc thường dùng, giúp bạn trong quá trình phát triển. Không giống thư viện, công cụ thường xử lý một task ở mã lệnh phía client. Nó dùng mã code làm dữ liệu ban đầu, thực hiện task trên đó, và trả về kết quả. Các công cụ thường dùng có transpiler và công cụ build, asset minifiers, module bundler và công cụ scaffolding.

# Tools: Trình chạy task có mục đích tổng thể

Trình chạy task General-purpose là các công cụ được dùng để tự động các công vlệc cụ thể. Các trình chạy task general-purpose gồm có:

## [Gulp](https://gulpjs.com)

Gulp là một bộ công cụ JavaScript được dùng như là một trình chạy task, được dựng như là một hệ thống xây dựng trong phát triển web. Biên dịch, thu gọn code, tối ưu hình ảnh, unit testing linting là những task lập lại nên được tự động hoá. Gulp giúp quá trình viết task dễ dàng hơn, thậm chí cho những người ít kinh nghiệm với JavaScript.

Gulp sử dụng pipeline để dẫn data từ một plugin sang một plugin khác, và kết quả sau cùng là xuất ra một thư mục đã được chỉ định trước. Gulp thực hiện công việc tốt hơn so với Grunt bởi vì nó không tạo ra file tạm thời để lưu trữ các kết quả, nó cho kết quả có ít lần gọi I/O hơn.

![Gulp](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Gulp.jpg "Gulp")

> [Tìm hiểu và sử dụng Gulp JS](https://boxxv.github.io/2022/12/27/tim-hieu-va-su-dung-gulpjs/)


## [Grunt](https://gruntjs.com)

Grunt là một task runner (trình chạy task) và một công cụ tự động của JavaScript. Grunt có một giao diện command-line cho phép bạn chạy các task tự chọn được định nghĩa trong một Gruntfile. Grunt có hàng ngàn plugins để chọn lựa, gồm có những task lập đi lập lại mà bạn sẽ gặp phải. Với Grunt, bạn có thể dùng tất cả task bằng một dòng lệnh, làm cuộc sống bạn dễ dàng hơn.

![Grunt the JavaScript task runner](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Grunt.jpg "Grunt the JavaScript task runner")

## [npm](https://www.npmjs.com)

Gulp và Grunt đòi hỏi bạn có thời gian học và thuần thục công cụ. Giới thiệu các phần phụ thuộc bổ sung vào dự án của bạn có thể tránh được bằng cách chọn lựa một thay thế đã được đóng gói với Node.js. Dù npm được biết đến nhiều hơn là một trình quản lý package, mã lệnh npm cũng có thể sử dụng để thực hiện các nhiệm vụ được đề cập trước đó.

![npm task runner](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-npm.jpg "npm task runner")

[6 điều khiến Yam trở thành quản lý JavaScript pakager tốt nhất](https://code.tutsplus.com/tutorials/6-things-that-make-yarn-the-best-javascript-package-manager--cms-29465)

# Tools: Testing

Testing là quá trình đánh giá và thẩm định phần mềm liệu đã đáp ứng được các yêu cầu mong đợi về kỹ thuật và business. Phương pháp Test-Driven Development cũng hướng đến việc phát hiện lỗi và được xem như một phần không thể thiếu của công việc phát triển front-end hiện đại.

## [Jest](https://jestjs.io)

Jest là một testing framework khá mới mẻ được xây dựng bởi Facebook và được cộng đồng React khá đón nhận. Có một quan niệm sai lầm phổ biến là Jest được thiết kế đặc thù để làm việc với React, tuy nhiên, theo tài liệu của Jest:

> Dù Jest có thể xem là test runner đặc thù cho React, nhưng thực tế là một nền tảng testing phổ cập, với khả năng thích nghi cho bất kể thư viện hoặc framework JavaScript nào. Bạn có thể sử dụng Jest để test bất kỳ mã JavaScript nào.

Lợi điểm to lớn nhất của Jest so với những bộ kiểm thử khác là không cần phải có cấu hình gì để bắt đầu viết các testing. Framework đã có phần thư viên dựng sẵn và hỗ trợ sử dụng của việc bắt chước các hàm.

![Delightful JavaScript testing using Jest](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Jest.jpg "Delightful JavaScript testing using Jest")

Jest có một tính năng gọi là snapshot testing cho phép bạn chắc chắn rằng UI của ứng dụng không thay đổi theo cách không mong muốn. Nhà phát triển tại Facebook và những người đóng góp khác đã bỏ rất nhiều công sức vào dự án này, vì vậy sẽ không ngạc nhiên nếu Jet trở thành testing framework phổ biến nhất trong những năm tối đây.

## [Mocha](https://mochajs.org)

Mocha là một testing JavaScript framework nổi bật với sự hỗ trợ của trình duyệt, hỗ trợ không đồng bộ gồm có promises, test coverage report (báo cáo kiểm tra), và một JavaScript API để vận hành các bài kiểm tra. Mocha thường dùng chung với một thư viện khác như Chai, should.js, expect.js hoặc một thu viện tốt hơn vì nó thiếu mất một thư viên của nó.

![Mocha test runner and testing framework](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Mocha.jpg "Mocha test runner and testing framework")

## [Jasmine](https://jasmine.github.io)

Jasmine là một testing framework theo kiểu behavior-driven cho JavaScript. Jasmine định hướng tới là một trình duyệt, nền tảng và bộ kiểm tra không lệ thuộc vào framework. Jasmine có một thư viện riêng của nó gọi là matchers với cú pháp rõ ràng và dễ đọc. Jasmine không có một test runner (trình chạy test) dựng sẵn, và bạn có lẽ phải dùng một test runner thuần tuý như Karma.

![Jasmine test runner and testing framework](https://boxxv.github.io/img/posts/Essential-JavaScript-Frameworls-Libraries-Tools-Jasmine.jpg "Jasmine test runner and testing framework")


# Tóm tắt

JavaScript, ngôn ngữ của web, đã xuất hiện từ ngày khái niệm về nó xuất hiện kể từ 1995. Nó dĩ nhiên sẽ tồn tại như thế miễn là các trình duyệt không quyết định thay nó bằng một ngôn ngữ khác. Mặc dù có rất nhiều ngôn ngữ khác biên dịch thành JavaScript, không có ngôn ngữ scripting nào khác có thể thay được JavaScript trong tương lai gần. Tại sao? Vì JavaScript đã trở nên quá phổ biến để có thể bị thay thế.

Ngôn ngữ này không chỉ dễ học, mà còn có rất nhiều framework và thư viện đủ để bạn bận rộn với nó. Nếu bạn đang tìm một số tài nguyên bổ sung để học hoặc sử dụng trong công việc, hãy xem qua những cái chúng tôi đã có sẵn trên Envato Market.

Môi trường JavaScript đang phát triển, với minh chứng là xu hướng hiện tại trong sự phát triển của web. Những thư viện và framework cũ đã bị thay thế bởi những công nghệ mới hơn. jQuery, một trong những thư viện JavaScript từng được yêu mến nhất, đang đương đầu với sự thất thế về độ hấp dẫn, cách sử dụng và sự phổ biến. Các thư viện, framework và công cụ thế hệ mới đang tăng trưởng và có được sự đón nhận rộng rãi.

Thích nghi dần với các xu hướng công nghệ mới cũng có lợi ích. Công việc code yêu cầu React có mức lương cao hơn trong ngành, với mức lương bình quân 105,000 đô Mỹ theo Stack Overflow (2016). Vậy bạn cần tiếp tục học và trải nghiệm những công cụ và framework mới nhất để chọn ra cái tốt nhất.

Nếu bạn nghĩ tôi đã bỏ lỡ một framework JavaScript, thư viện hoặc công cụ nào đáng để đề cập, hãy cho tôi biết thông qua phần bình luận nhé. 


-----
Tham khảo:
- [Roadmap to becoming a web developer in 2021](https://github.com/kamranahmedse/developer-roadmap)
- [Những thư viện và framework JavaScript quan trọng bạn cần biết](https://code.tutsplus.com/vi/articles/essential-javascript-libraries-and-frameworks-you-should-know-about--cms-29540)
- [The 40 Best JavaScript Libraries and Frameworks for 2021](https://kinsta.com/blog/javascript-libraries/)
- [42 Thư Viện Và Framework Javascript Hay Dành Cho Front-end Developer](https://www.niemvuilaptrinh.com/article/20-thu-vien-javascript-danh-cho-front-end-developer)
- [Essential JavaScript Libraries and Frameworks You Should Know About](https://www.4elements.com/nl/blog/read/essential_javascript_libraries_and_frameworks_you_should_know_about/)
- [Top 5 JavaScript frameworks cho Lập trình Front-end 2020](https://nordiccoder.com/blog/javascript-frameworks/)
- [Top 10 JavaScript Frameworks thông dụng năm 2020](https://itguru.vn/blog/top-10-javascript-framework-thong-dung/)
- [Những thư viện và framework của JavaScript mà bạn không thể bỏ qua](https://topdev.vn/blog/thu-vien-va-framework-cua-javascript/)
- [Những thư viện và framework của JavaScript mà bạn không thể bỏ qua](https://code.tutsplus.com/vi/articles/essential-javascript-libraries-and-frameworks-you-should-know-about--cms-29540)
- [Modules, cách tiệp cận tương lai cho thư viện JavaScript](https://code.tutsplus.com/articles/modules-a-future-approach-to-javascript-libraries--cms-21800)

