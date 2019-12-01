---
layout: post
title: Các bước để tạo plugin cho video.js
---

Trong chủ đề này, chúng ta sẽ tìm hiểu cách sử dụng generator-videojs-plugin để tạo và kiểm tra plugin cho video.js.

Trình tạo plugin video.js tạo các tệp và thư mục cần thiết để tạo một plugin thông thường. Nó bao gồm một môi trường thử nghiệm để bạn có thể dễ dàng thấy những thay đổi của mình khi bạn phát triển plugin. Nó thậm chí còn tạo các tệp plugin cuối cùng mà bạn có thể sử dụng khi bạn sẵn sàng phát hành nó.

### Tổng quan

Trong chủ đề này, bạn sẽ thực hiện các tác vụ sau:
- Setup your environment
- Create the plugin foundation
- View the source files
- Test your plugin
- Edit the JavaScript file
- Edit the CSS file
- Build your plugin
- Pass data to your plugin
- Recommendations
- Resources

### I. Thiết lập môi trường

Để thiết lập môi trường của bạn để chạy trình tạo plugin, hãy làm theo các bước sau:

#### 1) Install Node.js - https://nodejs.org
Nếu bạn chưa có nó, hãy tải xuống và cài đặt Node.js JavaScript runtime. Điều này bao gồm npm, là một hệ sinh thái trọn gói bao gồm một bộ sưu tập lớn các thư viện nguồn mở.

Để kiểm tra xem việc cài đạt đã thành công hay chưa, hãy sử dụng các lệnh sau:
{% highlight js %}
> node -v
v10.16.0

> npm -v
6.9.0
{% endhighlight %}

#### 2) Tạo một thư mục cục bộ trên máy tính của bạn.
Trong ví dụ này, chúng tôi sẽ tạo một thư mục có tên là **test**. Đây là nơi tạo ra các tệp và plugin của bạn sẽ sinh ra.

