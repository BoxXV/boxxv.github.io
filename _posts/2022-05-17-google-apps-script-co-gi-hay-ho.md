---
layout: post
title: Google Apps Script có gì hay ho?!
subtitle: Google Apps Script

tags:
- Google Apps Script
- Google Sheets Macros
- css
- node
---

![Google Apps Script](https://boxxv.github.io/img/posts/1_J6Qm1Gr3RaG1oVPW5v4-0Q.png "Google Apps Script")

Một ngày đẹp trời công ty bạn chuyển từ hệ thống mail cũ sang Gsuite - một dịch vụ điện toán đám mây với các công cụ phần mềm cộng tác được cung cấp bởi Google dành cho doanh nghiệp, lúc đó vấn đề gặp phải là: những dữ liệu trước đây đã từng được chia sẻ và đồng bộ với tài khoản gmail cá nhân của bạn nay phải chuyển qua tài khoản email gsuite của công ty. Bạn sẽ đi vào từng thư mục và từng file để thay đổi quyền chia sẻ bằng tay ư? Hãy quên chuyện đó đi. Google Apps Scripts sẽ giúp bạn. Nó là gì mà có vẻ lợi hại quá vậy? Cùng tìm hiểu nhé. 😉

### Google Apps Script là gì?

Google Apps Script - đọc qua cái tên thì ta cũng có thể mường tượng được chức năng của nó: là 1 ngôn ngữ lập trình dựa trên Javascript với trình biên tập, biên dịch đều nằm trên máy chủ của Google. Với công cụ này bạn có thể lập trình để thao tác, can thiệp trực tiếp đến các dịch vụ của Google.

#### Google Apps Script có thể làm được những gì?

- Thêm menu, dialogs, và thanh sidebar tùy chỉnh vào Google Docs, Sheets và Forms.
- Viết các hàm mở rộng hoặc các macros cho Google Sheets.
- Xuất bản Web Apps - độc lập hoặc tích hợp vào trang web của Google Sites.
- Tương tác với các dịch vụ khác của Google, bao gồm AdSense, Analytics, Lịch, Drive, Gmail và Bản đồ.
- Xây dựng các tiện ích bổ sung để mở rộng Google Docs, Sheets, Slides và Forms và xuất bản chúng lên cửa hàng Add-on.
- Chuyển đổi ứng dụng Android thành một tiện ích bổ sung Android để ứng dụng có thể trao đổi dữ liệu với Google Doc hoặc Sheet của người dùng trên thiết bị di động.
- Xây dựng Chat bot cho Hangout chat

Hiện tại Google Apps Scripts có thể lập trình để thao tác với hầu hết các dịch vụ của Google:

- Calendar (Lịch)
- Contacts (Danh bạ)
- Documents (Tài liệu)
- Drive (Lưu trữ đám mây)
- Forms (Biểu mẫu)
- Gmail (Email)
- Group (Nhóm)
- Language (Dịch)
- Maps (Bản đồ)
- Sites (Trang web)
- Slides (Trình chiếu)
- SpreadSheet (Bảng tính).

Và ở mục demo mình sẽ viết code để thao tác với Google Drive như bài toán đặt ra ở đầu bài. Tuy nhiên trước hết ta hãy tìm các sử dụng nó với bài HelloWorld quen thuộc trong mọi ngôn ngữ lập trình đã nhé. (go)


### Hello World với Google Apps Script

Với Google Apps Script bạn sẽ code mà chẳng cần phải cài cắm gì cả, chỉ cần 1 máy tính có kết nối mạng và 1 tài khoản gmail là có thể bắt đầu được rồi.

1. Truy cập vào [script.google.com](https://script.google.com/home) để mở trình soạn thảo code (trước đó bạn cần đăng nhập 1 tải khoản gmail)
2. Chọn New script và bắt đầu viết code
3. Copy đoạn code sau vào editor

```javascript
/**
 * Creates a Google Doc and sends an email to the current user with a link to the doc.
 */
function createAndSendDocument() {
  // Create a new Google Doc named 'Hello, world!'
  var doc = DocumentApp.create('Hello, world!');

  // Access the body of the document, then add a paragraph.
  doc.getBody().appendParagraph('This document was created by Google Apps Script.');

  // Get the URL of the document.
  var url = doc.getUrl();

  // Get the email address of the active user - that's you.
  var email = Session.getActiveUser().getEmail();

  // Get the name of the document to use as an email subject line.
  var subject = doc.getName();

  // Append a new string to the "url" variable to use as an email body.
  var body = 'Link to your doc: ' + url;

  // Send yourself an email with a link to the document.
  GmailApp.sendEmail(email, subject, body);
}
```










-----
Tham khảo:
- [Google Apps Script có gì hay ho?!](https://viblo.asia/p/google-apps-script-co-gi-hay-ho-07LKX2xElV4)
- [Apps Script](https://workspace.google.com/intl/vi/products/apps-script/)
- [01 Khai báo biến, làm quen với debugger, Logger trong Google Apps Script](https://youtu.be/gGgosi7ITR4?list=PLALCv46JuKEL2CmEzyr9_5bzYYGX2p8a6)
- [Cách tự động hóa Google Sheets với macro](https://quantrimang.com/cach-tu-dong-hoa-google-sheets-voi-macro-163586)
- [Hướng dẫn chi tiết cách ghi Macro trong Google Sheets](https://gitiho.com/blog/huong-dan-chi-tiet-cach-ghi-macro-trong-google-sheets.html)