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

### Npm là gì và tại sao nó lại quan trọng?

Node Package Manager, hoặc npm (thường được viết bằng chữ thường) là một trong những công cụ tạo và quản lý các thư viện được sử dụng phổ biến nhất trong các dự án JavaScript. Nó được xây dựng trên Node và rất mạnh mẽ nên hầu như tất cả mọi người đều đang sử dụng nó.

#### Công cụ quản lý thư viện là gì?

Hãy tưởng tượng rằng bạn bao gồm thư viện **A** để tùy chỉnh một trường văn bản. Thư viện đó sử dụng thư viện **B** để định dạng văn bản và thư viện **C** để hiển thị các bản dịch.

Hãy tưởng tượng rằng, cùng một lúc, thư viện **C** sử dụng năm thư viện khác nhau để xử lý các ngôn ngữ khác nhau và bạn kết thúc với một lược đồ như thế này.

![npm](https://boxxv.github.io/img/posts/dependency-tree.png "Node Package Manager")

Đó được gọi là _cây phụ thuộc_ của ứng dụng của bạn.





-----
Tham khảo:
- [How to Create an npm Package Ready to Distribute From Scratch](https://bugfender.com/blog/how-to-create-an-npm-package/)