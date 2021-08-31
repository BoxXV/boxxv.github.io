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

- [Kế thừa một bảng](martinfowler.com/eaaCatalog/singleTableInheritance.html): một bảng cho tất cả các loại Sản phẩm, có đủ cột để lưu trữ tất cả các thuộc tính của tất cả các loại. Điều này có nghĩa là rất nhiều cột, hầu hết trong số đó là NULL trên bất kỳ hàng nhất định nào. 






-----
[Database Schema for Multiple Types of Products](https://www.codingblocks.net/programming/database-schema-for-multiple-types-of-products/)  
[How to design a product table for many kinds of product where each product has many parameters](https://stackoverflow.com/questions/695752/how-to-design-a-product-table-for-many-kinds-of-product-where-each-product-has-m)  

