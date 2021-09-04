---
layout: post
title: Hệ thống mô-đun JavaScript và xây dựng thư viện của riêng bạn
subtitle: Learn the basics of the JavaScript module system and build your own library
tags:
- module
- npm
- JavaScript
- library
---

Gần đây, tất cả chúng ta đã nghe nói nhiều về “Mô-đun JavaScript”. Mọi người có thể tự hỏi phải làm gì với chúng, và làm thế nào để chúng thậm chí đóng một vai trò quan trọng trong cuộc sống hàng ngày của chúng ta…? 

## Vậy hệ thống mô-đun JS là cái gì?

Khi sự phát triển của JavaScript ngày càng phổ biến, không gian tên và các phần phụ thuộc trở nên khó xử lý hơn nhiều. Các giải pháp khác nhau đã được phát triển để đối phó với vấn đề này dưới dạng các hệ thống mô-đun.

![npm](https://boxxv.github.io/img/posts/1 xM9pXLcsQa641gzCfTz0iw.jpeg "Javascript vs Typescript")


## Tại sao việc hiểu Hệ thống mô-đun JS lại quan trọng?

Hãy để tôi kể cho bạn một câu chuyện.

> Kể chuyện là cơ bản đối với con người như ăn uống. Hơn thế nữa, trên thực tế, trong khi thức ăn làm cho chúng ta sống, thì những câu chuyện mới là thứ khiến cuộc sống của chúng ta trở nên đáng sống - Richard Kearney 

Tại sao tôi lại nói về tất cả những thứ này?

Vì vậy, công việc hàng ngày của tôi là thiết kế và kiến trúc các dự án, và tôi nhanh chóng nhận ra rằng có nhiều chức năng chung được yêu cầu trong các dự án. Tôi luôn kết thúc việc sao chép và dán các chức năng đó vào các dự án mới nhiều lần.

Vấn đề là bất cứ khi nào một đoạn mã thay đổi, tôi cần phải đồng bộ hóa những thay đổi đó theo cách thủ công trên tất cả các dự án của mình. Để tránh tất cả các tác vụ thủ công tẻ nhạt này, tôi quyết định trích xuất các chức năng phổ biến và soạn một gói npm từ chúng. Bằng cách này, những người khác trong nhóm sẽ có thể sử dụng lại chúng làm phụ thuộc và chỉ cần cập nhật chúng bất cứ khi nào có bản phát hành mới.

Cách tiếp cận này có một số ưu điểm:

- Nếu có một số thay đổi trong thư viện lõi, thì thay đổi chỉ phải được thực hiện ở một nơi mà không cần cấu trúc lại mã của tất cả các ứng dụng cho cùng một thứ.
- Tất cả các ứng dụng vẫn đồng bộ. Bất cứ khi nào thay đổi được thực hiện, tất cả các ứng dụng chỉ cần chạy lệnh "npm update". 

![npm](https://boxxv.github.io/img/posts/1 aCeYnQZBAYNdxG4mkJCGrQ.png "Source code of library")

Vì vậy, bước tiếp theo là xuất bản thư viện. Bên phải? ?

Đây là phần khó khăn nhất, bởi vì có rất nhiều thứ nảy ra trong đầu tôi, như:

1. Làm cách nào để làm cho cây có thể rung chuyển?
2. Tôi nên nhắm mục tiêu hệ thống mô-đun JS nào (commonjs, amd, hài hòa).
3. Tôi có nên chuyển nguồn không?
4. Tôi có nên bó nguồn không?
5. Tôi nên xuất bản những tệp nào?

Mọi người trong chúng ta đều đã có những câu hỏi như thế này trong đầu khi tạo một thư viện. Bên phải?

Tôi sẽ cố gắng giải quyết tất cả các câu hỏi trên ngay bây giờ.

## Các loại hệ thống mô-đun JS khác nhau?

### 1. CommonJS

- Được thực hiện bởi **node**
- Được sử dụng cho **phía máy chủ** khi bạn đã cài đặt các mô-đun
- Không tải mô-đun thời gian chạy / không đồng bộ
- nhập qua "**request**"
- xuất qua “**module.exports**”
- Khi nhập bạn nhận lại một đối tượng
- Không có **cây rung**, vì khi nhập bạn nhận được một đối tượng
- Không có phân tích tĩnh, khi bạn lấy một đối tượng, vì vậy việc tra cứu thuộc tính đang ở thời gian chạy
- Bạn luôn nhận được bản sao của một đối tượng, vì vậy **không có thay đổi trực tiếp** nào trong chính mô-đun
- Quản lý phụ thuộc theo chu kỳ kém
- Cú pháp đơn giản

### 2. AMD: Async Module Definition

- Được thực hiện bởi **RequestJs**
- Được sử dụng cho **phía máy khách (trình duyệt)** khi bạn muốn tải động các mô-đun
- Nhập qua "yêu cầu"
- Cú pháp phức tạp

### 3. UMD: Universal Module Definition

- Sự kết hợp của **CommonJs + AMD** (nghĩa là Cú pháp của CommonJs + tải không đồng bộ của AMD)
- Sử dụng được cho cả môi trường **AMD/CommonJs**
- Về cơ bản, UMD tạo ra một cách để sử dụng một trong hai cách, đồng thời hỗ trợ định nghĩa biến toàn cục. Kết quả là, các mô-đun UMD có khả năng hoạt động trên cả **máy khách và máy chủ**.

### 4. ECMAScript Harmony (ES6)

- Được sử dụng cho cả phía **máy chủ/máy khách**
- **Thời gian chạy / tải tĩnh** của các mô-đun được hỗ trợ
- Khi bạn **import**, bạn nhận lại **giá trị ràng buộc** (giá trị thực tế)
- Nhập thông qua "import" và xuất khẩu qua "export"
- **Phân tích tĩnh** - Bạn có thể xác định nhập và xuất tại thời điểm biên dịch (tĩnh) - bạn chỉ phải xem mã nguồn, bạn không phải thực thi nó
- **Tree shakeable**, vì **phân tích tĩnh** được hỗ trợ bởi ES6
- Luôn nhận được một **giá trị thực tế** để thay đổi trực tiếp trong chính mô-đun
- Quản lý phụ thuộc theo chu kỳ tốt hơn CommonJS



Vì vậy, bây giờ bạn đã biết tất cả về các loại hệ thống mô-đun JS khác nhau và chúng đã phát triển như thế nào.

Mặc dù hệ thống mô-đun **ES Harmony** được hỗ trợ bởi tất cả các công cụ và trình duyệt hiện đại, chúng tôi không bao giờ biết khi xuất bản các thư viện người tiêu dùng của chúng tôi có thể sử dụng chúng như thế nào. Vì vậy chúng tôi phải luôn đảm bảo rằng các thư viện của chúng tôi hoạt động trong mọi môi trường.

Hãy đi sâu hơn và thiết kế một thư viện mẫu để trả lời tất cả các câu hỏi liên quan đến việc xuất bản thư viện theo cách thích hợp.

Tôi đã xây dựng một thư viện giao diện người dùng nhỏ (bạn có thể tìm thấy mã nguồn trên [GitHub](https://github.com/kamleshchandnani/js-module-system)) và tôi sẽ chia sẻ tất cả kinh nghiệm và khám phá của mình để chuyển đổi, đóng gói và xuất bản nó.

![npm](https://boxxv.github.io/img/posts/1 u1HxrxTNgFJmIVMd5I-ucw.png "Directory Structure")

Ở đây chúng ta có một thư viện giao diện người dùng nhỏ có 3 thành phần: Nút, Thẻ và NavBar. Hãy chuyển đổi và xuất bản nó từng bước.


## Các phương pháp hay nhất trước khi xuất bản?

### 1. Tree Shaking?

- **Tree shaking** là một thuật ngữ thường được sử dụng trong ngữ cảnh của JavaScript để loại bỏ dead-code. Nó dựa trên [cấu trúc tĩnh](https://exploringjs.com/es6/ch_modules.html#static-module-structure) của cú pháp mô-đun ES2015, tức là [`import`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) và [`export`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export). Tên và khái niệm đã được phổ biến bởi bản tổng hợp gói mô-đun ES2015 [rollup](https://github.com/rollup/rollup).
- Webpack và Rollup đều hỗ trợ **Tree Shaking**, có nghĩa là chúng ta cần lưu ý một số điều để mã của chúng ta có thể shaking được.

### 2. Publish all module variants

- Chúng tôi nên xuất bản tất cả các biến thể mô-đun, như `UMD` và `ES`, bởi vì chúng tôi không bao giờ biết được phiên bản trình duyệt / webpack mà người tiêu dùng của chúng tôi có thể sử dụng thư viện / gói này trong.
- Mặc dù tất cả các gói như [Webpack](https://webpack.js.org) và [Rollup](https://rollupjs.org) đều hiểu mô-đun ES, nhưng nếu người tiêu dùng của chúng tôi đang sử dụng `Webpack 1.x`, thì họ không thể hiểu mô-đun ES.

{% highlight js %}
// package.json
{% endhighlight %}

{% highlight js %}
{"name": "js-module-system","version": "0.0.1",...
{% endhighlight %}

{% highlight js %}
"main": "dist/index.js","module": "dist/index.es.js",
{% endhighlight %}

{% highlight js %}
...}
{% endhighlight %}

- Trường `main` của tệp `package.json` thường được dùng để trỏ đến phiên bản `UMD` của library/package.
- **Bạn có thể tự hỏi - làm cách nào tôi có thể phát hành phiên bản `ES` của library/package của mình?**
- Trường `module` của `package.json` được sử dụng để trỏ đến phiên bản ES của library/package. Trước đây, nhiều trường đã được sử dụng như `js:next` và `js:main`, nhưng `module` hiện đã được tiêu chuẩn hóa và được các nhà cung cấp gói sử dụng để tra cứu phiên bản `ES` của library/package.

> **Sự thật ít được biết đến**: Webpack sử dụng [resolve.mainfields](https://webpack.js.org/configuration/resolve/#resolve-mainfields) để xác định trường nào trong `package.json` được kiểm tra.

> **Mẹo về hiệu suất**: Luôn cố gắng xuất bản phiên bản `ES` của library/package của bạn, vì tất cả các trình duyệt hiện đại hiện hỗ trợ mô-đun `ES`. Vì vậy, bạn có thể truyền tải ít mã hơn và cuối cùng bạn sẽ vận chuyển ít mã hơn cho người dùng của mình. Điều này sẽ tăng hiệu suất ứng dụng của bạn.

**Vì vậy, bây giờ là gì tiếp theo? Vận chuyển hay bó lại? Chúng ta nên sử dụng những công cụ nào?**

Ah, đây là phần khó nhất! Hãy đi sâu vào.?


## Webpack vs Rollup vs Babel?

Đây là tất cả các công cụ chúng ta sử dụng trong cuộc sống hàng ngày để gửi các ứng dụng / thư viện / gói của chúng ta. Tôi không thể tưởng tượng sự phát triển web hiện đại mà không có chúng - **#blessed**. Vì vậy, chúng tôi không thể so sánh chúng, vì vậy đó sẽ là một câu hỏi sai để đặt ra! ❌

Mỗi công cụ có những lợi ích riêng và phục vụ các mục đích khác nhau dựa trên nhu cầu của bạn.

Bây giờ chúng ta hãy xem xét từng công cụ sau:

### Webpack

[Webpack](https://webpack.js.org) là một trình gói mô-đun tuyệt vời? được chấp nhận rộng rãi và chủ yếu được sử dụng để xây dựng các SPA. Nó cung cấp cho bạn tất cả các tính năng như tách mã ([code splitting](https://webpack.js.org/guides/code-splitting/)), [tải không đồng bộ](https://webpack.js.org/guides/code-splitting/#dynamic-imports) các gói, [tree shaking](https://webpack.js.org/guides/tree-shaking/), v.v. Nó sử dụng hệ thống mô-đun **CommonJS**.

PS: [Webpack-4.0.0](https://github.com/webpack/webpack/issues/6064) alpha đã ra mắt chưa ?. Hy vọng rằng với bản phát hành ổn định, nó sẽ trở thành gói phổ biến cho tất cả các loại hệ thống mô-đun.

### RollupJS

[Rollup](https://rollupjs.org) cũng là một gói mô-đun tương tự như Webpack. Tuy nhiên, ưu điểm chính của cuộn lên là nó tuân theo định dạng chuẩn hóa mới cho các mô-đun mã có trong bản sửa đổi `ES6`, vì vậy bạn có thể sử dụng nó để gói biến thể `mô-đun ES` của library/package của bạn. Nó không hỗ trợ tcác gói **ải không đồng bộ**.

### Babel

[Babel](https://babeljs.io) là một trình chuyển tiếp (transpiler) cho JavaScript được biết đến nhiều nhất với khả năng biến mã ES6 thành mã chạy trong trình duyệt của bạn (hoặc trên máy chủ của bạn) hiện nay. Hãy nhớ rằng nó chỉ chuyển vị và không gói mã của bạn.

Lời khuyên của tôi: sử dụng Rollup cho thư viện và Webpack cho ứng dụng.

### Transpile (Babel-ify) the source or Bundle it

Một lần nữa, có một câu chuyện đằng sau câu chuyện này. ?

Tôi đã dành hầu hết thời gian của mình để cố gắng tìm ra câu trả lời cho câu hỏi này khi tôi xây dựng thư viện này. Tôi bắt đầu đào node_modules của mình để tra cứu tất cả các thư viện tuyệt vời và kiểm tra các hệ thống xây dựng của chúng.

![npm](https://boxxv.github.io/img/posts/1 JJ0hPQW4V7rnaCVHO0nV4w.jpeg "Libraries vs Packages build output comparision")

Sau khi xem xét kết quả xây dựng cho các thư viện / gói khác nhau, tôi có một bức tranh rõ ràng về những chiến lược khác nhau mà tác giả của những thư viện này có thể đã nghĩ đến trước khi xuất bản. Dưới đây là những quan sát của tôi.

Như bạn có thể thấy trong hình ảnh trên, tôi đã chia các thư viện / gói này thành hai nhóm dựa trên đặc điểm của chúng:

1. Thư viện giao diện người dùng UI (`styled-components`, `material-ui`)
2. Core Packages (`react`, `react-dom`)

Nếu bạn là một người quan sát tốt? bạn có thể đã tìm ra sự khác biệt giữa hai nhóm này.

**UI** Thư viện giao diện người dùng có một thư mục `dist` có phiên bản được đóng gói và rút gọn cho các hệ thống mô-đun `ES` và `UMD/CJS` làm mục tiêu. Có một thư mục `lib` có phiên bản chuyển đổi của thư viện.

Các `Core Packages` chỉ có một thư mục có phiên bản được đóng gói và rút gọn cho hệ thống mô-đun `CJS` hoặc `UMD` làm mục tiêu.

**Nhưng tại sao lại có sự khác biệt trong kết quả xây dựng của thư viện UI và Gói lõi?**


### UI Libraries

Hãy tưởng tượng nếu chúng ta chỉ xuất bản phiên bản đi kèm của thư viện và lưu trữ nó trên CDN. Người tiêu dùng của chúng tôi sẽ sử dụng nó trực tiếp trong thẻ <script />. Bây giờ nếu người tiêu dùng của tôi chỉ muốn sử dụng thành phần <; Button />, họ phải tải toàn bộ thư viện. Ngoài ra, trong trình duyệt, không có gói nào xử lý việc rung cây và cuối cùng chúng tôi sẽ vận chuyển toàn bộ mã thư viện cho người tiêu dùng của chúng tôi. Chúng tôi không muốn điều này.

{% highlight js %}
<script type="module">import {Button} from "https://unpkg.com/uilibrary/index.js";</script>
{% endhighlight %}

Bây giờ nếu chúng ta chỉ cần chuyển src thành lib và lưu trữ lib trên CDN, người tiêu dùng của chúng ta thực sự có thể nhận được bất cứ thứ gì họ muốn mà không cần bất kỳ chi phí nào. “Gửi ít hơn, tải nhanh hơn”. ✅

{% highlight js %}
<script type="module">import {Button} from "https://unpkg.com/uilibrary/lib/button.js";</script>
{% endhighlight %}

### Core Packages

Các gói cốt lõi không bao giờ được sử dụng thông qua thẻ <script />, vì chúng cần phải là một phần của ứng dụng chính. Vì vậy, chúng tôi có thể an toàn phát hành phiên bản đi kèm (UMD, ES) cho các loại gói này và để hệ thống xây dựng cho người tiêu dùng.

Ví dụ: họ có thể sử dụng biến thể UMD nhưng không rung cây hoặc họ có thể sử dụng biến thể ES nếu trình kết hợp có khả năng xác định và nhận được lợi ích của việc rung cây.

{% highlight js %}
// CJS requireconst Button = require("uilibrary/button");
{% endhighlight %}


{% highlight js %}
// CJS requireconst Button = require("uilibrary/button");
{% endhighlight %}

Nhưng… còn câu hỏi của chúng ta: chúng ta nên chuyển (Babelify) nguồn hay gộp nó lại? ?

Đối với Thư viện giao diện người dùng, chúng ta cần chuyển mã nguồn bằng Babel với hệ thống mô-đun es làm đích và đặt nó trong lib. Chúng tôi thậm chí có thể lưu trữ lib trên CDN.

Chúng ta nên gói và rút gọn nguồn bằng cách sử dụng cuộn lên cho hệ thống mô-đun cjs / umd và hệ thống mô-đun es làm mục tiêu. Sửa đổi package.json để trỏ đến các hệ thống đích thích hợp.

{% highlight js %}
// package.json
{% endhighlight %}

{% highlight js %}
{"name": "js-module-system","version": "0.0.1",...
{% endhighlight %}

{% highlight js %}
"main": "dist/index.js",-   // for umd/cjs builds"module": "dist/index.es.js", // for es build
{% endhighlight %}

{% highlight js %}
...}
{% endhighlight %}

Đối với các gói cốt lõi, chúng tôi không cần phiên bản lib.

Chúng ta chỉ cần gói và rút gọn nguồn bằng cách sử dụng cuộn lên cho hệ thống mô-đun cjs / umd và hệ thống mô-đun es làm mục tiêu. Sửa đổi package.json để trỏ đến các hệ thống đích thích hợp, giống như ở trên.

Mẹo: Chúng tôi cũng có thể lưu trữ thư mục dist trên CDN, cho những người tiêu dùng sẵn sàng tải xuống toàn bộ thư viện / gói thông qua thẻ <script />.


## Chúng ta nên xây dựng cái này như thế nào?

Chúng ta nên có các tập lệnh khác nhau cho từng hệ thống đích trong package.json. Bạn có thể tìm thấy cấu hình cuộn lên trong repo GitHub.

{% highlight js %}
// package.json
{% endhighlight %}

{% highlight js %}
{..."scripts": {"clean": "rimraf dist","build": "run-s clean && run-p build:es build:cjs build:lib:es","build:es": "NODE_ENV=es rollup -c","build:cjs": "NODE_ENV=cjs rollup -c","build:lib:es": "BABEL_ENV=es babel src -d lib"}...}
{% endhighlight %}

## Chúng ta nên xuất bản những gì?

- License
- README
- Changelog
- Metadata(main , module, bin) — package.json
- Control through package.json files property

Trong package.json, trường "tệp" là một mảng các mẫu tệp mô tả các mục nhập sẽ được đưa vào khi gói của bạn được cài đặt dưới dạng phụ thuộc. Nếu bạn đặt tên một thư mục trong mảng, thì nó cũng sẽ bao gồm các tệp bên trong thư mục đó.

Chúng tôi sẽ bao gồm các thư mục lib và dist trong trường "tệp" trong trường hợp của chúng tôi. 

{% highlight js %}
// package.json
{% endhighlight %}

{% highlight js %}
{..."files": ["dist", "lib"]...}
{% endhighlight %}

Cuối cùng thì thư viện đã sẵn sàng để xuất bản. Chỉ cần gõ lệnh npm run build trong terminal và bạn có thể thấy kết quả sau. Xem kỹ các thư mục dist và lib. ?

![npm](https://boxxv.github.io/img/posts/1 C0wMVo17NTVcTroA8dPe9g.png "Ready to publish ?")


## Gói lại

Ồ! Thời gian trôi bao lâu rồi? Đó là một chuyến đi hoang dã, nhưng tôi thực sự hy vọng nó đã giúp bạn hiểu rõ hơn về hệ thống Mô-đun JavaScript và cách bạn có thể tạo thư viện của riêng mình và xuất bản nó.

Chỉ cần đảm bảo rằng bạn quan tâm đến những điều sau:

1. Làm cho nó Cây có thể Rung. ?
2. Nhắm mục tiêu ít nhất là hệ thống mô-đun ES Harmony và CJS. ?
3. Sử dụng Babel và Bundlers cho các thư viện. ?
4. Sử dụng Bundlers cho các gói Core. ?
5. Đặt trường mô-đun của package.json trỏ đến phiên bản ES của mô-đun của bạn (PS: Nó giúp rung cây). ?
6. Xuất bản các thư mục đã chuyển đổi cũng như các phiên bản đi kèm của mô-đun của bạn. ? 


## Xu hướng trong tuần này?

1. Webpack-V4 alpha được phát hành. ?
2. ParcelJs: Gói ứng dụng web không cấu hình nhanh chóng. ?
3. Turbo: Nhanh hơn gấp 5 lần so với Yarn & NPM và chạy nguyên bản trong trình duyệt?

Cảm ơn Juho Vepsäläinen và Lakshya Ranganath vì những đánh giá và phản hồi của họ, Sean T. Larkin và Tobias Koppers đã chia sẻ những hiểu biết sâu sắc về webpack tại ReactiveConf, Addy Osmani vì đã chia sẻ hoạt động của các Hệ thống mô-đun JS khác nhau trong “Viết JavaScript mô-đun với AMD, CommonJS & ES Hòa hợp".

P.S. Nếu bạn thích điều này, hãy chắc chắn giới thiệu (bằng cách vỗ tay?), Theo dõi tôi trên twitter và chia sẻ điều này với bạn bè của bạn!?


-----
Tham khảo:
- [How to Create a JavaScript Library. 7 Tips to Create a Library That Every Developer Loves Using](https://bugfender.com/blog/how-to-create-a-javascript-library/)