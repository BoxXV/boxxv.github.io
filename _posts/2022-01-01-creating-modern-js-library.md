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

`Node Package Manager`, hoặc `npm` (thường được viết bằng chữ thường) là một trong những công cụ tạo và quản lý các thư viện được sử dụng phổ biến nhất trong các dự án JavaScript. Nó được xây dựng trên Node và rất mạnh mẽ nên hầu như tất cả mọi người đều đang sử dụng nó.

#### Công cụ quản lý thư viện là gì?

Hãy tưởng tượng rằng bạn bao gồm thư viện **A** để tùy chỉnh một trường văn bản. Thư viện đó sử dụng thư viện **B** để định dạng văn bản và thư viện **C** để hiển thị các bản dịch.

Hãy tưởng tượng rằng, cùng một lúc, thư viện **C** sử dụng năm thư viện khác nhau để xử lý các ngôn ngữ khác nhau và bạn kết thúc với một lược đồ như thế này.

![npm](https://boxxv.github.io/img/posts/dependency-tree.png "Node Package Manager")

Đó được gọi là _cây phụ thuộc_ của ứng dụng của bạn.

Không sớm thì muộn, dự án của bạn sẽ kết thúc với hàng tá phụ thuộc (bạn thậm chí sẽ không nhận thức được một số trong số chúng). Và điều tồi tệ hơn nữa, mỗi phụ thuộc đó sẽ chỉ tương thích với một số phiên bản cụ thể nhất định.

Tình huống này sẽ là một cơn ác mộng để quản lý thủ công. Một bản cập nhật đơn giản trong một mô-đun con có thể phá vỡ cây phụ thuộc của bạn và ứng dụng của bạn có thể không biên dịch. Đó chính xác là vấn đề mà `npm` giải quyết.

![npm](https://boxxv.github.io/img/posts/dependency-tree-wrong.png "Node Package Manager")

Khi bạn tạo một thư viện `npm`, bạn sẽ tạo một tệp json được gọi `package.json` trong đó bạn chỉ định những phụ thuộc nào mà thư viện JS của bạn có.

Đồng thời, các phụ thuộc trong thư viện của bạn sẽ có các `package.json` tệp riêng của chúng , tạo ra một cây phụ thuộc đầy đủ.

Nếu ai đó muốn thêm thư viện của bạn vào dự án của họ, thì họ sẽ chỉ cần chạy:

```bat
npm install <your-library-package-name>
```




















-----
Tham khảo:
- [How to Create an npm Package Ready to Distribute From Scratch](https://bugfender.com/blog/how-to-create-an-npm-package/)