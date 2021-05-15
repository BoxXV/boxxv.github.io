---
layout: post
title: Pass by Value và Pass by Reference trong Java
subtitle: Vì một tương lai lương Java cao ngất
tags:
- Java
- Interview
---

Hôm trước có bắt gặp cuộc tranh luận nảy lửa trên một group Skype về Java Developer. Nội dung tranh luận xoay quanh việc Java có `pass-by-reference` hay không.

Trước khi trả lời câu hỏi này, chúng ta cần hiểu sự khác biệt giữa `pass-by-value` (tham trị) và `pass-by-reference` (tham chiếu)

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/0_q5Tkq9ctyYd0gd1F.gif "Pass by Value và Pass by Reference trong Java")_Pass by Value và Pass by Reference trong Java_

## Pass-by-value

`Pass-by-value` được hiểu là khi bạn pass biến vào làm argument cho một function, chương trình sẽ không dùng thẳng biến đó mà sao chép giá trị và đưa cho function, và hệ quả là dù bên trong function xảy ra chuyện gì thì biến thực tế vẫn được bảo toàn

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_gZpx1_-g6SNPmtjET0eHSQ.webp "Pass by Value và Pass by Reference trong Java")



Tham khảo:
- [String concatenate, StringBuilder hay StringBuffer](https://luanvv.com/blog/string-concatenate-stringbuilder-hay-stringbuffer/)
- [Why String is Immutable in Java](https://dzone.com/articles/why-string-immutable-java)
