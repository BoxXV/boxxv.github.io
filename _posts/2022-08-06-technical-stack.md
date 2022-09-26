---
layout: post
title: Tìm hiểu về Technical Stack
subtitle: Cách Chọn Công Nghệ Phù Hợp Cho Doanh Nghiệp Của Bạn

tags:
- Technical Stack
- Web Stack
- MERN
- MEAN
- MEVN
- WISA
- LAMP
---

![Technical Stack](https://boxxv.github.io/img/2022/d4e7f08b71cf52785843342351f223f1.png "Technical Stack")

Lang thang trên mạng, ta thường nghe nhắc đến những một số thuật ngữ như LAMP Stack, MEAN Stack. Trong quá trình xây dựng sản phẩm start-up, ta cũng hay nghe nhắc tới tầm quan trọng của việc chọn technical stack cho phù hợp.

Đã có bao giờ bạn thắc mắc về ý nghĩa của những thuật ngữ này chưa? Hãy cùng tìm hiểu qua bài viết này nhé!

## Stack là gì, tại sao nó ra đời?

Để làm ra một ứng dụng hoàn chỉnh, chỉ viết code không thôi là không đủ. Khi cần lưu trữ thông tin, ta phải đưa chúng vào cơ sở dữ liệu. Sau khi đã hoàn thành phần code, ta phải tìm cách deploy nó, tức là đưa code lên một chỗ nào đó để chạy code.

Một chương trình hoàn thiện không chỉ có code, mà còn phải có nền tảng hệ điều hành và những phần mềm đi kèm (web server, cơ sở dữ liệu). Người ta gom những thứ này lại với nhau (giống như ráp Lego ấy), tạo thành technical stack.

Technical Stack, còn gọi là solution stack, là một tập hợp những phần mềm/công nghệ phối hợp chung với nhau, tạo thành một nền tảng để ứng dụng có thể hoạt động được.


### Cấu tạo của Stack ra sao?

Một stack thường được cấu tạo bởi các thành phần:
- Hệ điều hành
- Web Server
- Database Server
- Back-end Programming Language

Giả sử với LAMP Stack, các thành phần này sẽ lần lượt là:
- Linux
- Apache
- MySQL hoặc  MariaDB
- PHP hoặc Python

Mỗi thành phần trong stack đảm nhận một nhiệm vụ riêng biệt.

Giả sử với LAMP stack, máy chủ sẽ chạy hệ điều hành Linux, cài server Apache Tomcat. Khi có request từ người dùng, server sẽ gọi code PHP, code này đọc dữ liệu từ cơ sở dữ liệu MySQL, render ra HTML về phía người dùng.

Thông thường, với các host trên mạng (somee, hawkhost, digital ocean) họ cung cấp sẵn toàn bộ stack (os, web server và database), các bạn chỉ việc up code lên và chạy thôi.

Nếu muốn tìm hiểu cách stack hoạt động, các bạn hãy thử kiếm một con VPS chạy Linux, sau đó tự cài đặt các phần mềm cần thiết. Thú vị lắm đấy ;).


### Lựa chọn software stack theo tiêu chí nào?

Thông thường, người ta lựa chọn stack dựa vào khả năng, trình độ của nhân viên. Ví dụ  cácnhân viên đã quen code PHP thì cứ LAMP Stack mà táng, nhân viên khoái hàng Microsoft thì dùng Stack của Microsoft thôi.

