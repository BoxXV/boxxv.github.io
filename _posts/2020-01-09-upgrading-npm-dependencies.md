---
layout: post
title: Upgrading npm dependencies
subtitle: Cập nhật các thư viện phụ thuộc trong NPM
---

Làm thế nào chúng ta có thể nâng cấp một cách an toàn các phụ thuộc npm trong dự án của chúng ta? Các ký tự ^ và ~ có nghĩa là gì trước các phiên bản gói phụ thuộc? Làm thế nào chúng ta có thể nâng cấp phiên bản chính trên một phụ thuộc npm trong dự án của chúng ta? Chúng ta sẽ tìm ra trong bài viết này.

### Version parts
Phiên bản gói npm theo quy tắc đánh version cho software gọi là Semantic Versioning. Vì vậy, một phiên bản gói có 3 phần - Major.Minor.Patch
- Major: tăng khi bạn thực hiện các thay đổi dẫn đến KHÔNG tương thích ngược.
- Minor: tăng khi bạn thêm tính năng và vẫn đảm bảo tương thích ngược (backwards-compatible).
- Patch: tăng khi bạn thực hiện fix lỗi xử lý bên trong và vẫn đảm bảo tương thích ngược (backwards-compatible)

### ^ Và ~ có nghĩa là gì?

Một phiên bản thường có một ^ ở phía trước của nó (ví dụ ^ 16.8.6). Điều này có nghĩa là phiên bản nhỏ mới nhất có thể được cài đặt an toàn. Vì vậy, trong ví dụ này, ^ 16.12.1 có thể được cài đặt an toàn nếu đây là phiên bản mới nhất trong 16.x.

Đôi khi, một phiên bản có ~ ở phía trước của nó (ví dụ: ~ 16.8.6). Điều này có nghĩa là chỉ có phiên bản vá mới nhất có thể được cài đặt an toàn. Vì vậy, trong ví dụ này, ^ 16.8.12 có thể được cài đặt an toàn nếu đây là phiên bản mới nhất trong 16.8.x.


### Vì vậy, `npm install` cài đặt phiên bản an toàn mới nhất của các phụ thuộc?

Có và không!

Nếu các gói đã được cài đặt vào thư mục `node_modules`, thì `npm install` sẽ không cập nhật bất kỳ gói nào.

Nếu các gói chưa được cài đặt và tồn tại trong tệp `pack-lock.json`, thì `npm install` sẽ cài đặt các phiên bản phụ thuộc chính xác được chỉ định trong gói-lock.json.

`npm install` sẽ cài đặt phiên bản an toàn mới nhất của các phụ thuộc nếu chúng không tồn tại trong thư mục `node_modules` và không có tệp `pack-lock.json`. Tuy nhiên, bạn có thể nghĩ rằng phiên bản an toàn mới nhất đã được cài đặt vì `package.json` không thay đổi, nhưng nếu bạn kiểm tra các gói trong thư mục `node_modules`, phiên bản an toàn mới nhất sẽ được cài đặt.


### Vì vậy, làm thế nào để tôi cập nhật một cách an toàn tất cả các phụ thuộc?

Thứ nhất, các phụ thuộc đã hết hạn có thể được phát hiện bằng cách chạy lệnh sau:

{% highlight js %}
npm outdated
{% endhighlight %}

Các phụ thuộc sẽ được liệt kê ra:

