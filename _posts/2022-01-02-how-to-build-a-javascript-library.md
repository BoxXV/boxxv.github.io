---
layout: post
title: Cách tạo Thư viện JavaScript
title: Cách xây dựng Thư viện JavaScript
subtitle: Viết thư viện Lightbox hình ảnh không có phụ thuộc đơn giản
image: "img/js.jpg"
tags:
- module
- npm
- JavaScript
- library
---

Nếu bạn là nhà phát triển, gần như chắc chắn rằng bạn đã sử dụng Thư viện. Nói một cách dễ hiểu, Thư viện là một tập hợp các mã có thể sử dụng lại mà bạn có thể sử dụng trong chương trình của mình.

Giống như hầu hết chúng ta, tôi biết cách cắm các thư viện vào chương trình của mình và sử dụng chúng, nhưng tôi thường thấy sợ mỗi khi xem qua mã nguồn thực của thư viện cụ thể đó. Sau đó, tôi bắt đầu học Vanilla JS và tất cả đều không còn đáng sợ nữa. Vanilla JS là mã JavaScript đơn giản mà bạn viết mà không cần sử dụng bất kỳ thư viện bên ngoài nào.

Khi nói đến việc xây dựng một thư viện JavaScript mà bạn sẽ sử dụng để tạo một trang web, điều quan trọng là bạn phải học thao tác DOM bằng cách sử dụng Vanilla JS trước khi cố gắng thực sự xây dựng nó. Lý do quan trọng là bạn sẽ không có bất kỳ phụ thuộc nào và thư viện của bạn sẽ chỉ là một plug-n-play cho người dùng của bạn. Bạn có thể quen với thao tác DOM bằng jQuery nhưng điều đó sẽ tạo ra sự phụ thuộc vào jQuery và thư viện của bạn sẽ không hoạt động trên trang web không bao gồm tham chiếu đến thư viện jQuery.

Nếu bạn đã quen với jQuery và muốn tìm hiểu thêm về thao tác DOM bằng Vanilla JS, bạn có thể đọc thêm về nó [tại đây](https://faisalrashid.tech/blogs/JavaScript-vs-jQuery).

Với tất cả những gì đã nói, hãy đi sâu vào việc tạo Thư viện JavaScript từ đầu.

Chúng tôi sẽ xây dựng `Image Lightbox`. Lightbox là một thư viện được sử dụng để xem hình ảnh trên trang web bằng cách lấp đầy trang bằng hình ảnh và giảm làm nổi nền. Đây là những gì chúng tôi sẽ xây dựng.

![Image Lightbox](https://boxxv.github.io/img/posts/fs-ligthbox.gif "Image Lightbox")

Nếu bạn muốn tiếp tục và xem mã, bạn có thể tìm thấy kho lưu trữ GitHub [tại đây](https://github.com/FaisalST32/fs-lightbox).

Khi xây dựng Thư viện JavaScript, có một số điều bạn muốn lưu ý.

Mã của bạn không được can thiệp vào mã hiện có do người dùng viết.
Để làm điều này, chúng tôi sẽ đóng gói tất cả mã của chúng tôi trong một đối tượng Hàm duy nhất.

{% highlight js %}
function FsLightbox() {
	// all the code goes here 
}
{% endhighlight %}


-----
Tham khảo:
- [How to build a JavaScript Library](https://faisalrashid.tech/blogs/How-to-build-a-JavaScript-Library)
- [How to build a JavaScript Library](https://levelup.gitconnected.com/how-to-build-a-javascript-library-6b7161315f3d)
- [39 of the best JavaScript libraries and frameworks to try in 2021](https://getflywheel.com/layout/best-javascript-libraries-frameworks-2020/)