#### 3) Read README
Xem lại thông tin **README** cho [video.js plugin generator.](https://github.com/videojs/generator-videojs-plugin). Trong thư mục **docs**, mở và xem lại các quy ước Plugin video.js. Tài liệu này nói về các quy tắc được đề xuất để tạo plugin của bạn.

#### 4) Open Terminal
Mở ứng dụng Terminal trong thư mục bạn đã tạo ở bước trước. Trong ví dụ này, hãy mở ứng dụng Terminal trong thư mục **test**.

#### 5) Cài đặt plugin generator cùng với Yeoman:
{% highlight js %}
> npm install -g yo generator-videojs-plugin
{% endhighlight %}

Trình tạo plugin video.js sử dụng trình tạo Yeoman, đây là công cụ tạo scaffolding để thiết lập nền tảng cho bất kỳ dự án nào. Điều này thiết lập các tập tin và thư mục cơ bản. Bạn không cần phải hiểu Yeoman. Bạn chỉ cần cài đặt nó với trình tạo plugin.


### II. Tạo nền tảng plugin
Trong phần này, bạn sẽ tạo các thư mục và tệp nền tảng cho plugin của mình.

#### 6) Trong Terminal, chạy lệnh sau:
{% highlight js %}
> yo videojs-plugin
{% endhighlight %}

Bạn có thể chạy lệnh này nhiều lần như bạn muốn. Điều này rất hữu ích nếu bạn quyết định thêm một tùy chọn vào plugin của mình sau khi làm việc với nó. Công cụ sẽ ghi nhớ các lựa chọn trước đó của bạn, nhưng bạn có thể phải ghi đè lên một số tệp.

#### 7) Cài đặt option cho plugin
Tiếp theo, bạn sẽ được hỏi một loạt các câu hỏi về chi tiết về plugin của bạn. Dưới đây là danh sách các tùy chọn cũng như mô tả ngắn gọn cho mỗi tùy chọn.

| Option | Description | Values for this example |
| -- | -- | -- |
| Package scope | **Optional**: Điều này chỉ cần thiết nếu bạn có kế hoạch xuất bản plugin của mình lên một tổ chức npm riêng. Bạn có thể sử dụng tên công ty của bạn ở đây hoặc để trống. | blank |
| Plugin name | Đặt tên cho plugin của bạn. Nhập tên **demo** sẽ tạo một plugin có tên **videojs-demo**. | demo |
| Description | Nhập mô tả cho plugin của bạn. | This is a demo |
| Author | Định dạng tên và địa chỉ email là không bắt buộc, nhưng được sử dụng để điền vào trường tác giả trong tệp pack.json. Trình tạo sẽ cố gắng đoán các giá trị này dựa trên thiết lập git của bạn, nhưng bạn có thể thay đổi chúng. | [your name] <your email address> |
| License | Chọn một trong các tùy chọn giấy phép. Đối với các plugin riêng tư của bạn, bạn có thể chọn Unlicensed. | Unlicensed |
| Basic or Advanced Plugin | Plugin dựa trên chức năng cơ bản là một hàm JavaScript đơn giản. Nếu trước đây bạn đã viết một plugin Video.js, thì bạn nên làm quen với khái niệm plugin cơ bản. Plugin dựa trên lớp nâng cao đã được giới thiệu với Video.js 6. Loại plugin này bắt đầu bằng một lớp JavaScript, là một hàm tạo. Để biết chi tiết, hãy xem tài liệu readme Plugins của [Video.js Plugins](https://github.com/videojs/Video.js/blob/master/docs/guides/plugins.md). | Basic plugin (function-based) |
| CSS tooling | Chọn có, nếu bạn muốn bao gồm kiểu CSS. Điều này sẽ tạo ra một tệp CSS. | Yes |
| Documentation tooling | Nếu có, trình tạo bao gồm JSDoc và cung cấp lệnh để tạo tài liệu. | Yes |
| Internationalized strings | Điều này rất hữu ích nếu bạn có văn bản mà bạn muốn dịch sang các ngôn ngữ khác nhau. Công cụ này không cung cấp dịch tự động, nhưng nó chuyển đổi các tệp từ định dạng JSON của video.js sang JavaScript. Sau đó, bạn có thể tạo ngôn ngữ như bạn muốn cho video.js và biên dịch chúng thành đầu ra của plugin. | Yes |
| Lint changed files | Bao gồm một công cụ Linting được gọi là tiêu chuẩn videojs. Quá trình này kiểm tra mã của bạn cho một số lỗi phổ biến. | Yes |
| Before Git push | Điều này cung cấp cho bạn tùy chọn để ngăn việc đẩy vào kho git nếu kiểm tra được chọn không thành công. Kiểm tra chất lượng mã là một cách tốt để ngăn chặn việc đẩy mã không đạt tiêu chuẩn. | Yes |

Đây là kết quả đầu ra trông như thế nào với các giá trị được đặt cho ví dụ này:

<img align="center" alt="placeholder" src="/img/option-values.png" title="Plugin option values">_Option values_

#### 8) Khi thiết lập hoàn tất
Bạn sẽ thấy một vài thông báo. Có thể có một số thông điệp cảnh báo, nhưng không có lỗi.

<img align="center" alt="placeholder" src="/img/setup-complete.png" title="Plugin setup complete">_Setup complete_

Lưu ý rằng tên của plugin là videojs-demo.


### III. Xem các tập tin source
Trong phần này, chúng tôi sẽ xem xét các tệp nguồn được tạo bởi videojs generator.

#### 9) src folder
Trong trình chỉnh sửa, hãy mở thư mục trên cùng nơi bạn đặt dự án plugin của mình. Mở thư mục src. Ở đây bạn sẽ tìm thấy như sau:
- Một tập tin plugin.js. Tập tin này chứa mã cho plugin của bạn.
- Một tập tin plugin.css, nếu bạn chọn Có với tùy chọn công cụ CSS.

#### 10) plugin.css
(Nếu bạn không chọn Có với tùy chọn công cụ CSS, bạn có thể bỏ qua bước này.) Mở tệp src> plugin.css.

Mã của bạn sẽ trông giống như sau:
{% highlight css %}
/* Note: all vars must be defined here, there are no "local" vars */
:root {
  --main-color: red;
  --base-font-size: 9;
  --font-size: 7;
}

.video-js {

  &.vjs-basic {
    /* This class is added to the video.js element by the plugin by default. */
    display: block;

    & .remove-me, & .remove-me-too, &.finally-remove-me {
      /* examples of postcss syntax, you probably want to remove this */

      color: var(--main-color);

      /**
       * Note that you have to use calc and multiply by a value with a unit
       * prepending the unit like `var(--base-font-size)px` or
       * `calc(10 * var(--base-font-size)em` will NOT work!
       */
      font-size: calc(var(--font-size) * 8 * var(--base-font-size) * 1px);

    }
  }
}
{% endhighlight %}




