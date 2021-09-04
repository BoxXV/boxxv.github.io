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

## Tại sao bạn nên tạo một thư viện JavaScript mới?

Bạn đã bao giờ thấy mình sao chép và dán các đoạn mã JavaScript giống nhau giữa các dự án khác nhau chưa? Chà, khi tình huống này xảy ra hai hoặc ba lần liên tiếp, đó thường là một dấu hiệu tốt cho thấy bạn có một đoạn mã hữu ích và có thể tái sử dụng.

Vì vậy, nếu bạn đang sử dụng lại mã của mình trong một số dự án khác nhau, tại sao không đi xa hơn và chuyển đổi nó thành một thư viện cho phép bạn tối ưu hóa việc chia sẻ mã này? Tạo thư viện sẽ cho phép bạn xây dựng các phiên bản khác nhau, theo dõi các lỗi mà bạn sửa và biết chính xác phiên bản nào đang sử dụng cho mỗi dự án.

Bài đăng này là tổng hợp các mẹo và kiến ​​thức từ nhóm Bugfender JS. Hãy tính đến những điểm sau khi tạo thư viện JavaScript mới và các nhà phát triển khác sẽ hài lòng khi sử dụng nó.


## Cách tốt nhất để tạo một thư viện JavaScript là gì?

Thư viện là một khái niệm mờ trong JavaScript hoặc jQuery . Không có bất kỳ định dạng cụ thể nào cho nó. Tuy nhiên, có nhiều thông số kỹ thuật (mặc dù npm là tiêu chuẩn trên thực tế).

Trong khi các nền tảng khác, như Android hoặc iOS, nêu rõ thư viện là gì, định dạng nó phải có và cách tích hợp nó vào một dự án, JavaScript không cung cấp bất kỳ cơ chế tích hợp nào. Nếu bạn là một nhà phát triển thiết bị di động và bạn đang tìm kiếm thứ gì đó giống như `JAR` hoặc `xcframeworks`, bạn sẽ không tìm thấy nó.


## Ok, Vậy Thư viện Javascript là gì?

Cho dù bạn tạo thư viện của mình bằng cách sử dụng cấu trúc npm hay các [tiêu chuẩn hiện đại](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) khác , nó có thể bao gồm bất kỳ thành phần phát triển chung nào, chẳng hạn như một thể hiện, một lớp, một hàm, một nguyên thủy hoặc một đối tượng (thậm chí là một đối tượng chứa tất cả các mục được liệt kê trước).

Thư viện JS có thể phức tạp như một đối tượng Singleton, với vòng đời riêng của nó và chạy các tác vụ của nó trong các luồng riêng biệt hoặc đơn giản như một tệp chứa một bộ công cụ tiện dụng.


## Cấu trúc Javascript Ưu tiên cho Thư viện vào năm 2020 là gì?

