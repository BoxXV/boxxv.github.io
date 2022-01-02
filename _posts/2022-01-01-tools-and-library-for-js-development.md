---
layout: post
title: Công cụ và Thư viện cần thiết cho Fullstack
subtitle: Tools and Library required for Fullstack

tags:
- JavaScript
- frontend
- roadmap
---

Khi chúng tôi bắt đầu phát triển, chúng tôi có rất nhiều câu hỏi liên quan đến những công cụ nào và những thư viện khác nhau nên được sử dụng: Editor, Module format, HTML generation, Transpiling, Project structure, HTTP, Production build, Bundler, Linting, Testing?

Hãy nói về các phương pháp hay nhất và thiết lập để thiết lập phát triển nhanh cho các nhà phát triển.


### JavaScript Editor

![JavaScript Editor](https://boxxv.github.io/img/posts/large.jpg "JavaScript IDE")

Atom, Visual Studio Code, Eclipse, Sublime Text, Brackets, NetBeans, Vim, Webstorm .v.v.

Biên tập viên JavaScript: Tìm kiếm gì. Hỗ trợ ES2015 + mạnh mẽ
- Tự động hoàn thành
- Phân tích cú pháp nhập ES6
- Báo cáo hàng nhập chưa sử dụng
- Tự động tái cấu trúc / Tự động nhất quán thông qua Editorconfig Framework thông minh Tích hợp trong thiết bị đầu cuối


### Package Managers

![Package Managers](https://boxxv.github.io/img/posts/npmvsyarn.png "Package Managers")

Yarn, tuyên bố rằng npm tốt nhất tại Quản lý phụ thuộc. Yarn cực kỳ đơn giản để cài đặt và sử dụng. Nó cài đặt hơn npm và thay thế npm trong thiết bị đầu cuối của bạn. Bạn có thể cài đặt nó bằng Bash hoặc npm hoặc bất kỳ phương pháp nào khác được liệt kê ở [đây](https://classic.yarnpkg.com/en/docs/install#windows-stable).

Theo thông báo của Facebook, nhu cầu ngay lập tức đối với Yarn là sự phụ thuộc của npm vào việc có kết nối internet đang hoạt động, điều này đã phá vỡ Tích hợp liên tục trên môi trường Sandbox ngoại tuyến của họ, tức là cài đặt npm không hoạt động nếu Môi trường của bạn ngoại tuyến.


### Tự động hóa Workflow & tasks

![Automation of Workflow & tasks](https://boxxv.github.io/img/posts/1 3cPPzqyp-g_JeMsFJQS8dA.png "Automation of Workflow & tasks")

Theo thời gian, tôi đã nhận thấy ba vấn đề cốt lõi với những người chạy nhiệm vụ như Gulp và Grunt:
- Sự phụ thuộc vào tác giả plugin
- Gỡ lỗi khó chịu
- Tài liệu rời rạc

Gulp có ~ 2.100 plugin.
Grunt có ~ 5.400.
npm cung cấp hơn 227.000 gói, tăng với tốc độ hơn 400 hàng ngày.


### Transpilers

![Transpilers](https://boxxv.github.io/img/posts/1 oxn0OoAavba8pyykZTbYCg.png "Transpilers")

Transpilers , hoặc trình biên dịch từ source-to-source, là công cụ đọc mã nguồn được viết bằng một ngôn ngữ lập trình và tạo ra mã tương đương bằng một ngôn ngữ khác. Các ngôn ngữ bạn viết chuyển tiếp sang JavaScript thường được gọi là ngôn ngữ compile-to-JS và được cho là nhắm mục tiêu JavaScript.

`Babel` có khả năng sắp xếp các đầu ra dài dòng ở dạng con người có thể đọc được, do đó, việc gỡ lỗi mã của bạn trở nên dễ dàng hơn. Công cụ này cũng có rất nhiều plugin có sẵn cho nó. Một số plugin quan trọng mà bạn có thể thấy mình đang sử dụng là: ES2015, ES2016, ES2017 và React. Babel cũng có một bộ plugin được gọi là “mới nhất” được cập nhật thường xuyên với tất cả các công cụ có thể có mà một người có thể cần để cập nhật những cải tiến mới nhất trong JS.

Tự động hoàn thành nâng cao `TypeScript`, Khả năng đọc nâng cao, Tái cấu trúc an toàn hơn Các tính năng không chuẩn khác Babel Viết JS chuẩn hóa Đòn bẩy Hệ sinh thái JS đầy đủ Sử dụng các tính năng thử nghiệm trước đó Không có định dạng loại, chú thích cần nhập ES6 là Kiểm tra có thể phân tích tĩnh, Lint, Babel, Great libs, IDE = an toàn


### Bundler

![Bundler](https://boxxv.github.io/img/posts/1 GMJ6QEWQWSaaIgS528GT9A.png "Bundler")

#### Module patterns
Một số định dạng được điều chỉnh rộng rãi và nổi tiếng là:
- Biểu thức hàm được gọi ngay lập tức (IIFE)
- Định nghĩa mô-đun không đồng bộ (AMD)
- CommonJS
- Định nghĩa mô-đun chung (UMD)
- System.register
- Định dạng mô-đun ES6

#### Module loaders

![Module loaders](https://boxxv.github.io/img/posts/1 pub7A-2Q39L7A04JAiQjlQ.png "Module loaders")



-----
Tham khảo:
- [Tools and Library required for Fullstack](https://tkssharma.com/tools-and-library-for-js-development/)
- [Choosing the Best JavaScript Editor From 7 Options](https://www.testim.io/blog/best-javascript-editor-6-options/)
- [Best JavaScript IDE & Source Code Editors to Use](https://hackr.io/blog/best-javascript-ide-source-code-editors)
- [Why I Left Gulp and Grunt for npm Scripts](https://www.freecodecamp.org/news/why-i-left-gulp-and-grunt-for-npm-scripts-3d6853dd22b8/)

