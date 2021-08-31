---
layout: post
title: Thiết kế CSDL sản phẩm cho nhiều loại sản phẩm
subtitle: Database Schema for Multiple Types of Products
image: "img/projects-bg.jpg"
tags:
- CSDL
- Database
- Schema
- Multiple Types
---

Mục tiêu của là tạo một hoặc nhiều bảng `sản phẩm` đáp ứng các yêu cầu:
- Hỗ trợ nhiều loại sản phẩm (TV, Điện thoại, PC, ...). Mỗi loại sản phẩm có một bộ thông số khác nhau, như:
    + Điện thoại sẽ có Màu sắc, Kích thước, Trọng lượng, Hệ điều hành ...
    + PC sẽ có CPU, HDD, RAM ...
- Tập hợp các tham số phải là động. Bạn có thể thêm hoặc chỉnh sửa bất kỳ thông số nào bạn thích.

Có ít nhất năm tùy chọn này để lập mô hình phân cấp:

- [Single Table Inheritance](martinfowler.com/eaaCatalog/singleTableInheritance.html): Kế thừa một bảng - một bảng cho tất cả các loại Sản phẩm, có đủ cột để lưu trữ tất cả các thuộc tính của tất cả các loại. Điều này có nghĩa là rất nhiều cột, hầu hết trong số đó là NULL trên bất kỳ hàng nhất định nào. 
- [Class Table Inheritance](https://martinfowler.com/eaaCatalog/classTableInheritance.html): Kế thừa bảng lớp - một bảng cho Sản phẩm, lưu trữ các thuộc tính chung cho tất cả các loại sản phẩm. Sau đó, một bảng cho mỗi loại sản phẩm, lưu trữ các thuộc tính cụ thể cho loại sản phẩm đó. 
- [Concrete Table Inheritance](https://martinfowler.com/eaaCatalog/concreteTableInheritance.html): Kế thừa Bảng Concrete - không có bảng cho các thuộc tính Sản phẩm chung. Thay vào đó, một bảng cho mỗi loại sản phẩm, lưu trữ cả thuộc tính sản phẩm chung và thuộc tính sản phẩm cụ thể. 
- [Serialized LOB](https://martinfowler.com/eaaCatalog/serializedLOB.html): LOB tuần tự - Một bảng cho Sản phẩm, lưu trữ các thuộc tính chung cho tất cả các loại sản phẩm. Một cột bổ sung lưu trữ BLOB dữ liệu bán cấu trúc, ở định dạng XML, YAML, JSON hoặc một số định dạng khác. BLOB này cho phép bạn lưu trữ các thuộc tính cụ thể cho từng loại sản phẩm. Bạn có thể sử dụng các Mẫu thiết kế ưa thích để mô tả điều này, chẳng hạn như Mặt tiền và Vật lưu niệm. Nhưng bất kể bạn có một loạt các thuộc tính không thể dễ dàng truy vấn trong SQL; bạn phải tìm nạp toàn bộ đốm màu trở lại ứng dụng và sắp xếp nó ở đó. 
- [Entity-Attribute-Value](https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model): Thực thể-Thuộc tính-Giá trị, Một bảng cho Sản phẩm và một bảng xoay các thuộc tính thành hàng, thay vì cột. EAV không phải là một thiết kế hợp lệ đối với mô hình quan hệ, nhưng nhiều người vẫn sử dụng nó. Đây là "Mô hình thuộc tính" được đề cập bởi một câu trả lời khác. Xem các câu hỏi khác với thẻ eav trên StackOverflow để biết một số cạm bẫy. 

Về cơ bản, không có giải pháp nào trong số này dễ dàng hoặc hiệu quả trong cơ sở dữ liệu quan hệ. Toàn bộ ý tưởng về việc có "các thuộc tính biến đổi" về cơ bản là mâu thuẫn với lý thuyết quan hệ.

Điều quan trọng là bạn phải chọn một trong những giải pháp dựa trên đó là giải pháp ít xấu nhất cho ứng dụng của bạn. Do đó, bạn cần biết mình sẽ truy vấn dữ liệu như thế nào trước khi chọn thiết kế cơ sở dữ liệu. Không có cách nào để chọn một giải pháp "tốt nhất" bởi vì bất kỳ giải pháp nào trong số các giải pháp đều có thể tốt nhất cho một ứng dụng nhất định. 


### Single Table Inheritance

> Biểu diễn một hệ thống phân cấp kế thừa của các lớp dưới dạng một bảng duy nhất có các cột cho tất cả các trường của các lớp khác nhau.

![Single Table Inheritance](https://boxxv.github.io/img/db/singleTableInheritance.png "Single Table Inheritance")

Cơ sở dữ liệu quan hệ không hỗ trợ kế thừa, vì vậy khi ánh xạ từ các đối tượng đến cơ sở dữ liệu, chúng ta phải xem xét cách thể hiện các cấu trúc kế thừa tốt đẹp của chúng ta trong các bảng quan hệ. Khi ánh xạ tới cơ sở dữ liệu quan hệ, chúng tôi cố gắng giảm thiểu các phép nối có thể nhanh chóng gắn kết khi xử lý cấu trúc kế thừa trong nhiều bảng. Kế thừa bảng đơn ánh xạ tất cả các trường của tất cả các lớp của cấu trúc kế thừa thành một bảng duy nhất.

Để có mô tả đầy đủ, hãy xem [Patterns of Enterprise Application Architecture](https://martinfowler.com/books/eaa.html) trang 278


### Class Table Inheritance

> Đại diện cho một hệ thống phân cấp kế thừa của các lớp với một bảng cho mỗi lớp.

![Class Table Inheritance](https://boxxv.github.io/img/db/classTableInheritance.png "Class Table Inheritance")

Một khía cạnh rất dễ thấy của sự không khớp đối tượng-quan hệ là thực tế là cơ sở dữ liệu quan hệ không hỗ trợ kế thừa. Bạn muốn cấu trúc cơ sở dữ liệu ánh xạ rõ ràng đến các đối tượng và cho phép liên kết ở bất kỳ đâu trong cấu trúc kế thừa. Kế thừa bảng lớp hỗ trợ điều này bằng cách sử dụng một bảng cơ sở dữ liệu cho mỗi lớp trong cấu trúc kế thừa. 

Để có mô tả đầy đủ, hãy xem [Patterns of Enterprise Application Architecture](https://martinfowler.com/books/eaa.html) trang 285


### Concrete Table Inheritance

> Đại diện cho một hệ thống phân cấp kế thừa của các lớp với một bảng cho mỗi lớp cụ thể trong hệ thống phân cấp.

![Concrete Table Inheritance](https://boxxv.github.io/img/db/concreteTableInheritance.png "Concrete Table Inheritance")

Như bất kỳ người theo chủ nghĩa đối tượng nào sẽ nói với bạn, cơ sở dữ liệu quan hệ không hỗ trợ kế thừa - một thực tế làm phức tạp việc ánh xạ quan hệ đối tượng. Suy nghĩ về các bảng từ một quan điểm đối tượng, một lộ trình hợp lý là lấy từng đối tượng trong bộ nhớ và ánh xạ nó vào một hàng cơ sở dữ liệu duy nhất. Điều này ngụ ý Concrete Table Inher-itance, nơi có một bảng cho mỗi lớp cụ thể trong hệ thống phân cấp kế thừa.

Tôi thú nhận là đã gặp một số khó khăn khi đặt tên cho mẫu này. Hầu hết mọi người nghĩ về nó như là định hướng lá vì bạn thường có một bảng cho mỗi lớp lá trong một hệ thống phân cấp. Theo logic đó, tôi có thể gọi đây là kế thừa bảng mẫu lá và thuật ngữ "lá" thường được sử dụng cho mẫu này. Tuy nhiên, một cách nghiêm túc, một lớp cụ thể không phải là một chiếc lá cũng thường có một bảng, vì vậy tôi quyết định sử dụng thuật ngữ đúng hơn, nếu ít trực quan hơn.

Để có mô tả đầy đủ, hãy xem [Patterns of Enterprise Application Architecture](https://martinfowler.com/books/eaa.html) trang 293




-----
[Database Schema for Multiple Types of Products](https://www.codingblocks.net/programming/database-schema-for-multiple-types-of-products/)  
[How to design a product table for many kinds of product where each product has many parameters](https://stackoverflow.com/questions/695752/how-to-design-a-product-table-for-many-kinds-of-product-where-each-product-has-m)  