![npm](https://boxxv.github.io/img/posts/javascript-library.png "Node Package Manager")

Trước đây, bạn sẽ tạo một tệp mới, dán mã của bạn và đặt tệp này vào mọi dự án yêu cầu. Một quy ước chung là nhóm mọi thư viện đã sử dụng thành một dự án trong thư mục _vendors_. Thực tế này đã bị phá hoại bởi thực tế là khó quản lý các phụ thuộc và lập phiên bản. Ngoài ra, khi một thư viện cần sử dụng một thư viện khác, không có cách nào rõ ràng để xác định mối quan hệ này. Nó thậm chí còn phổ biến để tìm các thư viện sẽ sao chép và dán một thư viện đầy đủ khác vào bên trong để tránh các vấn đề phụ thuộc (thật không may, sao chép nhiều mã và ẩn những phụ thuộc này khỏi các nhà phát triển khác).

Vì lý do này, cách phổ biến nhất để tạo thư viện hiện nay là sử dụng `npm`. Các thư viện được tạo cho npm phải tuân theo một quy ước chính xác liên quan đến cấu trúc của chúng, vì vậy phải rõ ràng thư viện làm gì và những phụ thuộc nào khác được yêu cầu.

Chúng tôi đã viết một hướng dẫn đầy đủ về [cách tạo và phân phối thư viện JavaScript trong gói npm](https://boxxv.github.io/2022/01/01/how-to-create-an-npm-package/) , trong đó chúng tôi kết hợp quy trình làm việc chính thức với nhiều mẹo mà chúng tôi đã học được khi phát triển Bugfender JS.


### Nếu tôi không muốn sử dụng npm thì sao?

Nếu bạn muốn tạo thư viện của mình theo cách đơn giản nhất có thể, bạn có thể chỉ cần nhập mã của mình vào tệp JavaScript và đặt tệp này vào mọi dự án bạn muốn sử dụng.

Tuy nhiên, điều này làm tăng thêm vấn đề về lập phiên bản. Khi bạn cập nhật thư viện của mình, chẳng hạn như để sửa lỗi, bạn sẽ cần cập nhật tệp theo cách thủ công trong mọi dự án. Sử dụng hằng số cục bộ hoặc thậm chí là chú thích để đặt số phiên bản có thể xác định phiên bản thư viện bạn đang sử dụng, vì vậy bạn có một cách nhanh chóng để xác định phiên bản nào đang sử dụng mỗi dự án.

Sử dụng kho lưu trữ git trong `GitHub` để theo dõi các phiên bản phát hành khác nhau của mô-đun của bạn luôn là một ý tưởng hay.

Nếu thư viện của bạn có phụ thuộc với các thư viện khác, hãy nhớ ghi lại rõ ràng thư viện nào khác và phiên bản nào của chúng, là cần thiết để sử dụng nó.

Cũng cần lưu ý rằng mô-đun của bạn có thể cần được tải theo một thứ tự cụ thể.

Ví dụ, khi tích hợp Bugfender JS theo cách thủ công trong một dự án, cần phải sử dụng từ khóa `defer`.


## Tôi có nên sử dụng Javascript thuần túy hoặc Typescript khi tạo một thư viện mới không?

![npm](https://boxxv.github.io/img/posts/javascript-vs-typescript.png "Javascript vs Typescript")

`TypeScript` ngày càng trở thành lựa chọn ưu tiên khi tạo một thư viện mới. Vì TypeScript là một tập hợp siêu JavaScript nên tất cả mã nguồn của Typecript đều tương thích trực tiếp với tất cả các dự án JavaScript. Tuy nhiên, bạn sẽ nhận được một số đặc quyền khi tạo thư viện Typecript.

Ví dụ: trước khi xuất bản thư viện của bạn với Typescript, bạn sẽ cần phải biên dịch nó. Quá trình này xuất ra `types` thư viện của bạn. Có thể _types_ được hiểu là `header` các tệp và chúng rất hữu ích khi các nhà phát triển khác áp dụng mã của bạn. Một hàm Typecript _type_ rất dễ đọc và dễ hiểu vì nó được nêu rõ ràng những tham số nào sẽ nhận một hàm và những giá trị nào sẽ trả về.


## Quản lý luồng bên trong thư viện Javascript

Nói chung, các công cụ JavaScript là một luồng. Tuy nhiên, nếu thư viện của bạn cần thực hiện một số công việc chuyên sâu, bạn có thể đang chặn giao diện người dùng. Trong trường hợp này, Sử dụng [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) để chạy các tác vụ nền có thể là một lựa chọn tốt.

Web workers đi kèm với một số ràng buộc. Ví dụ: hãy cẩn thận với thao tác DOM, vì không thể thao tác trực tiếp _DOM_ hoặc truy cập một số API web. Nhưng chúng là một lựa chọn tuyệt vời cho các tác vụ mạng chuyên sâu liên quan đến sockets hoặc storage.


#### Ví dụ về web workers trong Bugfender

Từ kinh nghiệm của chúng tôi với SDK di động của chúng tôi, chúng tôi biết rằng một số người dùng sẽ đẩy SDK đến các giới hạn.

Để cung cấp cho bạn ý tưởng về sự đa dạng tuyệt đối của các nhà phát triển sử dụng Bugfender, ở một điểm cuối của quy mô, chúng tôi yêu cầu các nhà phát triển trò chơi gửi nhật ký từ Unreal Engine, một môi trường mà việc giữ mức độ thấp là bắt buộc để giữ tốc độ khung hình cao nhất có thể, và ở đầu bên kia, có các nhà phát triển sử dụng Bugfender để gỡ lỗi trạng thái của các cảm biến thời gian thực, gửi hàng trăm bản ghi mỗi giây.

Trong nền tảng di động, chúng tôi tự hào nói rằng những tác vụ này được hoàn thành với tác động hiệu suất không thể phân biệt được. Đó là nhờ cấu trúc dữ liệu tốt (được đánh bóng trong vài năm) cùng với việc sử dụng tốt các luồng nền.

Chúng tôi muốn Bugfender JS có khả năng duy trì hiệu suất tương đương trong nhiều trường hợp. Vì vậy, chúng tôi đang sử dụng Web workers để thực hiện các tác vụ nặng như tạm thời lưu trữ nhật ký trong `IndexedDB`, cho đến khi chúng có thể được gửi đến máy chủ Bugfender.


## Tính toán thứ tự mà thư viện của bạn sẽ được tải

Khi thêm Bugfender SDK vào ứng dụng web của bạn theo cách thủ công, bạn cần sử dụng khóa `defer`.

{% highlight html %}
<script defer src="https://js.bugfender.com/bugfender.js"></script>
{% endhighlight %}

Đó là bởi vì thứ tự mà bạn tải các tập lệnh không được đảm bảo. Bạn nên tính đến điều này nếu bạn tự tạo một thư viện và bạn muốn truy cập nó từ một tập lệnh khác.

Đây là một lý do khác để sử dụng npm. Nếu bạn làm điều đó, mọi thứ sẽ được tải trước trong một núi mã lớn, trong đó mọi thứ đều có thể truy cập được và bạn sẽ không cần phải lo lắng về điều đó nữa.


## Các bước để xuất bản Thư viện Javascript của tôi là gì?

Cho dù đây là một dự án cho chính bạn, một dự án mà bạn sẽ chia sẻ với nhóm công ty của mình hay một dự án mã nguồn mở, trước hết bạn cần ghi lại tài liệu mã của mình!

Nếu bạn không thêm tài liệu tốt vào thư viện của mình, đừng khó chịu khi đồng đội của bạn bắt đầu gửi cho bạn tin nhắn riêng tư trong Slack hoặc email hỏi cách sử dụng nó.

Thực ra, đó là trường hợp tốt nhất… thường thì họ sẽ bỏ qua thư viện của bạn!

Hãy nhớ rằng, không ai muốn dành thời gian của họ để kỹ thuật đảo ngược mã của bạn. Sau khi thư viện của bạn được tài liệu đầy đủ, bạn có thể tải nó lên GitHub và chia sẻ nó (hoặc thậm chí tốt hơn, hãy làm theo hướng dẫn của chúng tôi và [xuất bản nó lên npm](https://bugfender.com/blog/how-to-create-an-npm-package/) ).


## Where to Go From Here?

Tại Bugfender, chúng tôi là những nhà phát triển và chúng tôi muốn chia sẻ những kiến ​​thức của mình với cộng đồng. Bạn có thể đăng ký nhận bản tin hàng quý không có spam của chúng tôi trong hộp bên dưới hoặc bạn có thể tiếp tục đọc một trong các bài đăng liên quan sau:




-----
Tham khảo:
- [How to Create a JavaScript Library. 7 Tips to Create a Library That Every Developer Loves Using](https://bugfender.com/blog/how-to-create-a-javascript-library/)