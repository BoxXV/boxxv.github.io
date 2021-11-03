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




-----
Tham khảo:
- [Roadmap to becoming a web developer in 2021](https://github.com/kamranahmedse/developer-roadmap)
- [Những thư viện và framework JavaScript quan trọng bạn cần biết](https://code.tutsplus.com/vi/articles/essential-javascript-libraries-and-frameworks-you-should-know-about--cms-29540)
- [The 40 Best JavaScript Libraries and Frameworks for 2021](https://kinsta.com/blog/javascript-libraries/)