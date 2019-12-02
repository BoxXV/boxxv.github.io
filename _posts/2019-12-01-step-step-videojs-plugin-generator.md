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


-----
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

<img align="center" alt="placeholder" src="/img/plugin-generator/option-values.png" title="Plugin option values">_Option values_

#### 8) Khi thiết lập hoàn tất
Bạn sẽ thấy một vài thông báo. Có thể có một số thông điệp cảnh báo, nhưng không có lỗi.

<img align="center" alt="placeholder" src="/img/plugin-generator/setup-complete.png" title="Plugin setup complete">_Setup complete_

Lưu ý rằng tên của plugin là videojs-demo.


-----
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

#### 11) plugin.js
Trình tạo sử dụng ES6, đây là phiên bản JavaScript mới nhất. Tìm hiểu thêm về các tính năng mới trong [ECMAScript 6](http://es6-features.org). Trình tạo dịch mã ES6 của bạn thành mã ES5 để mã phân phối của bạn sẽ chạy trên phần lớn các trình duyệt.

Mã của bạn sẽ trông giống như sau:
- Dòng 25-27: gọi hàm `onPlayerReady()`, khi player sẵn sàng. Tại đây, bạn có thể chuyển các biến vào plugin bằng cách sử dụng đối tượng tùy chọn.
- Dòng 26: thêm lớp `vjs-demo` cho player của bạn. Theo mặc định, đây là điều duy nhất mã bộ xương làm. Đây là nơi bạn có thể thêm chức năng vào plugin của mình.
- Dòng 48: đăng ký plugin của bạn với `video.js`.
- Dòng 51: thêm một tham số phiên bản vào plugin của bạn. Khi bạn chạy tập lệnh phiên bản npm, nó sẽ cập nhật biến này thành phiên bản bạn đang bật.

{% highlight js %}
import videojs from 'video.js';
import {version as VERSION} from '../package.json';

// Default options for the plugin.
const defaults = {};

// Cross-compatibility for Video.js 5 and 6.
const registerPlugin = videojs.registerPlugin || videojs.plugin;
// const dom = videojs.dom || videojs;

/**
 * Function to invoke when the player is ready.
 *
 * This is a great place for your plugin to initialize itself. When this
 * function is called, the player will have its DOM and child components
 * in place.
 *
 * @function onPlayerReady
 * @param    {Player} player
 *           A Video.js player object.
 *
 * @param    {Object} [options={}]
 *           A plain object containing options for the plugin.
 */
const onPlayerReady = (player, options) => {
  player.addClass('vjs-demo');
};

/**
 * A video.js plugin.
 *
 * In the plugin function, the value of `this` is a video.js `Player`
 * instance. You cannot rely on the player being in a "ready" state here,
 * depending on how the plugin is invoked. This may or may not be important
 * to you; if not, remove the wait for "ready"!
 *
 * @function demo
 * @param    {Object} [options={}]
 *           An object of options left to the plugin author to define.
 */
const demo = function(options) {
  this.ready(() => {
    onPlayerReady(this, videojs.mergeOptions(defaults, options));
  });
};

// Register the plugin with video.js.
registerPlugin('demo', demo);

// Include the version number.
demo.VERSION = VERSION;

export default demo;
{% endhighlight %}


-----
### IV. Test plugin của bạn
Trình tạo plugin giúp dễ dàng phát triển và kiểm tra plugin của bạn bằng môi trường kiểm tra cục bộ. Thực hiện theo các bước sau để kiểm tra plugin của bạn:

#### 12) Trong Terminal, nhập lệnh sau để khởi động máy chủ phát triển:
{% highlight js %}
> npm start
{% endhighlight %}

#### 13) Trong trình duyệt, nhập thông tin sau để mở máy chủ phát triển:
{% highlight js %}
http://localhost:9999/
{% endhighlight %}

Bạn sẽ thấy player với một video thử nghiệm. Trình tạo cho bạn một player demo chạy trong trang. Trong các công cụ dành cho nhà phát triển trình duyệt, hãy mở tab Elements để xem HTML cho player.

<img align="center" alt="placeholder" src="/img/plugin-generator/browser-test.png" title="Browser testing">_Browser testing_

#### 14) Kiểm tra các yếu tố của trang web này. Bạn sẽ thấy rằng lớp vjs-demo đã được thêm vào player. Hãy nhớ rằng chúng tôi đã thêm lớp này cho player trong mã plugin.

<img align="center" alt="placeholder" src="/img/plugin-generator/vjs-demo-class.png" title="vjs-demo class">_vjs-demo class_

#### 15) Bây giờ, hãy thử thêm mã vào plugin để tự động bắt đầu phát video khi player tải. Quay trở lại tệp **src> plugin.js** trong trình chỉnh sửa của bạn.

#### 16) In the `onPlayerReady()` method, add code to start playback of the video.
{% highlight js %}
const onPlayerReady = (player, options) => {
  player.addClass('vjs-demo');
  player.play();
};
{% endhighlight %}

#### 17) Lưu tệp plugin.js trong trình chỉnh sửa của bạn. Khi bạn làm mới trình duyệt của mình, bạn sẽ thấy rằng video bắt đầu phát trong môi trường thử nghiệm.

Khi bạn phát triển plugin của mình trong tệp plugin.js và lưu các thay đổi, công cụ sẽ tự động xây dựng lại và tải lại player trong trình duyệt. Điều này giúp dễ dàng phát triển và kiểm tra plugin của bạn.

#### 18) Xóa dòng mã để bắt đầu phát video.
{% highlight js %}
player.play();
{% endhighlight %}

> Trong Terminal, nhấn **CTRL-C** để dừng máy chủ phát triển.


-----
### V. Edit the JavaScript file

Trong phần này, bạn sẽ thêm mã vào tệp nguồn JavaScript để thêm một phần tử có văn bản tùy chỉnh vào player.

#### 19) Trong trình chỉnh sửa của bạn, quay lại tệp src> plugin.js.

#### 20) Trong hàm `onPlayerReady()`, thêm mã để thêm phần tử `<p>` với văn bản tùy chỉnh vào player.
{% highlight js %}
const onPlayerReady = (player, options) => {
  player.addClass('vjs-demo');
  var textDisplay = document.createElement('p');
  textDisplay.className = 'vjs-text';
  textDisplay.innerHTML = "Becoming a plugin developer";
  player.el().appendChild(textDisplay);
};
{% endhighlight %}

#### 21) Lưu các tập tin. Hãy nhớ rằng những thay đổi của bạn sẽ được cập nhật tự động trong trình duyệt thử nghiệm.

#### 22) Quay trở lại trình duyệt thử nghiệm. Bạn sẽ thấy không có gì thay đổi trong player. Vấn đề là văn bản ở đó, nhưng nó không nhìn thấy được. Chúng tôi sẽ sửa nó tiếp theo.

Để xác minh rằng phần tử văn bản đã được thêm vào player, hãy sử dụng các công cụ phát triển trong trình duyệt. Trong phần **Elements**, mở rộng phần tử `<div>` của người chơi. Bạn sẽ thấy thẻ đoạn vừa được thêm vào.

<img align="center" alt="placeholder" src="/img/plugin-generator/p-element.png" title="Added paragraph tag">_Added paragraph tag_

Chúng tôi sẽ làm cho văn bản hiển thị trong phần tiếp theo bằng cách sử dụng CSS.


-----
### VI. Edit the CSS file
Trong phần này, bạn sẽ thêm mã vào tệp nguồn CSS để hiển thị văn bản trên player.

#### 23) Trong trình chỉnh sửa của bạn, quay lại tệp src> plugin.css.

Add the .vjs-text selector with styles to display the custom text in the player.
#### 24) Thêm `.vjs-text` selector với các styles để hiển thị văn bản tùy chỉnh trong player.
{% highlight css %}
/* Note: all vars must be defined here, there are no "local" vars */
:root {
  --main-color: red;
  --base-font-size: 9;
  --font-size: 7;
}

.vjs-text {
  background-color: #333333;
  color: white;
  position: absolute;
  font-size: 2em;
  text-align: center;
  width: 100%;
  margin-top: 10%;
}
{% endhighlight %}

#### 25) Lưu các tập tin. Hãy nhớ rằng những thay đổi của bạn sẽ được cập nhật tự động trong trình duyệt thử nghiệm.

#### 26) Quay trở lại trình duyệt thử nghiệm. Bây giờ bạn sẽ thấy văn bản tùy chỉnh được hiển thị trên trình phát.
<img align="center" alt="placeholder" src="/img/plugin-generator/text-display.png" title="Text displayed over the player">_Text displayed over the player_

#### 27) Dừng máy chủ phát triển bằng cách nhấn **CTRL-C** trong ứng dụng Terminal.

Bây giờ, bạn đã sẵn sàng để chuẩn bị plugin để phân phối. Chúng tôi sẽ làm điều đó tiếp theo.


-----
### VII. Build your plugin
Trong phần này, bạn sẽ xây dựng plugin của mình. Điều này lấy mã nguồn của bạn và tạo các tệp CSS và JavaScript có thể phân phối.

#### 28) Trong Terminal, chạy lệnh sau:
{% highlight js %}
> npm run build
{% endhighlight %}

Bản dựng lấy mã nguồn ES6 của bạn và chuyển đổi thành mã JavaScript ES5.

#### 29) Trong thư mục dự án của bạn, mở rộng thư mục **dist**. Đây là nơi bạn sẽ tìm thấy một phiên bản phân phối của plugin của bạn. Tại đây, bạn sẽ tìm thấy các tệp sau (giả sử bạn đã chọn Có cho công cụ CSS):
- **videojs-demo.css**
- **videojs-demo.js**
- **videojs-demo.min.js**

Bạn cũng sẽ tìm thấy các tệp ít được sử dụng này:
- **videojs-demo.cjs.js** Đây là mô-đun CommonJS được sử dụng khi dự án của bạn được yêu cầu trong Node hoặc nếu bạn đang sử dụng Browserify để gói JavaScript.
- **videojs-demo.es.js** Đây là mô-đun ES6 cho các dự án hiện đại sử dụng WebPack hoặc Rollup để đóng gói các phụ thuộc của chúng.

#### 30) Trong thư mục **dist**, mở tệp videojs-demo.js.
<img align="center" alt="placeholder" src="/img/plugin-generator/dist-js.png" title="Distribution files">_Distribution files_

Một số điều cần lưu ý về tệp phân phối này:
- Một biểu ngữ giấy phép đã được thêm vào đầu tập tin.
- Plugin của bạn đã được bọc trong một không gian tên browserify. Điều này có nghĩa là không có biến toàn cục có thể xung đột với mã trang của bạn.
- Các plugin nội bộ đăng ký chính nó với videojs. Điều này có nghĩa là bạn có thể tạo nhiều plugin, mỗi plugin hoạt động độc lập cho một người chơi.


-----
### VIII. Pass data to your plugin
Phần này là tùy chọn. Bạn có thể bỏ qua phần này trừ khi bạn muốn tìm hiểu cách truyền dữ liệu đến plugin của mình.

#### 31) Chúng tôi sẽ sử dụng thuộc tính tùy chọn để chuyển dữ liệu từ trang HTML của chúng tôi vào plugin.
Để biết chi tiết về cách sử dụng thuộc tính này, hãy xem  tài liệu [Truyền dữ liệu vào Plugin](https://support.brightcove.com/pass-data-plugin).

#### 32) Trong trình chỉnh sửa của bạn, quay lại tệp src> plugin.js.

#### 33) Trong hàm `onPlayerReady()`, thêm mã để sử dụng giá trị văn bản trong thuộc tính tùy chọn nếu nó tồn tại, nếu không thì sử dụng giá trị văn bản mặc định.
- Dòng 4: tạo một phần tử đoạn
- Dòng 5: gán loại lớp văn bản
- Dòng 6: kiểm tra xem đối tượng displayText có tồn tại trong thuộc tính tùy chọn không
- Dòng 7: sử dụng giá trị displayText để điền vào màn hình văn bản
- Dòng 9: sử dụng giá trị hiển thị văn bản mặc định
- Dòng 13: thêm phần tử văn bản hiển thị vào DOM
{% highlight js %}
const onPlayerReady = (player, options) => {
  player.addClass('vjs-demo');

  var textDisplay = document.createElement('p');
  textDisplay.className = 'vjs-text';

  if ('displayText' in options) {
    textDisplay.innerHTML = options.displayText;
  } else {
    textDisplay.innerHTML = "Becoming a plugin developer";
  }

  player.el().appendChild(textDisplay);
};
{% endhighlight %}

#### 34) Lưu tệp và quay lại trình duyệt thử nghiệm.
Bạn không nên thấy bất kỳ thay đổi nào đối với màn hình văn bản.

#### 35) Nếu bạn chưa làm như vậy, hãy thêm css cho `.vjs-text` selector từ phần Chỉnh sửa tệp CSS.

#### 36) Xây dựng plugin của bạn. Chúng tôi sẽ sử dụng các tệp trong thư mục dist trong một trang web thử nghiệm.

#### 37) Trong máy chủ thử nghiệm cục bộ của bạn, như MAMP, hãy tạo một thư mục có tên là **plugin-generator**.

#### 38) Trong thư mục này, sao chép các tệp **videojs-demo.css** và **videojs-demo.js** từ thư mục **dist** và dán chúng vào thư mục máy chủ thử nghiệm, **plugin-generator**.

#### 39) Tiếp theo, trong thư mục này, tạo một tệp HTML với trình phát gọi plugin thử nghiệm của chúng tôi và chuyển vào một giá trị cho văn bản hiển thị. Chúng tôi sẽ đặt tên tệp này là tests.html.
- Dòng 8: bao gồm các kiểu plugin của chúng tôi.
- Dòng 13-22: thêm trình phát Brightcove vào trang web của chúng tôi.
- Dòng 24: bao gồm tệp JavaScript plugin của chúng tôi.
- Dòng 26-32: thực thi tập lệnh trang tùy chỉnh.
- Dòng 27: chờ player sẵn sàng.
- Dòng 28: được tham chiếu đến player.
- Dòng 29: định nghĩa đối tượng `options`.
- Dòng 30: gọi plugin `demo` của chúng tôi và chuyển vào đối tượng `options`. Lưu ý rằng tên plugin là `demo`, trong khi tên tệp plugin là `videojs-demo`.

{% highlight html %}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Passing data to the plugin</title>

  <link href="videojs-demo.css" rel="stylesheet">
</head>
<body>
  <video-js id="myPlayerID"
    data-video-id="5977793284001"
    data-account="1752604059001"
    data-player="default"
    data-embed="default"
    data-application-id
    class="video-js"
    width="640px" height="360px"
    controls></video-js>
  <script src="//players.brightcove.net/1752604059001/default_default/index.min.js"></script>
<script type="text/javascript" src="videojs-demo.js"></script>
<script type="text/javascript">
  videojs.getPlayer('myPlayerID').ready(function() {
    var myPlayer = this,
      options = {"displayText": "This data supplied at initialization"};
      myPlayer.demo(options);
  });
</script>
</body>
</html>
{% endhighlight %}

#### 40) Trong trình duyệt, hãy chạy tệp **tests.html**. Bạn sẽ thấy giá trị văn bản hiển thị đến từ mã trang thay vì plugin.
<img align="center" alt="placeholder" src="/img/plugin-generator/passed-data.png" title="Data passed to the plugin">_Data passed to the plugin_


-----
### IX. Khuyến nghị
Bạn nên sử dụng trình tạo này cho tất cả các plugin của mình, ngay cả những plugin đơn giản. Bằng cách này, bạn sẽ luôn có cùng một thiết lập cho tất cả các plugin của mình. Nó cũng giải phóng bạn khỏi nhiệm vụ phải tạo các tập lệnh để thực hiện các chức năng nhất định, như linting hoặc minifying.

Với trình tạo này, bạn có thể tập trung vào phát triển và thử nghiệm plugin của mình mà không phải lo lắng về các công cụ cơ bản.

Bạn có thể giữ plugin của mình cục bộ hoặc đặt nó vào repo GitHub riêng tư của bạn. Tạo plugin videojs có nghĩa là nó sẽ hoạt động với trình phát Brightcove.


-----
### X. Resources
Dưới đây là một bản tóm tắt các tài nguyên bạn sẽ sử dụng trong khi làm việc thông qua sự khởi đầu nhanh chóng này. Các liên kết này cũng được cung cấp trong các bước dưới đây:
- Tải xuống và cài đặt: [Node.js](https://nodejs.org) (Điều này bao gồm npm) Sử dụng phiên bản "Recommended For Most Users".
- [video.js generator](https://github.com/videojs/generator-videojs-plugin)
- [video.js plugin conventions](https://github.com/videojs/generator-videojs-plugin/blob/master/docs/conventions.md)
- [Getting started with npm](https://docs.npmjs.com)
- [The yeoman scaffolding tool](https://yeoman.io)
- [Step-by-Step: Video.js Plugin Generator](https://support.brightcove.com/step-step-videojs-plugin-generator)
- [Step-by-Step: Plugin Development](https://support.brightcove.com/step-step-plugin-development)
- [Pass Data to the Plugin](https://support.brightcove.com/pass-data-plugin)

