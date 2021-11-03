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






-----
Tham khảo:
- [Roadmap to becoming a web developer in 2021](https://github.com/kamranahmedse/developer-roadmap)
- [Những thư viện và framework JavaScript quan trọng bạn cần biết](https://code.tutsplus.com/vi/articles/essential-javascript-libraries-and-frameworks-you-should-know-about--cms-29540)
- [The 40 Best JavaScript Libraries and Frameworks for 2021](https://kinsta.com/blog/javascript-libraries/)