Ngoài ra, người ta còn lựa chọn Stack dựa theo tốc độ phát triển ứng dụng hay tốc độ xử lý. Thuở mới start-up, Twitter chọn stack dựa trên Ruby on Rails để phát triểu ứng dụng nhanh chóng. Sau đó, họ chuyển qua Stack dùng Java/Scala để tăng khả năng chịu tải của hệ thống ([Nguồn](https://www.theregister.co.uk/2012/11/08/twitter_epic_traffic_saved_by_java/)).

Lựa chọn technical stack là một điều quan trọng bậc nhất khi bắt đầu xây dựng sản phẩm. Nó xác định kiến trúc hệ thống, chi phí vận hành cũng như tốc độ và khả năng mở rộng của ứng dụng.

Do vậy, chúng ta sẽ cùng tìm hiểu về một số stack thông dụng, cùng với những ưu nhược điểm của chúng ở phần dưới nhé!

-----

Sau đây là một số stack thông dụng

## LAMP Stack

![LAMP Stack](https://boxxv.github.io/img/2022/lamp.jpg "LAMP Stack")

Đây là stack thông dụng nhất, được hầu hết các website sử dụng. Stack này bao gồm: Linux, Apache, MySQL và PHP/Python/Perl. Những CMS phổ biến như Joomla, WordPress đều dựa trên nền stack này cả.

Điểm “hay ho” của Stack này là những thành phần của nó đều Open Source, không cần phải bỏ đồng nào ra mua, chi phí bản quyền bằng 0. Cộng đồng người sử dụng rất nhiều nên bạn rất dễ dàng tìm hướng dẫn khi gặp vấn đề.

Các máy chủ cài đặt Linux giá cả cũng rất hạt dẻ. Do đó, nếu code trên LAMP Stack, các bạn có thể dễ dàng tìm host free cho ứng dụng của mình.

Stack này còn có một số dị bản như: MAMP (Trên MAC), WAMP( Trên Win), XAMPP (Trên mọi hệ điều hành).


## WISA Stack

![WISA Stack](https://boxxv.github.io/img/2022/LAMP-Stack-vs.-WISA-Stack.jpg "WISA Stack")

Stack này bao gồm: Window, IIS, SQL Server, ASP.NET. Có thể thấy, toàn bộ stack sử dụng hàng của Microsoft.

Stack này được nhiều công ty, tổ chức sử dụng. Thông thường những ứng dụng được code trên nền tảng ASP.NET sẽ lựa chọn stack này.

Ưu điểm của stack này là tốc độ phát triển ứng dụng và khả năng bảo trì: C# là một ngôn ngữ khá mạnh mẽ, ASP.NET làm việc rất tốt với SQL Server, có nhiều tool hỗ trợ tận răng cho người dùng.

Tuy vậy, sử dụng hàng của Microsoft thì chi phí bản quyền (mua Visual Studio để code, bản quyền Window, SQL Server) khá cao, do đó các công ty nhỏ thường không sử dụng.

Gần đầy, C# đã trở thành ngôn ngữ Open Source. Cách đây không lâu .NET Core ra đời, SQL Server cũng đã có mặt trên Linux. Biết đâu không lâu sau chúng ta sẽ có một stack miễn phí chạy trên Linux với công nghệ của Microsoft thì sao ;).


## MEAN Stack

![MEAN Stack](https://boxxv.github.io/img/2022/1_ocOSqSFc_j0rhAaBl-g_0g.png "MEAN Stack")

Một stack cũng khá nổi trong vài năm trở lại đây là MEAN stack. Nó bao gồm: MongoDB, Express, AngularJS, NodeJS.

Thật ra stack này không hoàn toàn đúng chuẩn stack vì nó không bao gồm hệ điều hành. NodeJS dùng để viết code server-side, có thể hoạt động như web server luôn (Trong thực tế người ta thường dùng thêm nginx làm proxy server).

Cũng như LAMP Stack, toàn bộ các thành phần của MEAN Stack đều là hàng Open Source. Điểm “hay ho” của stack này là toàn bộ các thành phần của nó đều sử dụng ngôn ngữ JavaScript.

Điều này đồng nghĩa với việc bạn có thể xây dựng toàn bộ một hệ thống chỉ bằng một ngôn ngữ duy nhất, chạy ở cả front-end và back-end, tiết kiệm thời gian và chi phí.

## MERN Stack

![MERN Stack](https://boxxv.github.io/img/2022/VS--1-.jpg "MERN Stack")

MERN là một thuật ngữ rút gọn của MongoDB, Express, React và Node. Stack MERN là một stack Javascript được thiết kế để giúp phát triển ứng dụng web toàn ngăn xếp dễ dàng hơn và nhanh hơn.

Tất cả bốn công nghệ này cung cấp một khuôn khổ hoàn chỉnh cho các nhà phát triển để tạo ra bất kỳ ứng dụng web nào. MERN đang tuân theo kiến ​​trúc 3 tầng truyền thống, bao gồm tầng hiển thị front-end (React.js), tầng ứng dụng (Express.js và Node.js) và tầng cơ sở dữ liệu (MongoDB)

MongoDB có thể cung cấp khả năng mở rộng cao hơn, Express.js để nâng cao tốc độ, JavaScript là ngôn ngữ cơ bản để phát triển từ đầu đến cuối; MERN là một trong những bộ phát triển full-stack tốt nhất sau MEAN.

React.js rất tuyệt khi nói đến tính trừu tượng của lớp giao diện người dùng. Nó có các công cụ tốt nhất để phát triển mã nhanh hơn. Mặc dù React chỉ là một thư viện, nhưng nó cho phép bạn tự do xây dựng ứng dụng và tổ chức mã theo cách bạn muốn, với các công cụ cần thiết. Do đó, nó tốt hơn Angular.js về hiệu suất và kết xuất giao diện người dùng.

MERN và MEAN tương tự như MongoDB, Express và Node, và điểm khác biệt duy nhất là front end framework, React.js trong MERN và Angular.js trong MEAN.

React là một thư viện có thể giúp bạn tạo giao diện người dùng động một cách dễ dàng. Như đã đề cập trước đó, Nó là một thư viện các công cụ và chức năng có thể giúp thiết kế, phát triển và hiển thị các thành phần giao diện người dùng. React là cách tốt nhất để kiểm soát trạng thái của các sự kiện khi có một lượng lớn dữ liệu động cần được cập nhật. Bởi vì React chỉ là một thư viện, nhà phát triển có trách nhiệm duy trì mã và ứng dụng và thường vẫn chưa được tổ chức thay vì cơ sở mã có hệ thống của Angular.js.

Angular.js là một khung công tác MVC, có một khung hệ thống và kiến ​​trúc cụ thể. Nó giúp làm cho mã và ứng dụng được tổ chức tốt, do đó, dễ bảo trì. Tuy nhiên, angle.js tuân theo mô hình liên kết dữ liệu hai chiều nên khó xử lý, thay đổi các sự kiện đối với một khối lượng lớn dữ liệu.

Cả MERN & MEAN đều là những nền tảng vững chắc để phát triển ứng dụng web, Nhưng nó phụ thuộc vào sở thích của nhà phát triển và tính chất công việc. Tuy nhiên, MERN được ưa thích hơn bởi các dịch vụ phát triển của Magento ngày nay.


## MEVN Stack

![MEVN Stack](https://boxxv.github.io/img/2022/pp,840x830-pad,1000x1000,f8f8f8.u7.jpg "MEVN Stack")

MEVN là viết tắt của MongoDB, Express.js, VueJS, Node.js. 

MEVN Stack là stack phần mềm JavaScript mã nguồn mở đã nổi lên như một cách mới và đang phát triển để xây dựng các ứng dụng web động và mạnh mẽ. Các thành phần phần mềm của nó có thể được sử dụng để thiết kế phát triển giao diện người dùng và phụ trợ một cách hiệu quả và cải thiện chức năng của trang web hoặc ứng dụng của bạn.

- **MongoDB**: Cơ sở dữ liệu không SQL hướng tài liệu, được sử dụng để lưu trữ dữ liệu ứng dụng.
- **ExpressJS**: Một khuôn khổ xếp lớp trên NodeJS, được sử dụng để xây dựng phần phụ trợ của một trang web bằng cách sử dụng các chức năng và cấu trúc NodeJS. Vì NodeJS chủ yếu được phát triển để chạy JavaScript trên máy thay vì tạo trang web, ExpressJS được tạo ra cho mục đích sau này.
- **Vue JS**: VueJS được gọi là khuôn khổ phía máy khách và đặc biệt được sử dụng trong phát triển web front-end. Nó có liên kết dữ liệu hai chiều cho phép phát triển giao diện người dùng liền mạch cùng với khả năng MVC và các ứng dụng phía máy chủ tương tác.
- **NodeJS**: Môi trường thời gian chạy JavaScript. Nó được sử dụng để chạy JavaScript trên máy chứ không phải trong trình duyệt.


## Tổng kết

Mỗi developer sẽ có một technical stack ưa thích. Các bạn cùng chia sẻ về technical stack mà mình hay dùng trong phần comment nha. Nếu có thắc mắc gì, đừng ngại ngùng đặt câu hỏi nhé!


-----
Tham khảo:
- [Technical Stack là cái khỉ gì?](https://toidicodedao.com/2017/05/23/giai-thich-technical-stack-la-gi/)
- [Mỗi người nên có một "Tech Stack" cho riêng mình](https://www.goccuachung.com/moi-nguoi-nen-co-mot-tech-stack-cho-rieng-minh/)
- [Technical Stack](https://hoangtung.blog/2019/06/20/technical-stack/)
- [Technical Stack Là Gì? Định Nghĩa Và Giải Thích Ý Nghĩa Của Từ Stack](https://ingoa.info/tech-stack-la-gi-1640010386/)
- [Tech Stack là gì? 13 Cách Chọn Công Nghệ Phù Hợp Cho Doanh Nghiệp Của Bạn – tech stack là gì](https://phptravels.vn/tech-stack-la-gi-13-cach-chon-cong-nghe-phu-hop-cho-doanh-nghiep-cua-ban-tech-stack-la-gi/)
- [Biztalk Server là gì ? Ưu và nhược điểm của Biztalk Server ?](https://viblo.asia/p/biztalk-server-la-gi-uu-va-nhuoc-diem-cua-biztalk-server-GrLZDkDOKk0)
- [Top Web Development Stacks In 2022: Front-end, Back-end & Database](https://www.angularminds.com/blog/article/top-web-development-stack-for-developers.html)
- [What is a Tech Stack](https://www.apxor.com/blog/what-is-a-tech-stack)
- [A Comprehensive Guide to Modern Web Development Stacks](https://enkonix.com/blog/web-development-stacks/)
- [7 khung JavaScript hàng đầu để tăng tốc phát triển phần mềm của bạn](https://viblo.asia/p/top-7-javascript-frameworks-to-accelerate-your-software-development-eW65GgJj5DO)

-----
MEAN Stack
- [MEAN Stack](https://onexlab-io.medium.com/mean-stack-bd3f479f426)
- [Angular & NodeJS - The MEAN Stack Guide [2022 Edition]](https://www.udemy.com/course/angular-2-and-nodejs-the-practical-guide/)
- [MEAN Stack E-Commerce App: Angular 14, NX, PrimeNg [2022]](https://www.udemy.com/course/mean-stack-ecommerce-app-angular-nx-primeng/)

-----
MERN Stack
- [Giới thiệu MERN Stack](https://viblo.asia/p/gioi-thieu-mern-stack-bWrZnv4vZxw)
- [MERN STACK LÀ GÌ? CÙNG TÌM HIỂU KHÁI NIỆM MERN STACK](https://t3h.com.vn/tin-tuc/mern-stack-la-gi)
- [Khóa học MERN Stack 2021 - React, Redux, Node, Mongo - Dự án thực tế](https://www.codientu.online/2022/02/khoa-hoc-mern-stack-2021-react-redux-node-mongo-du-an-thuc-te.html)
- [Xây dựng và deploy ứng dụng MERN APP - Học Full Stack (React+Redux, NodeJS , Express, MongoDB)](https://youtu.be/khcjRUZCufs)
- [Hướng dẫn Full Stack MERN (MongoDB, Express, React, Node)](https://youtu.be/rgFd17fyM4A)
- [KHOÁ HỌC LẬP TRÌNH MERN STACK 100% DỰ ÁN THỰC TẾ & CHẤT LƯỢNG](https://trungquandev.com/khoa-hoc-lap-trinh-mern-stack-100-du-an-thuc-te-chat-luong/)
- [KHOÁ HỌC LẬP TRÌNH MERN STACK 100% DỰ ÁN THỰC TẾ & CHẤT LƯỢNG](https://www.youtube.com/playlist?list=PLP6tw4Zpj-RKdGMqhYpfdl94cd4fu-RFg)
- [Deploy ứng dụng MERN stack của bạn 1 cách miễn phí 100% (MERN + HNMA)](https://viblo.asia/p/deploy-ung-dung-mern-stack-cua-ban-1-cach-mien-phi-100-mern-hnma-bJzKmAQ6K9N)
- [Xây dựng stack M.E.R.N với app NodeJS – phần 1](https://hocweb.vn/xay-dung-mo-hinh-mern-voi-app-nodejs-phan-1/)
- [Hướng dẫn Deploy website NodeJS lên VPS](https://hocweb.vn/huong-dan-deploy-website-nodejs-len-vps/)
- [How to Use MERN Stack: A Complete Guide](https://www.mongodb.com/languages/mern-stack-tutorial)
- [#21. M.E.R.N STACK, Displaying Alert Messages & Logout, Authentication](https://youtu.be/-Vin4eRTc0A)

-----
MEVN Stack
- [Xây dựng full stack web apps với MEVN Stack [Phần 1/2]](https://viblo.asia/p/xay-dung-full-stack-web-apps-voi-mevn-stack-phan-12-djeZ1xd8KWz)
- [Xây dựng full stack web apps với MEVN Stack [Phần 2/2]](https://viblo.asia/p/xay-dung-full-stack-web-apps-voi-mevn-stack-phan-22-Eb85oBqml2G)
- [Build webapp with ExpressJS - VueJS (Vuex) - MongoDB (CRUD)](https://viblo.asia/p/build-webapp-with-expressjs-vuejs-vuex-mongodb-crud-eW65GE1LZDO)
- [Xây dựng app chat realtime với VueJS - NodeJS - Express - SocketIO](https://viblo.asia/p/xay-dung-app-chat-realtime-voi-vuejs-nodejs-express-socketio-WAyK86bElxX)
- [Xây dựng app chat realtime với VueJS - NodeJS - Express - SocketIO (Phần 2)](https://viblo.asia/p/xay-dung-app-chat-realtime-voi-vuejs-nodejs-express-socketio-phan-2-vyDZO6vaKwj)