---
layout: post
title: Tạo thư viện JavaScript hiện đại
subtitle: Tạo gói npm sẵn sàng phân phối từ đầu
tags:
- Tips
- Tricks
- JavaScript
- library
---

# Introduction

Sử dụng hệ sinh thái JavaScript hiện đại, về phần lớn, là một trải nghiệm khá tốt. Chắc chắn, có thể có quá nhiều frameworks để đếm, nhưng nếu bạn đã sử dụng JS đủ lâu, bạn đã biết chính xác gói nào mình sẽ sử dụng trong mỗi dự án mới và tệ nhất là bạn sẽ sử dụng một cái gì đó như Tạo Ứng dụng React để đi tắt đón đầu.

{% highlight js %}
// Magic! React now works
import React from 'react';
{% endhighlight %}

Mặc dù việc sử dụng các thư viện rất đơn giản, nhưng việc tạo và duy trì một thư viện có thể là một cơn ác mộng tuyệt đối. 


## The problem

Bạn cần hỗ trợ càng nhiều phiên bản của nhiều nền tảng khác nhau càng tốt để làm hài lòng người dùng của mình. Ngay cả khi bạn đang tạo một gói chỉ cho Node.js hoặc chỉ các trình duyệt, việc xuất hoạt động bình thường có thể rất khó khăn.

{% highlight js %}
// ES Modules
import myPackage from 'my-package';

// CommonJS
const myPackage = require('my-package');

// UMD
document.write('<script src="//unpkg.com/my-package"></script>');
{% endhighlight %}

Bạn muốn giảm thiểu kích thước gói cho người dùng trình duyệt, nhưng có rất ít tài nguyên mô tả cách tốt nhất để làm như vậy. Nếu thư viện của bạn nhiều hơn một trăm kilobyte, người dùng của bạn sẽ phàn nàn rằng bây giờ phải mất thêm một hoặc hai giây để tải trang web của họ trên một thiết bị di động rẻ tiền.

Bạn có thể muốn hỗ trợ người dùng TypeScript và Flow bằng cách thêm các kiểu đánh máy cho gói của mình, nhưng vẫn chưa rõ liệu bạn có nên thêm chúng vào DefiniedlyTyped / flow-typed hay không hay đưa chúng vào gói của mình. Nếu bạn không quen thuộc với TypeScript hoặc Flow, việc quản lý các loại khi thư viện của bạn phát triển có thể trở nên cực kỳ khó khăn.

Có rất nhiều mối quan tâm khác. Làm thế nào để bạn viết tài liệu tốt? Làm cách nào để bạn sửa lỗi nhanh chóng và quản lý các vấn đề khi chúng bắt đầu chồng chất? Làm thế nào để bạn khuyến khích sự đóng góp của cộng đồng? Làm thế nào để bạn làm cho thư viện của bạn dễ hiểu cho người mới? 


## Tại sao phải nghe những lời đề nghị của tôi?

Nói ngắn gọn: Tôi đã làm việc trên [Parcel](https://github.com/parcel-bundler/parcel) trong vài tháng và do đó đã tìm hiểu rất sâu về các chi tiết nhỏ của việc làm cho một gói thân thiện với người dùng gói. Tôi cũng đã xuất bản và duy trì các gói thành công khác nhau, trong đó phổ biến nhất là [thư viện nén hiệu suất cao](https://github.com/101arrowz/fflate) đạt hơn 4 triệu lượt tải xuống trong 6 tháng và hiện đang phụ thuộc vào các dự án lớn như SheetJS và Three.js. Tôi đã giải quyết nhiều vấn đề mà các tác giả thư viện mới gặp phải nhiều lần, vì vậy tôi đã quen với các cách giải quyết.


## Giải pháp

Loạt bài này sẽ mô tả những điều nên làm và không nên khi tạo một thư viện JavaScript mà người dùng của bạn sẽ thích sử dụng và bạn sẽ thích duy trì. Ngay cả khi bạn không có kế hoạch tạo thư viện sớm, những bài viết này sẽ giúp bạn tìm hiểu thêm về hệ sinh thái JavaScript và nhiều điều kỳ quặc của nó. Đừng lo lắng về việc làm theo bất kỳ thứ tự cụ thể nào; bạn sẽ không cần phải đọc bất kỳ mục nào trong loạt bài này để hiểu phần tiếp theo. Tôi hy vọng thông tin này sẽ giúp bạn thiết kế phần bổ sung tuyệt vời tiếp theo cho hệ sinh thái JS!


# Writing good code

Không thể gán một định nghĩa cố định cho "`good code`", nhưng hầu hết thời gian trong thế giới JS, chúng tôi muốn nói đến mã đó là:
- Không có lỗi
- Linh hoạt
- Có thể đọc được
- Nhanh
- Nhỏ

Theo thứ tự đó. Đối với thư viện, bạn có thể chọn chuyển khả năng đọc xuống cuối danh sách, nhưng đó có lẽ không phải là động thái tốt nhất nếu bạn muốn người khác giúp bạn duy trì dự án của mình. Bây giờ, chúng ta hãy xem từng khía cạnh của "mã tốt" bao gồm những gì.

Xin hãy nhớ rằng, đây hoàn toàn là ý kiến của riêng tôi: vui lòng bỏ qua nó hoàn toàn. Mọi người nên có định nghĩa của riêng mình về "các phương pháp hay nhất".


## Viết mã không có lỗi

![Writing bug-free code](https://boxxv.github.io/img/posts/new_bug.png "Writing bug-free code")




-----
Tham khảo:
- [Creating a modern JS library: Introduction](https://dev.to/101arrowz/creating-a-modern-js-library-introduction-1a0c)
- [Creating a modern JS library: Writing good code](https://dev.to/101arrowz/creating-a-modern-js-library-writing-good-code-170a)
- [Creating a modern JS library: TypeScript and Flow](https://dev.to/101arrowz/creating-a-modern-js-library-typescript-and-flow-3ge)
- [Creating a modern JS library: package.json and dependencies](https://dev.to/101arrowz/creating-a-modern-js-library-package-json-and-dependencies-5ek9)