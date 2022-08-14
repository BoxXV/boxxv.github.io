---
layout: post
title: Tìm hiểu về Technical Stack
subtitle: Cách Chọn Công Nghệ Phù Hợp Cho Doanh Nghiệp Của Bạn

tags:
- Technical Stack
- MERN
- MEAN
- MEVN
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

Một stack cũng khá nổi trong vài năm trở lại đây là MEAN stack. Nó bao gồm: MongoDB, Express, AngularJS, NodeJS.

Thật ra stack này không hoàn toàn đúng chuẩn stack vì nó không bao gồm hệ điều hành. NodeJS dùng để viết code server-side, có thể hoạt động như web server luôn (Trong thực tế người ta thường dùng thêm nginx làm proxy server).

Cũng như LAMP Stack, toàn bộ các thành phần của MEAN Stack đều là hàng Open Source. Điểm “hay ho” của stack này là toàn bộ các thành phần của nó đều sử dụng ngôn ngữ JavaScript.

Điều này đồng nghĩa với việc bạn có thể xây dựng toàn bộ một hệ thống chỉ bằng một ngôn ngữ duy nhất, chạy ở cả front-end và back-end, tiết kiệm thời gian và chi phí.

## MERN Stack



## MEVN Stack


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