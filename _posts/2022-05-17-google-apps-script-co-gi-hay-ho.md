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

1) Truy cập vào [script.google.com](https://script.google.com/home) để mở trình soạn thảo code (trước đó bạn cần đăng nhập 1 tải khoản gmail)
2) Chọn New script và bắt đầu viết code
3) Copy đoạn code sau vào editor

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

4) Lưu lại và chọn hàm `createAndSendDocument` để chạy thử.

Kết quả của việc chạy script trên là Google Apps Script sẽ tạo ra 1 file docs với title là `Hello, world!`, nội dung là `This document was created by Google Apps Script.` và gửi về địa chỉ email của bạn.

![Google Apps Script](https://boxxv.github.io/img/posts/c22729cc-57d1-42ee-af13-abeadffc61cc.webp "Google Apps Script")

Như vậy đọc qua đoạn code trên thì ta có thể hiểu được cơ bản cách hoạt động của Google Apps Script. Nhìn code được viết dựa trên Javascript nên rất dễ đọc và dễ hiểu. Ở trên ta thấy có một số Class được cung cấp sẵn như DocumentApp: class để thao tác với Google Document, Session: Dùng để thao tác với các thông tin session đang truy cập, GmailApp: dùng để thao tác với Gmail mà ở trên chính là hành động gửi mail. Xong bài Hello World cơ bản nhất ta sẽ tiếp tục tiến đến bài nâng cao như đầu bài (gogo)


### Demo với Google Drive

Nhắc lại bài toán ở đầu bài thì cơ duyên bắt đầu từ việc Framgia chuyển sang dùng Gsuite và tài liệu các dự án được shared với tài khoản gmail cá nhân của mỗi thành viên giờ đây cần được chuyển sang với email gsuite tương ứng của họ và xóa email cũ đi trong list shared. Mình sẽ mô tả lại các bước code script này step by step nhé.

Đầu tiên ta hãy làm 1 cái giao diện người dùng cơ bản để dễ thao tác và sử dụng sau này. Google Apps Script hỗ trợ bạn tạo giao diện từ html, để làm được phần này bạn cần đọc tài liệu về nó ở đây [https://developers.google.com/apps-script/guides/html/](https://developers.google.com/apps-script/guides/html/). Với ứng dụng của mình mình đã sử dụng css AdminLTE quen thuộc để làm 1 cái form cho nó đẹp. Giao diện mình đã tạo như sau:

![Google Apps Script](https://boxxv.github.io/img/posts/b0ade875-39c8-4819-829d-352c0a723b20.webp "Google Apps Script")

Từ giao diện ta có: mình chia ra 3 chức năng riêng biệt dành cho tool này

1. Là tự động chuyển đổi quyền share file từ email cũ sang email gsuite mới
2. Thêm mới danh sách email vào list share
3. Gỡ bỏ email cũ đã share từ trước đó

Dưới đây là cấu trúc thư mục code và flow cơ bản để hiển thị view:

![Google Apps Script](https://boxxv.github.io/img/posts/c60b569d-deb8-42c7-852d-8893cd8f77cd.webp "Google Apps Script")

Cấu trúc thư mục gồm 1 file code.gs chứa mã xử lý chính của ứng dụng (ta có thể coi là xử lý phía server) và các File html chứa view, css và script ở phía client. Để hiện thị được từ file html lúc thực thi ứng dụng dưới dạng web ta cần viết hàm là doGet trong đó định sẵn việc sẽ render ra file Index.html:

```javascript
function doGet(request) {
  var html = HtmlService.createTemplateFromFile('Index')
  html.yourEmail = Session.getActiveUser().getEmail();
  
  return html.evaluate().setTitle('Tool change User\'s email shared with Google drive account');
}
```

Nói về phần code ở tab 2 dễ hơn trước nhé: ta cần bắt sự kiện khi click vào submit ở form html thì sẽ gom toàn bộ các thông tin và gửi lên server chính là file code.gs xử lý. Ở client muốn gọi 1 hàm trên server thì ta dùng câu lệnh `google.script.run.withSuccessHandler(updateLog).withFailureHandler(onFailure).executeAddEmails(emails, folderId);` trong đó `executeAddEmails` là tên hàm mà bạn viết code xử lý trong file code.gs. Phần liên lạc giữa client và server bạn có thể tham khảo ở đây [https://developers.google.com/apps-script/guides/html/communication](https://developers.google.com/apps-script/guides/html/communication) Và việc còn lại là xử lý các thông tin gửi lên từ client: nó sẽ có dạng 1 email + quyền (edit hoặc view) => ta cần quét trong thư mục đc chỉ định và thêm email với quyền tương ứng vào mục share. Trong đó thư mục được chỉ định đc lấy từ link mà ta cần xử lý paste vào ô text `Please enter folder url to scan` (xem lại hình giao diện ở trên). Phần xử lý đó như sau:

```javascript
// in code.gs
function executeAddEmails(emails, folderId) {
  var folder = DriveApp.getFolderById(folderId);
  for (var i = 0; i < emails.length; i++) {
    if (emails[i].permission == DriveApp.Permission.EDIT) {
      folder.addEditor(emails[i].email); 
    } else if (emails[i].permission == DriveApp.Permission.VIEW) {
      folder.addViewer(emails[i].email); 
    }
    Logger.log('Added: ' + emails[i].email + ' - ' + emails[i].permission);
  }
  
  return Logger.getLog();
}
```

Nhìn khá đơn giản phải không nào. Chạy thử nhé: Đầu tiên mình vào Google Drive tạo 1 thư mục là `QuanVH Test Script` và không share gì cả.

![Google Apps Script](https://boxxv.github.io/img/posts/042643c0-9435-4758-a970-c05a94a4f3ca.webp "Google Apps Script")

Tiếp theo mở ứng dụng ra nhập link folder trên vào và nhập thử 2 email để test trong đó 1 email có quyền edit và 1 email có quyền view.

![Google Apps Script](https://boxxv.github.io/img/posts/d718ab7e-63fd-4bfd-b09e-83a4d2997651.webp "Google Apps Script")


Click execute và chờ đợi thành quả. Sau mấy giây chạy xong ta có logs như sau:

![Google Apps Script](https://boxxv.github.io/img/posts/69f6b377-c920-4737-86ad-8b63af6f3975.webp "Google Apps Script")

Như vậy là đã thêm thành công quyền share cho 2 mail trên rồi, giờ thử mở Google drive kiểm tra thành quả nhé:

![Google Apps Script](https://boxxv.github.io/img/posts/1f7bfb82-b52e-472e-b2c4-dacfbaccb912.webp "Google Apps Script")

Wow, có vẻ mọi thứ ngon lành và kết quả đúng như ta mong đợi 😄


### Tổng kết

Còn 2 phần code về tự động đổi email và gỡ bỏ email đã share mình để lại cho các bạn tự khám phá nhé. Code mình để quyền view mọi người có thể vào đây để xem: https://script.google.com/d/1WvMPdGLa9ZMetKxRd6C4Tl5r4z-FvlyFvLzwLpL3ZJxoN4yzq1OhPIyp/edit?usp=sharing

Còn bạn nào muốn dùng thử luôn thì có thể truy cập vào web app mình đã publish: https://script.google.com/macros/s/AKfycbx1LUkXwjHeb1jvfM91AdQWZ8_mAQ9bfxptgZCUQb0n9iuxElQ/exec. (Lúc chạy có thể hiển thị ứng dụng này chưa xác minh là bởi vì mình chỉ viết cái này để dùng cá nhân chứ chưa submit cho Google xác minh và bạn hãy yên tâm sử dụng vì mình chỉ code đúng với chức năng của nó thôi chứ không làm gì GDrive của bạn đâu =))) )

Ngoài ra Google Apps Script còn đầy thứ hay ho khác trong mỗi dịch vụ mà nó có thể thao tác. Nó tùy thuộc vào bài toán của chính bạn. Trong phạm vi bài viết này mình chỉ đề cập và ứng dụng nó với GDrive để giúp các bạn hiểu cách hoạt động và bước đầu làm quen với nó.


-----
Tham khảo:
- [Google Apps Script có gì hay ho?!](https://viblo.asia/p/google-apps-script-co-gi-hay-ho-07LKX2xElV4)
- [Apps Script](https://workspace.google.com/intl/vi/products/apps-script/)
- [[48 videos] Tự học lập trình Google Apps Script trong Google Sheets](https://youtube.com/playlist?list=PLALCv46JuKEL2CmEzyr9_5bzYYGX2p8a6)
- [Cách tự động hóa Google Sheets với macro](https://quantrimang.com/cach-tu-dong-hoa-google-sheets-voi-macro-163586)
- [Hướng dẫn chi tiết cách ghi Macro trong Google Sheets](https://gitiho.com/blog/huong-dan-chi-tiet-cach-ghi-macro-trong-google-sheets.html)