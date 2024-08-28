---
layout: post
title: Xây dựng ứng dụng Chrome Extension
subtitle: Chrome Extension Getting Started
image: "img/2024/1277070923.png"
tags:
- Chrome
- Extension
- lập trình
---

## Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
- [Tâm sự cùng AI](#tâm-sự-cùng-ai)
- [Cách hoạt động](#cách-hoạt-động)
  - [Manifest file](#manifest-file)
  - [Content script](#content-script)
  - [Popup page](#popup-page)
  - [Background page](#background-page)
  - [Options](#options)
- [Giao tiếp gữa các thành phần](#giao-tiếp-gữa-các-thành-phần)
- [Publish một extension lên chrome store](#publish-một-extension-lên-chrome-store)
- [Kết luận](#kết-luận)

## Giới thiệu

Xin chào tất cả các bạn. Chắc hẳn các bạn không còn xa lạ gì với trình duyệt web Chrome nữa. Một điều mình rất thích chrome là hỗ trợ rất nhiều extension (Tiện ích mở rộng) như Google translate, Docs, Sheet, AdBlock, ... .Các tiện ích này rất hữu ích cho chúng ta đúng? Nhưng bạn có biết cách để tạo ra extension như thế nào? Trong bài viết này mình sẽ hướng dẫn các bạn làm một extension đơn giản và tương tác giữa extension với website.

## Tâm sự cùng AI

`Người dùng bình thường`: hello world chrome extension

`Claude-3-Sonnet`: Để tạo một tiện ích mở rộng (extension) "Hello World" cho trình duyệt Chrome, bạn cần thực hiện các bước sau:

Tạo thư mục cho tiện ích mở rộng, ví dụ "hello_world_extension".
Trong thư mục đó, tạo một tệp tin `manifest.json` để mô tả tiện ích mở rộng. Nội dung tệp tin có thể là:

```json
{
  "manifest_version": 2,
  "name": "Hello World",
  "version": "1.0",
  "description": "Tiện ích mở rộng Hello World đơn giản",
  "browser_action": {
    "default_popup": "popup.html"
  }
}
```

Tạo một tệp tin `popup.html` với nội dung sau:

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Hello World!</h1>
    <script src="popup.js"></script>
  </body>
</html>
```

Tạo một tệp tin `popup.js` với nội dung:

```javascript
alert('Hello World!');
```

Mở trình duyệt Chrome và truy cập vào `chrome://extensions/`.
Bật "Chế độ dành cho nhà phát triển" ở góc trên bên phải.
Nhấn vào "Tải tiện ích mở rộng chưa đóng gói" và chọn thư mục "hello_world_extension".
Tiện ích mở rộng "Hello World" đã được cài đặt. Khi bạn nhấn vào biểu tượng tiện ích, cửa sổ bật lên sẽ hiển thị "Hello World!".

Đây chỉ là một ví dụ đơn giản. Bạn có thể mở rộng tiện ích bằng cách thêm nhiều tính năng khác nhau vào tệp tin popup.js và popup.html.

## Cách hoạt động

Đầu tiên nãy nói về các khái niệm và mô hình hoạt động của chrome extension nhé. 

![Extension](https://boxxv.github.io/img/2024/06b94e36-9691-45c7-b93c-69e92fe38f23.png "Extension")

Về cơ bản, một Chrome Extension chủ yếu sẽ được viết bằng Javascript và HTML. Bạn có thể tổ chức các thư mục tùy ý sao cho phù hợp và tiện lợi nhất trong quá trình code.

Cấu trúc của một extension, Chức năng của các thành phần

### Manifest file

manifest.json là 1 file rất quan trọng nó dùng để khai báo các quyền mà extension cần ví dụ như tabs, storage, ... Khai báo các đường dẫn đến resource (icons, script, UI,...) của extenions.

```json
{
  "name": "demo-extension",
  "description": "A chrome extension",
  "version": "1.0.0",
  "manifest_version": 2,
  "permissions": [ "tabs", "https://www.yoursite.com/*"],
  "icons": { "16": "icons/icon_16.png", "48": "icons/icon_48.png", "128": "icons/icon_128.png" },
  "browser_action": { "default_title": "your title", "default_popup": "popup.html" },
  "background": {
    "scripts": ["background.js"]
  },
  "content_scripts": [{
    "matches": ["https://www.yoursite.com/*"],
    "js": ["content.js"]
  }],
  "options_ui": { "page": "options.html", "chrome_style": true },
  "externally_connectable": {
    "matches": ["https://www.yoursite.com/*"]
  }
}
```

Đối với người mới chỉ cần quan tâm đến các thuộc tính quan trọng sau:

- `name`: Là thuộc tính xác định tên extension của bạn
- `version`: Phiên bản hiện tại, Chrome sẽ dựa vào đây để xác định xem extension của bạn có bản cập nhật mới hay không
- `manifest_version`: Xác định phiên bản của chính file manifest.json
- `description`: Miêu tả chi tiết hơn về extension
- `icons`: Icon của extension sẽ được hiển thị trên store. Trong trường hợp này, mình để chúng trong thư mục images
- `browser_action`:
    + `default_icon`: Icon sẽ được sử dụng để hiển thị trên trình duyệt
    + `default_title`: Title sẽ được hiển thị khi hover chuột vào icon của extension
    + `default_popup`: Đây là file HTML sẽ được hiển thị khi bạn mở extension ra. Chúng ta sẽ nói rõ hơn về file này trong phần sau
- `background`: Dẫn đến background script. Còn background script mình sẽ nói rõ hơn ở phần dưới
    + `page`: Đây sẽ là trang chạy ngầm bên dưới và thường sẽ chỉ chứa một script tag để đưa file javascript vào
    + `persistent`: Là flag có giá trị là true hoặc false. Xác định trang background sẽ được chạy như thế nào
- `content_scripts`: Phần này dùng để inject các script, style vào page được khai báo.
    + `matches`: Xác định các trang web mà bạn muốn thêm các nội dung của mình vào
    + `js`: Là danh sách các file javascript sẽ được inject vào các trang web đã được khai báo bên trên
    + `css`: Tương tự như thuộc tính js nhưng là danh sách các file css
    + `run_at`: Thời điểm inject các file content bên trên vào trang web
- `permissions`: Khai báo các quyền hạn truy cập cho extension

Bạn có thể xem chi tiết phần config file manifest.json [ở đây](https://developer.chrome.com/docs/extensions/reference/manifest)

### Content script

Đây là các thành phần được inject vào các trang web mà bạn khai báo ở thuộc tính `matches` trong file `manifest.json`. Các thành phần này được chạy cùng môi trường với trang web hiện tại nên bạn có thể sử dụng javascript, css để thao tác lên các thành phần DOM. Nhờ đó bạn có thể thay đổi giao diện trang, thêm các button, thêm các chức năng khác mà bạn muốn.

### Popup page

Đây là trang sẽ chạy và hiển thị khi bạn mở extension của mình lên. Cấu trúc của nó cũng tương tự như những trang HTML khác. Trong trường hợp của mình thì đó trang `popup.html`. Trang này được chạy ở một môi trường khác so với các content script. Có thể hiểu nôm na là chúng được chạy ở một cửa sổ trình duyệt khác so với cửa sổ trình duyệt hiện tại.

```html
<!doctype html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <link rel="stylesheet" href="./styles/lib/bootstrap.min.css">
        <link rel="stylesheet" href="./styles/page.css">
        <title>My Extension</title>
    </head>
    <body>
        <div class="wrapper">
            <h1>This is popup page</h1>
        </div>
        <script src="./scripts/lib/bootstrap.min.js"></script>
        <script type="module" src="./scripts/popup.js"></script>
    </body>
</html>
```

Bạn sẽ tạo giao diện chính cho extension của mình tại đây. Trang sẽ được load lại mỗi khi extension được mở. Bạn có thể sử dụng `localStorage` để lưu trữ dữ liệu giống như một database.

### Background page

Cũng giống như trang `popup.html`, trang `background.html` cũng sẽ chạy cùng một môi trường. Tuy nhiên nó không có giao diện mà đơn thuần chỉ chứa một script tag với mục đích đưa vào đó file `background.js`.

```html
<html>
    <body>
        <script type="module" src="./scripts/background.js"></script>
    </body>
</html>
```

Mặc định trang này sẽ được tự động sinh ra và tự động inject file `background.js`, nhưng trong trường hợp bạn muốn custom nó thì đây sẽ là nơi để bạn thực hiện điều đó

File `background.js` được sử dụng với mục đích tương tự như một server, nó lắng nghe các sự kiện được gọi từ trang popup hay trang content. Xử lý, lưu trữ dữ liệu cũng như là trả về data trong response.

### Options

Đây thường là phần dùng để hiển thị các setting cho extentions đó. Chẳng hạn setting chọn ngôn ngữ, thông báo, ... Phần này có thể có hoặc không tùy vào mục đích của bạn.

![Extension](https://images.viblo.asia/fc18beca-b580-4bc4-a832-16f4e81961db.png "Extension")

## Giao tiếp gữa các thành phần

Vừa rồi chúng ta đã phần nào hiểu được chức năng của các thành phần trong một extension. Như chúng ta đã biết, file content.js được chạy cùng với trang web hiện tại mà nó được inject vào. Trong khi đó, popup.js và background.js được chạy ở cùng một môi trường và chúng tách biệt hoàn toàn so với của sổ hiện tại mà trình duyệt đang hiển thị. Vì thế, để có sự kết nối giữa các file script ở các môi trường khác nhau, Chrome sử dụng các message để thể hiện sự giao tiếp đó.

Chúng ta sẽ cùng nhau làm môt ví dụ để hiểu hơn vấn đề này nhé. Extension của chúng ta sẽ có chức năng là lưu lại các bài hát mà mình thích trên https://www.nhaccuatui.com/ để hàng ngày có thể nghe lại chúng mà không phải mất công tìm kiếm. Tất nhiên là thực tế thì trang nhạc nào cũng có chức năng tạo playlist rồi. Nào hãy cùng bắt đầu thôi.

## Publish một extension lên chrome store

Chuẩn bị: 1 tài khoản gmail, 5$ để mua tài khoản develop, 1 extension đã dc zip( chú ý ko được mã hóa code và minimize code không sẽ ko vượt qua dc tester của goole)

Thực hiện: Vào trang dashboard của extension: https://chrome.google.com/webstore/developer/dashboard?authuser=1. Sau đó add new item.

- Phần upload ta upload file zip lên
- Phần detail : bạn điền description cho extension của bạn
- Phần screenshots: bạn có thể chụp ảnh hướng dẫn, video youtube và add vào đây. Sau khi lên google store nó sẽ hiện ra những ảnh or video đó
- Phần icon bạn upload icon 128x128.
- Phần category bạn chọn một loại category cho extension của mình ví dụ: Func, Social & Communication... Phần Visibility options bạn chọn private or pubic extension của bạn. Khi 1 extension được publish sẽ phải qua tester của google review. Bạn để public thì mọi người mới có thể cài thấy và cài extension

## Kết luận

Để tạo môt extension và publish lên rất là đơn giản nhưng để làm được một extension hữu ích cho người sử dụng thì còn cần rất nhiều kiến thức mà trong thời gian cho phép mình chưa thể tìm hiểu hết được. Hy vọng trong các bài report tháng tới sẽ nghiên cứu và viết được mốt số extension hay ho (yaoming)

-----
- [Tiện ích Hello World (Xin chào thế giới)](https://developer.chrome.com/docs/extensions/get-started/tutorial/hello-world?hl=vi)
- []()
- [Cách viết một chrome extentions](https://viblo.asia/p/cach-viet-mot-chrome-extentions-ByEZkOBqZQ0)
- [Tự tạo Chrome Extension cho riêng mình](https://viblo.asia/p/tu-tao-chrome-extension-cho-rieng-minh-1VgZv4rM5Aw)
- [Hướng dẫn viết một Extension trên Chrome](https://viblo.asia/p/huong-dan-viet-mot-extension-tren-chrome-924lJqaWZPM)
- [Cách viết một extension chrome cơ bản](https://viblo.asia/p/cach-viet-mot-extension-chrome-co-ban-m68Z0wzMKkG)
- [Xây dựng ứng dụng Chrome Extension đơn giản trong 10 phút](https://viblo.asia/p/xay-dung-ung-dung-chrome-extension-don-gian-trong-10-phut-RnB5pkrrlPG)
- [Web developer extension for Chrome](https://viblo.asia/p/web-developer-extension-for-chrome-QpmlenMM5rd)
- [Làm quen với chrome extension](https://viblo.asia/p/lam-quen-voi-chrome-extension-aWeKmgDvGBD)
- [Make a simple Chrome Extension - Cute Cat](https://viblo.asia/p/make-a-simple-chrome-extension-cute-cat-maGK7k7BKj2)
- [Viết Chrome Extension bằng VueJS](https://viblo.asia/p/viet-chrome-extension-bang-vuejs-Ljy5VoVjKra)
- [Xây dựng một Chrome Extension bằng ReactJs (Phần 1 - Tổng quan)](https://viblo.asia/p/xay-dung-mot-chrome-extension-bang-reactjs-phan-1-tong-quan-924lJAxNZPM)
- [Tạo ứng dụng Todo trên Chrome Extension với React](https://viblo.asia/p/tao-ung-dung-todo-tren-chrome-extension-voi-react-bWrZnObblxw)
- [Tạo một Google Chrome Extension với React](https://viblo.asia/p/tao-mot-google-chrome-extension-voi-react-Az45byVNlxY)
- [[Chrome Extension] Hướng dẫn tạo ứng dụng đầu tay](https://viblo.asia/p/chrome-extension-huong-dan-tao-ung-dung-dau-tay-QpmlegykKrd)
- [Tự xây dựng một Chrome Extension đo performance của website đơn giản trong 5 phút](https://viblo.asia/p/tu-xay-dung-mot-chrome-extension-do-performance-cua-website-don-gian-trong-5-phut-ByEZkLNglQ0)
- [Tạo ứng dụng Chrome extension](https://viblo.asia/p/tao-ung-dung-chrome-extension-al5XRBZkRqPe)
- [Newbie tập viết extension trên chrome](https://viblo.asia/p/newbie-tap-viet-extension-tren-chrome-07LKXw4k5V4)
- [Cần học gì để tự làm một Chrome Extension?](https://viblo.asia/p/can-hoc-gi-de-tu-lam-mot-chrome-extension-3P0lPE245ox)
- []()
- [Chrome Extension: Xây dựng một Trading BOT cơ bản](https://viblo.asia/p/chrome-extension-xay-dung-mot-trading-bot-co-ban-GrLZDOeEKk0)
- [Giới thiệu extension Chat++++](https://viblo.asia/p/gioi-thieu-extension-chat-Qpmle9Brlrd)
- [Chrome exension và viết extension skip quảng cáo trên Youtube](https://viblo.asia/p/chrome-exension-va-viet-extension-skip-quang-cao-tren-youtube-vyDZO7GQZwj)
- [Tạo 1 Notification Extension đơn giản trên Chrome](https://viblo.asia/p/tao-1-notification-extension-don-gian-tren-chrome-djeZ1yd3ZWz)
- [Tạo extension "NOTE" của riêng bạn](https://viblo.asia/p/tao-extension-note-cua-rieng-ban-bJzKmoeXl9N)
- [Ghi chép về Browser Extension đầu tiên](https://viblo.asia/p/ghi-chep-ve-browser-extension-dau-tien-1VgZvrymZAw)
- [Developer mà vẫn chưa biết những Chrome Extensions này thì... giờ biết rồi nhé!!!](https://viblo.asia/p/developer-ma-van-chua-biet-nhung-chrome-extensions-nay-thi-gio-biet-roi-nhe-6J3Zg3zAZmB)
- [Tôi đã viết Chrome extension đầu tiên của mình bằng Github Copilot như thế nào?](https://viblo.asia/p/toi-da-viet-chrome-extension-dau-tien-cua-minh-bang-github-copilot-nhu-the-nao-GyZJZd18Vjm)
- [[Small Project] - Chrome Extension - Chia sẻ cuộc hội thoại ChatGPT](https://viblo.asia/p/small-project-chrome-extension-chia-se-cuoc-hoi-thoai-chatgpt-AZoJjYX24Y7)
- []()
- [[Selenium Webdriver] How to add chrome extension and access link in selenium.](https://viblo.asia/p/selenium-webdriver-how-to-add-chrome-extension-and-access-link-in-selenium-Do754JJVZM6)
- [How to create a chrome extension](https://viblo.asia/p/how-to-create-a-chrome-extension-QWkwGnYqM75g)
- [How to create a Google Chrome Extension : case study "Chatwork Emoticons Plus"](https://viblo.asia/p/how-to-create-a-google-chrome-extension-case-study-chatwork-emoticons-plus-AeJ1vOYQMkby)
- [Chrome Extension: Getting Started](https://viblo.asia/p/chrome-extension-getting-started-djeZ1p8GKWz)
- [hello-world-chrome-extension](https://github.com/gitfaf/hello-world-chrome-extension)