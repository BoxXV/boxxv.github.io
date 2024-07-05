---
layout: post
title: Bộ cài đặt tốt nhất cho máy Windows
subtitle: Chrome Extension Getting Started
image: "img/2024/1277070923.png"
tags:
- Mạt Code
- lập trình
---

## Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
- [Cách hoạt động](#cách-hoạt-động)
- [Cấu trúc của một extension](#cấu-trúc-của-một-extension)
- [Publish một extension lên chrome store](#publish-một-extension-lên-chrome-store)
- [Kết luận](#kết-luận)


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

## Giới thiệu



## Cách hoạt động



## Cấu trúc của một extension



## Publish một extension lên chrome store



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