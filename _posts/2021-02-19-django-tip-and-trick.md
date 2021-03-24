---
layout: post
title: Django Programming Tips & Tricks
subtitle: Thực tiễn hiện đại, Hướng dẫn đầy đủ
tags:
- Csharp
- Tips
- Tricks
- volatile
- Invoke
- InvokeRequired
---

### 1. Đăng ký người dùng nâng cao
Tại thời điểm này, chúng ta đã triển khai đăng ký người dùng Django tiêu chuẩn. Nhưng thường đó chỉ là điểm khởi đầu trong các dự án chuyên nghiệp. Tùy chỉnh mọi thứ một chút thì sao? Ví dụ: mẫu tên người dùng / email / mật khẩu mặc định của Django ngày nay hơi cũ. Phổ biến hơn nhiều là chỉ cần yêu cầu email / mật khẩu để đăng ký và đăng nhập. Và thực sự mọi phần của quy trình xác thực – biểu mẫu, email, trang – đều có thể được tùy chỉnh nếu muốn.

Một yếu tố chính khác trong nhiều dự án là nhu cầu xác thực xã hội, đó là xử lý đăng ký và đăng nhập thông qua dịch vụ của bên thứ ba như Google, Facebook, v.v.

Chúng ta có thể triển khai các giải pháp của riêng mình ở đây từ đầu nhưng có một số rủi ro nhất định: đăng ký người dùng là một khu vực phức tạp với nhiều bộ phận chuyển động và một khu vực mà chúng tôi thực sự không muốn mắc lỗi bảo mật.

Vì lý do này, nhiều nhà phát triển Django chuyên nghiệp dựa vào [django-allauth](https://github.com/pennersr/django-allauth) phổ biến của bên thứ ba. Việc thêm bất kỳ gói bên thứ ba nào cũng nên đi kèm với một mức độ thận trọng vì bạn đang thêm một phần phụ thuộc khác vào ngăn xếp kỹ thuật của mình. Điều quan trọng là đảm bảo bất kỳ gói nào đều được cập nhật và đã được kiểm tra tốt. May mắn thay, `django-allauth` là cả hai.

Với cái giá của một chút ma thuật, nó giải quyết tất cả những mối quan tâm này và làm cho việc tùy chỉnh trở nên dễ dàng hơn nhiều.


-----
Tham khảo:
- [Ý Nghĩa Của Từ Khóa Volatile Trong C](https://ktmt.github.io/blog/2013/05/09/y-nghia-cua-tu-khoa-volatile-trong-c/)
- [Top 16 C# Programming Tips & Tricks](https://www.vn.freelancer.com/community/articles/top-16-c-programming-tips-tricks)
- [Invoke, InvokeRequired trong C# có nghĩa là gì?](http://diendan.congdongcviet.com/threads/t52293::invoke-invokerequired-trong-csharp-co-nghia-la-gi.cpp)
