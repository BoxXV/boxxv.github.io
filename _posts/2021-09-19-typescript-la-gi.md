---
layout: post
title: Tìm hiểu về TypeScript
subtitle: What Is TypeScript? Pros and Cons of TypeScript vs. JavaScript
image: "img/js.jpg"
tags:
- CSDL
- Database
- Schema
- Multiple Types
---

![TypeScript](https://boxxv.github.io/img/posts/typescript-la-gi-uu-va-nhuoc-diem-cua-typescript-4.png "TypeScript")

Hôm nay chúng ta sẽ cùng nhau phân tích cặn kẽ điểm mạnh và điểm yếu của typescript để có thể quyết định xem nên sử dụng nó như thế nào cho hiệu quả nhé!


# Định nghĩa Typescript là gì?

![TypeScript](https://boxxv.github.io/img/posts/TypeScript-JavaScriptPlusTypes.webp "TypeScript")

Là một ngôn ngữ được Microsoft tặng free cho chúng ta, nền tảng của TypeScript ít nhiều cũng có sự liên quan đến JavaScript vì nó là một ngôn ngữ mã nguồn mở của JavaScript. Vai trò của TypeScript là dùng để thiết kế và xây dựng các dự án ứng dụng quy mô lớn mang tính chất phức tạp.

Khác với sự đơn giản của JavaScript, du TypeScript cũng đồng thời kế thừa nhiều định nghĩa, khái niệm của đa dạng các ngôn ngữ C#, Java,… nhưng TypeScript lại có yêu cầu cao về trật tự rõ ràng.

TypeScript được xem là một phiên bản nâng cao hơn của JavaScript vì nó được thiết kế thêm nhiều chức năng tiện lợi hơn, cải tiến hơn từ những điểm yếu của JavaScript như các lớp hướng đối tượng và Static Structural typing, bên cạnh đó TypeScript còn có thể hoạt động rộng rãi cho các ứng dụng của ngôn ngữ Angular2 và Nodejs.

## Lợi thế của việc sử dụng TypeScript

JavaScript đã đủ tốt và bạn có thể tự hỏi: Liệu tôi có thực sự cần học TypeScript? Về mặt kỹ thuật, bạn không cần học TypeScript để trở thành một lập trình viên giỏi, hầu hết mọi người đều ổn mà không có nó. Tuy nhiên, làm việc với TypeScript có một số lợi thế sau:

- Với static typing, code viết bằng TypeScript dễ dự đoán hơn, và dễ debug hơn.
- Dễ dàng tổ chức code cho các ứng dụng cực lớn và phức tạp nhờ modules, namespaces và hỗ trợ OOP mạnh mẽ.
- TypeScript có một bước biên dịch thành JavaScript, sẽ bắt tất cả các loại lỗi trước khi chúng chạy và làm hỏng một vài thứ.
- Framework Angular 2 viết với TypeScript và nó cũng khuyến khích các lập trình viên sử dụng ngôn ngữ này trong các dự án của họ.


# Chức năng của TypeScript

## Static Typing

### Các kiểu dữ liệu được sử dụng phổ biến

- **Any** – Một biến với kiểu này có thể có giá trị là một string, number hoặc bất kỳ kiểu nào.
- **String** – Giống chức năng của string trong JavaScript, có thể được bao quanh bởi ‘dấu nháy đơn’ hoặc “dấu nháy kép”.
- **Number** – Tất cả giá trị số trong hàm đều được biểu diễn bởi kiểu number, không có định nghĩa riêng cho số nguyên (interger), số thực (float) cũng như các kiểu khác.
- **Boolean** – true hoặc false, sử dụng 0 và 1 sẽ gây ra lỗi biên dịch.
- **Arrays** – Có 2 kiểu cú pháp: my_arr: number[]; hoặc my_arr: Array<number>.
- **Void** – sử dụng khi hàm không trả lại bất kỳ giá trị nào.

## Interfaces

## Classes

## Modules

## Generics


## Cài đặt TypeScript

Cách dễ nhât để thiết lập TypeScript là thông qua npm. Sử dụng lệnh dưới đây có thể cài đặt TypeScript package toàn cục, giúp cho trình biên dịch TypeScript có thể sử dụng trong mọi dự án của chúng ta:

```bat
npm install -g typescriptjavascript:void(0)
```

Thử mở một cửa sổ terminal ở bất kỳ đâu và chạy lệnh **tsc -v** , nếu cài đặt thành công màn hình sẽ như thế này:

```bat
tsc -v
Version 1.8.10
```

# Hiển thị “Hello, World!” trong TypeScript






-----
- [Tìm hiểu về TypeScript](https://topdev.vn/blog/typescript-la-gi/)
- [TypeScript là gì?](https://viblo.asia/p/typescript-la-gi-yMnKMRBjZ7P)
- [Làm quen với TypeScript](https://viblo.asia/p/javascript-lam-quen-voi-typescript-gGJ59QkP5X2)
- [So sánh Typescript với JavaScript](https://topdev.vn/blog/so-sanh-typescript-voi-javascript/)
- [Giới thiệu Typescript - Sự khác nhau giữa Typescript và Javascript](https://viblo.asia/p/gioi-thieu-typescript-su-khac-nhau-giua-typescript-va-javascript-LzD5dDn05jY)
- [Typescript là gì? Ưu và nhược điểm của Typescript](https://topdev.vn/blog/typescript-la-gi-uu-va-nhuoc-diem-cua-typescript/)
- [What Is TypeScript? Pros and Cons of TypeScript vs. JavaScript](https://www.stxnext.com/blog/typescript-pros-cons-javascript/)
- [Tại sao sử dụng TypeScript ?](https://viblo.asia/p/tai-sao-su-dung-typescript-L4x5xAq1KBM)
- [Tại sao TypeScript là lựa chọn tốt nhất để viết Frontend?](https://itnavi.com.vn/blog/tai-sao-typescript-la-lua-chon-tot-nhat-de-viet-frontend)
- [TypeScript - P1: Vì sao TypeScript được yêu thích đến vậy?](https://viblo.asia/p/typescript-p1-vi-sao-typescript-duoc-yeu-thich-den-vay-1Je5E79LZnL)
- [Một ít về type script](https://viblo.asia/p/mot-it-ve-type-script-3Q75w6n3lWb)
- [TypeScript luồng gió mới cho ngôn ngữ Client](https://viblo.asia/p/typescript-luong-gio-moi-cho-ngon-ngu-client-l5XRBVz4RqPe)

- [Cài đặt TypeScript](https://viblo.asia/p/cai-dat-typescript-QpmleRMM5rd)
- [Hiển thị “Hello, World!” trong TypeScript](https://viblo.asia/p/hien-thi-hello-world-trong-typescript-Eb85oAz8Z2G)
- [Sử dụng class trong TypeScript](https://viblo.asia/p/su-dung-class-trong-typescript-bJzKmAbDK9N)
- [Class trong TypeScript](https://viblo.asia/p/class-trong-typescript-4dbZNkaklYM)
- [TypeScript - Hành trình OOP (1)](https://viblo.asia/p/typescript-hanh-trinh-oop-1-yMnKM6pzZ7P)
- [Modules Trong TypeScript](https://viblo.asia/p/modules-trong-typescript-Qpmlez3k5rd)
- [Một số mẹo và thủ thuật TypeScript](https://viblo.asia/p/mot-so-meo-va-thu-thuat-typescript-Ljy5VWq9Kra)

- [Using TypeScript to implement Multi-Platform Libraries](https://www.dotnetcurry.com/typescript/1370/typescript-nodejs-target-multi-platform-libraries)
- [Multi-Platform Distribution with TypeScript](https://www.sitepen.com/blog/multi-platform-distribution-with-typescript)
- [Cross-Compatible Typescript Libraries (browser and Node.js)](https://blog.unterholzer.dev/cross-compatible-typescript-libraries/)
- [Writing Your Own TypeScript CLI](https://betterprogramming.pub/writing-your-own-typescript-cli-6f9c5688ad34)

- [7 lý do bạn không nên sử dụng TypeScript](https://topdev.vn/blog/7-ly-do-ban-khong-nen-su-dung-typescript/)
- [Fullstack App With TypeScript, PostgreSQL, Next.js, Prisma & GraphQL: Image upload](https://www.prisma.io/blog/fullstack-nextjs-graphql-prisma-4-1k1kc83x3v)
- [typescript on viblo](https://viblo.asia/tags/typescript)
- [quandv on viblo](https://viblo.asia/u/quandv)