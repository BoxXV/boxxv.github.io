---
layout: post
title: Cách tạo Thư viện JavaScript
subtitle: 7 mẹo để tạo một thư viện mà mọi nhà phát triển yêu thích sử dụng
tags:
- Tips
- Tricks
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

Chúng tôi đã viết một hướng dẫn đầy đủ về [cách tạo và phân phối thư viện JavaScript trong gói npm](https://boxxv.github.io/2022/01/01/creating-modern-javascript-library/) , trong đó chúng tôi kết hợp quy trình làm việc chính thức với nhiều mẹo mà chúng tôi đã học được khi phát triển Bugfender JS.


### Nếu tôi không muốn sử dụng npm thì sao?

Nếu bạn muốn tạo thư viện của mình theo cách đơn giản nhất có thể, bạn có thể chỉ cần nhập mã của mình vào tệp JavaScript và đặt tệp này vào mọi dự án bạn muốn sử dụng.

Tuy nhiên, điều này làm tăng thêm vấn đề về lập phiên bản. Khi bạn cập nhật thư viện của mình, chẳng hạn như để sửa lỗi, bạn sẽ cần cập nhật tệp theo cách thủ công trong mọi dự án. Sử dụng hằng số cục bộ hoặc thậm chí là chú thích để đặt số phiên bản có thể xác định phiên bản thư viện bạn đang sử dụng, vì vậy bạn có một cách nhanh chóng để xác định phiên bản nào đang sử dụng mỗi dự án.

Sử dụng kho lưu trữ git trong `GitHub` để theo dõi các phiên bản phát hành khác nhau của mô-đun của bạn luôn là một ý tưởng hay.

Nếu thư viện của bạn có phụ thuộc với các thư viện khác, hãy nhớ ghi lại rõ ràng thư viện nào khác và phiên bản nào của chúng, là cần thiết để sử dụng nó.

Cũng cần lưu ý rằng mô-đun của bạn có thể cần được tải theo một thứ tự cụ thể.

Ví dụ, khi tích hợp Bugfender JS theo cách thủ công trong một dự án, cần phải sử dụng từ khóa `defer`.








-----
Tham khảo:
- [How to Create a JavaScript Library. 7 Tips to Create a Library That Every Developer Loves Using](https://bugfender.com/blog/how-to-create-a-javascript-library/)