![npm-outdated](http://boxxv.com/img/posts/npm-outdated.png "npm-outdated")

Phiên bản mong muốn là phiên bản an toàn mới nhất có thể được thực hiện (theo phiên bản ngữ nghĩa và tiền tố ^ hoặc ~). Phiên bản mới nhất là phiên bản mới nhất có sẵn trong sổ đăng ký npm.

Tất cả các phụ thuộc có thể được cập nhật an toàn lên phiên bản mong muốn bằng cách sử dụng lệnh sau:

{% highlight js %}
npm update
{% endhighlight %}

Cũng như cập nhật các gói trong thư mục `node_modules`, các tệp `pack.json` và `package-lock.json` sẽ được cập nhật.


Nếu bạn không muốn cập nhật tất cả các gói, thì tên gói có thể được chỉ định ở cuối lệnh:

{% highlight js %}
npm update "react" "react-dom"
{% endhighlight %}

React được cập nhật trong ví dụ trên.


### Cập nhật tất cả các phụ thuộc với những thay đổi lớn

Vì vậy, làm thế nào để chúng tôi nâng cấp phụ thuộc khi đã có một sự thay đổi phiên bản lớn?

Có lẽ cách an toàn nhất là như sau:
- Kiểm tra thay đổi của gói phụ thuộc để biết các thay đổi có thể ảnh hưởng đến ứng dụng của chúng ta
- Nếu chúng tôi nghĩ rằng chúng tôi an toàn để thực hiện nâng cấp, hãy chạy lệnh sau:
{% highlight js %}npm install <packagename>@latest{% endhighlight %}
- Nếu nhiều gói đi cùng nhau, bạn có thể liệt kê tất cả chúng ra. Ví dụ dưới đây sẽ cập nhật React lên phiên bản mới nhất:
{% highlight js %}npm install react@latest react-dom@latest{% endhighlight %}
- Xác minh ứng dụng không bị hỏng bằng cách thực hiện một số thử nghiệm
- Lặp lại quy trình cho các gói khác khi có sự thay đổi phiên bản chính

Có cách nào nhanh hơn để chỉ cập nhật tất cả các phụ thuộc, bao gồm các thay đổi phiên bản chính? Vì vậy, như `npm update` nhưng đối với các bản cập nhật lớn là tốt?

Vâng, có một công cụ gọi là [npm-check-update](https://github.com/raineorshine/npm-check-updates) sẽ làm điều này. Chỉ cần chạy lệnh sau:

{% highlight js %}
npx npm-check-updates -u
{% endhighlight %}

Điều này sẽ cập nhật các phụ thuộc lên các phiên bản mới nhất (bao gồm các thay đổi phiên bản chính) trong `package.json`. Nếu chúng ta vui lòng tiếp tục nâng cấp, chúng ta cần chạy lệnh sau:

{% highlight js %}
npm install
{% endhighlight %}

Điều này sau đó sẽ nâng cấp các gói trong thư mục `node_modules` và `package-lock.json` cũng sẽ được cập nhật.


### Tóm lại

- Sử dụng `npm outdated` để khám phá các phụ thuộc đã lỗi thời
- Sử dụng `npm update` để thực hiện nâng cấp phụ thuộc an toàn
- Sử dụng `npm install <packagename>@latest` để nâng cấp lên phiên bản chính mới nhất của gói
- Sử dụng `npx npm-check-updates -u` và `npm install` tất cả các phụ thuộc lên các phiên bản chính mới nhất của chúng


-----
Tham khảo:
- [Upgrading npm dependencies](https://www.carlrippon.com/upgrading-npm-dependencies/)
- [Cùng tìm hiểu về Npm và package](https://codelearn.io/sharing/cung-tim-hieu-ve-npm-va-package)
- [Sự Khác Nhau Giữa devDependencies và Dependencies](https://hungphamdevweb.com/devdependencies-dependencies-va-su-khac-nhau.html)
- [Sử dụng npm như một Build Tool](https://viblo.asia/p/su-dung-npm-nhu-mot-build-tool-jdWrvwq8Mw38)
- [Câu hỏi phỏng vấn: Liệt kê npm package dependencies](https://medium.com/@dinhthibc/c%C3%A2u-h%E1%BB%8Fi-ph%E1%BB%8Fng-v%E1%BA%A5n-li%E1%BB%87t-k%C3%AA-npm-package-dependencies-18806ffc632d)