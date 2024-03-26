---
layout: post
title: So sánh công cụ kiểm thử API
subtitle: A Free Solution with the Best Alternative
image: "img/api.jpg"
tags:
- API
- Automated testing
---

API testing là một loại kiểm thử phần mềm bao gồm kiểm thử giao diện lập trình ứng dụng (API) một cách trực tiếp hoặc như một phần của kiểm thử tích hợp để xác định xem chúng có đáp ứng được mong đợi về chức năng, độ tin cậy, hiệu suất và bảo mật không.

Kiểm thử API là một trong những bước quan trọng nhất trong quá trình phát triển để kiểm thử kết quả đầu cuối . Nếu không kiểm thử API thì bạn không thể biết được data do server trả về có chính xác hay không, có thể tham số required bị sai, thiếu quyền truy cập hoặc server không được kết nối, ứng dụng của bạn không hoạt động. Ứng dụng không hoạt động thì khách hàng không thể sử dụng được ứng dụng, điều đó ảnh hưởng trực tiếp tới team dự án. Khi đó khả năng phải giải trình về các nguyên nhân đó rất dễ xảy ra.

Vì thế mà các công cụ kiểm thử API ra đời. Các công cụ này đã giúp developers, testers... kiểm tra khi nhận 1 bộ dữ liệu cụ thể từ server xuống App có cho phản hồi đúng mong đợi hay không. Đây là 1 ý tưởng đơn giản, nhưng sẽ rất hữu ích đối với chúng ta cũng như vòng đời phát triển phần mềm.

![API](https://boxxv.github.io/img/2024/c53f283e-6834-45b6-beb9-57b10b2a22fd_1280x1664.webp "API")

## Lợi ích của công cụ kiểm thử API

Một số lợi ích phổ biến khi sử dụng công cụ kiểm thử API:
- Dùng công cụ kiểm thử API sẽ hỗ trợ công việc của bạn nhanh chóng kiểm thử được kết quả cuối cùng mà không cần hiểu toàn bộ luồng nghiệp vụ
- Ít phải tương tác với câu lệnh
- Có nhiều cách để cài đặt authorization
- Định dạng của code gửi và nhận rõ ràng hơn
- Kiểm thử hiệu năng và độ tin cậy dễ dàng hơn

### Điểm chung của công cụ kiểm thử

Những ưu điểm của công cụ:
- Là phiên bản phần mềm miễn phí dành cho người dùng (bất cứ lúc nào cần có thể nâng cấp lên phiên bản trả phí sẽ có nhiều tính năng hơn)
- Là các phần mềm mã nguồn mở
- Cho phép nhiều môi trường làm việc (development, acceptance, prod,...)
- Các biến môi trường và cục bộ có khả năng được cập nhật mỗi khi có yêu cầu được gửi đến endpoint ( đôi khi là chuỗi yêu cầu)
- Cho phép imports và exports dữ liệu test một cách dễ dàng để chia sẻ chúng với team member
- Có khả năng lưu các câu lệnh và sắp xếp chúng vào foldes hoặc bộ sưu tập
- Hỗ trợ các lựa chọn kiểm thử và tích hợp GraphQL
- Có nhiều cách để cấu hình authorization (OAuth, bearer tokens, Basic, HAWK, etc.) và generate / manage cookies
- Cả 2 ứng dụng đều có dark/ light theme (đây không phải là vấn đề lớn, tuy nhiên nó tạo cảm hứng tốt trong lúc làm việc)

## Postman

Postman có 1 bộ sản phẩm và các tính năng của nó mạnh mẽ hơn nhiều khi thực sự đi sâu vào tìm hiểu tài liệu. Có một số thứ khiến Postman khác biệt với các công cụ kiểm thử API khác như:

- Tài liệu API (Postman sẽ tạo và lưu trữ tài liệu API dựa trên trình duyệt trong thời gian thực)
- Collection runs ( Chạy một nhóm các yêu cầu như một chuỗi với môi trường tương ứng - điều này cực kỳ hữu ích cho kiểm thử tự động )
- Theo dõi nơi Postman định kỳ chạy bộ dữ liệu để kiểm tra hiệu suất và phản hồi của nó
- Các kịch bản test được viết bằng Javascript sẽ hỗ trợ kiểm tra các kết quả phản hồi, thời gian ... từ endpoint.
- Các server giả lập giúp các team mô phỏng từng endpoint và response tương ứng trong Postman Collection. Developers có thể xem các phản hồi mà không cần đến Back- End, các thành viên trong team cũng có thể được sắp xếp một cách sớm và hợp lý nhất trong các giai đoạn phát triển API.

## Insomnia

Insomnia có một số tính năng đặc biệt mà Postman không cung cấp như:

- Template tags (tương tự như biến môi trường nhưng chúng thực hiện các thao tác trên strings, timestamps,...)
- Khả năng tạo mới plugins cho cộng đồng Insomnia.
- Hỗ trợ Client certificate assignments và SSL validation (hoặc disable nó),
- Hỗ trợ 12 ngôn ngữ khác nhau (rất tiện dụng nếu bạn muốn chạy lệnh bằng CURL hoặc cho nó vào code thực tế)
- Có một khu vực lưu tài liệu rất chi tiết, như hướng dẫn, code và thậm chí cả dữ liệu kiểm thử có thể thêm vào các calls hoặc collections cụ thể
- Xem phản hồi cả bằng JSON và XML (với Insomnia có thể xem trang HTML, hình ảnh, SVG, tệp âm thanh và thậm chí cả tài liệu pdf )

## 


Cảm ơn bạn đã đọc bài viết này của tôi, hy vọng rằng nó sẽ hữu ích và giúp bạn hiểu rõ hơn để lựa chọn tốt nhất trong công việc kiểm thử API của mình.

-----
- [So sánh công cụ kiểm thử API Postman vs Insomnia](https://viblo.asia/p/so-sanh-cong-cu-kiem-thu-api-postman-vs-insomnia-Qbq5QyD45D8)
- [Free Postman Limitations: A Free Solution with the Best Alternative](https://apidog.com/blog/postman-plan-limitations-free-solution/)
- [Giới thiệu Postman Flows - Tạo chuỗi xử lý các Request, Response với Postman](https://viblo.asia/p/gioi-thieu-postman-flows-tao-chuoi-xu-ly-cac-request-response-voi-postman-3P0lPBEPKox)

- [Automated testing with Postman](https://www.postman.com/automated-testing/)
- [thunderclient.com](https://www.thunderclient.com)
- [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)
- [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)
- [rest-assured.io](https://rest-assured.io)
- [Thunder Client CLI — A new way to test APIs inside VS Code](https://medium.com/thunderclient/thunder-client-cli-a-new-way-to-test-apis-inside-vscode-d91eb5c71d8e)
- [Sử dụng Thunder Client ngay trên VSCode để thay thế Postman](https://thangdangblog.com/su-dung-thunder-client-ngay-tren-vscode-de-thay-the-postman/)

- [Paypal api](https://www.postman.com/paypal/workspace/paypal-public-api-workspace/collection/19024122-92a85d0e-51e7-47da-9f83-c45dcb1cdf24)

- [Testing Cross-Site Scripting](https://viblo.asia/p/testing-cross-site-scripting-4P8566jL5Y3)
- [Tản mạn về API security](https://viblo.asia/p/tan-man-ve-api-security-5pPLk9bd4RZ)