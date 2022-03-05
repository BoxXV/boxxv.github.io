---
layout: post
title: Tổng quan về Design Pattern
subtitle: 33 Dạng Thức Triển Khai Design Patterns trong OOP
tags:
- Design Pattern
- Creational
- Structural
- Behavioral
---

Design Patterns là các dạng thức triển khai code được các lập trình viên OOP giàu kinh nghiệm đúc kết, giúp nhanh chóng xử lý nhiều vấn đề phổ biến mà chúng ta thường gặp trong quá trình viết code. Các giải pháp này được ghi nhận qua thời gian dài và được chiêm nghiệm bởi rất nhiều nhà phát triển phần mềm.

![Design Patterns](https://boxxv.github.io/img/patterns/Design-Patterns-Certification-Training-Online.webp "Design Patterns")

## Giới thiệu Bộ Tứ GoF (Gang of Four)

Năm 1994, có bốn tác giả lớn là Erich Gamma, Richard Helm, Ralph Johnson, và John Vlissides đã đồng xuất bản một cuốn sách có tên là Design Patterns - Elements of Reusable Object-Oriented Software (Dịch nôm na là: Các dạng thức triển khai - Những yếu tố đặc trưng của code OOP có thể tái sử dụng). Cuốn sách này đã đặt nền móng mở đầu cho thuật ngữ Design Patterns trong việc phát triển phần mềm.

Các tác giả này được biết đến với tên gọi là Bộ Tứ hay GoF (Gang of Four). Theo họ cho biết, Design Patterns chủ yếu được xây dựng dựa theo các tiêu chí sau của thiết kế hướng đối tượng:
- Lập trình hướng đến 1 interface (giao diện) chứ không phải là triển khai mở rộng interface đó.
- Ưu tiên việc tổ hợp Object hơn so với việc sử dụng hình thức kế thừa.

## Ứng dụng của Design Patterns

Design Patterns có 2 ứng dụng chính trong việc phát triển phần mềm.

#### 1. Tạo ra một nền tảng chung cho các nhà phát triển
Các Patterns cung cấp một giải pháp chung mang tính chất tiêu chuẩn mặt bằng và đặc trưng cho nhiều trường hợp. Ví dụ, Singleton được các nhà phát triển biết đến và sử dụng làm giải pháp chung để tạo ra một Object đơn nguyên duy nhất của một Class. Và họ cũng sẽ nói ra cái tên này khi được hỏi về giải pháp thực hiện một công việc như vậy.

#### 2. Có thể được xem là các giải pháp tốt nhất
Các Patterns cũng được phát triển qua thời gian dài và mang đến những giải pháp tốt nhất cho nhiều vấn đề thường gặp khi phát triển phần mềm. Việc học các dạng thức triển khai này sẽ giúp cho các nhà phát triển phần mềm chưa có kinh nghiệm có thể học được cách thiết kế phần mềm dễ dàng hơn.

#### Có tất cả bao nhiêu dạng thức đã được công nhận
Nguyên gốc theo cuốn Design Patterns - Elements of Reusable Object-Oriented Software thì có tất cả 23 dạng thức triển khai và có thể được chia ra làm 3 nhóm là Khởi Tạo, Kiến Trúc, và Hành Vi - dựa trên công dụng của các dạng thức. Tuy nhiên thì ở thời điểm hiện tại con số này đã có một chút sự tăng tiến và chúng ta còn có thêm một nhóm Patterns mới là J2EE Patterns. Chúng ta sẽ cùng nhau tìm hiểu chi tiết hơn trong các bài viết tiếp theo.

- Các Patterns Khởi Tạo `Creational Patterns`
    + Các Patterns này cung cấp giải pháp khởi tạo các Object trong khi ẩn đi logic của tiến trình khởi tạo, thay vì khởi tạo Object trực tiếp bằng toán tử new. Cách khởi tạo này giúp đem lại sự linh động tốt hơn trong việc quyết định những Object này cần được tạo ra trong trường hợp cụ thể.
- Các Patterns Kiến Trúc `Structural Patterns`
    + Các Patterns này quan tâm tới vấn đề tổ hợp các Class và Object. Trong đó, tính kế thừa được áp dụng để tổ hợp các giao diện và định nghĩa cách thức tổ hợp các Object để có thêm tính năng mới.
- Các Patterns Hành Vi `Behavioral Patterns`
    + Các Patterns này quan tâm chủ yếu tới yếu tố giao tiếp giữa các Object.
- Các Patterns J2EE
    + Các Patterns này đặc biệt quan tâm tới tầng biểu thị và được đặt nhận diện bởi Sun Java Center.

Nhân tiện dịch tới đây thì mình mới nhớ ra một vấn đề quan trọng, đó là các ví dụ triển khai được sử dụng trong các bài viết tiếp theo sẽ là triển khai trên Java. Lý do mà Tutorialspoint họ chọn Java để làm Tút có lẽ cũng dễ hiểu bởi vì sự phổ biến của ngôn ngữ này và quan trọng hơn cả đó là cú pháp rườm rà, cứng nhắc, khó có thể có sự nhầm lẫn gì giữa người viết và người đọc code.

Vì vậy nên nếu như bạn chưa từng nói chuyện với máy tính bằng Java bao giờ thì rất có thể bạn sẽ cần một khóa cơ bản cấp tốc trước khi đọc bài viết tiếp theo đấy nhé. 


## Factory Pattern

Factory là một trong những dạng thức triển khai được sử dụng nhiều nhất và được xếp vào nhóm các dạng thức Khởi Tạo.

Trong phép triển khai Factory, chúng ta tạo ra các `object` mà không để mở logic khởi tạo cho phía client (đoạn code gửi yêu cầu và sử dụng `object` được khởi tạo). Thêm vào đó, việc tham chiếu tới object được khởi tạo sẽ được thực hiện thông qua một `interface` (giao diện) chung thay vì sử dụng `class` cụ thể.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/48e2578f-6105-4bf6-8aca-166f3263f169.png "Design Patterns")

- Chúng ta sẽ tạo ra `01 interface` chung có tên là `Shape` cho các `class` mô tả hình 2D (hình tròn, tam giác, hình vuông) và các `class` cụ thể triển khai `interface` này.
- Ở bước tiếp theo, `01 class` có tên là `Factory` sẽ được định nghĩa.
- Cuối cùng là `main` của chương trình sẽ sử dụng `Factory` để yêu cầu khởi tạo `1 Shape` (hình 2D). `main` sẽ truyền vào thông tin về kiểu `Shape` muốn khởi tạo (`circle` / `triangle` / `square` - hình tròn / tam giác / hình vuông).

Về mặt quản lý code, chúng ta sẽ có `01 package` được đặt tên là `shapefactory`.
`Package` này sẽ chứa:
- `01 class Factory` mở `public`
- `01 interface Shape` mở `public`
- `03 class` triển khai `Shape` để `default`

Điều này có nghĩa là code client ở phía bên ngoài `package` sẽ hoàn toàn không biết tới `03 class` triển khai `Shape` mà chỉ có thể gọi `Factory` để khởi tạo các `Shape` và tham chiếu tới các `object` được tạo ra thông qua `interface`.

#### Bước 1
Tạo `01 interface` có tên là `Shape` mở `public`.

`shapefactory/Shape.java`

```java
package shapefactory;

public interface Shape {
   void draw();
}
```

#### Bước 2
Tạo các `class` cụ thể triển khai `interface` với `access modifier` đặt `default`, không mở `public`.

`shapefactory/Circle.java`

```java
package shapefactory;

class Circle
implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình tròn.");
   }
}
```

`shapefactory/Triangle.java`

```java
package shapefactory;

class Triangle
implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình tam giác.");
   }
}
```

`shapefactory/Square.java`
```java
package shapefactory;

class Square
implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình vuông.");
   }
}
```

#### Bước 3

#### Bước 4

#### Bước 5


-----
Tham khảo:
- [Design Patterns in Java Tutorial](https://www.tutorialspoint.com/design_pattern/index.htm)
- [Hướng Dẫn Cơ Bản Design Patterns - 33 Dạng Thức Triển Khai Trong OOP](https://viblo.asia/p/design-patterns-gioi-thieu-tong-quan-YWOZrAWrKQ0)
- [Giới thiệu Design Patterns](https://gpcoder.com/4164-gioi-thieu-design-patterns/)
- [Nhập môn Design Pattern (Phong cách kiếm hiệp)](https://toidicodedao.com/2016/03/01/nhap-mon-design-pattern-phong-cach-kiem-hiep/)
- [https://tuanitpro.com/design-pattern-la-gi/](https://tuanitpro.com/design-pattern-la-gi/)
- [https://blog.duyet.net/2015/02/oop-design-patterns-la-gi.html](https://blog.duyet.net/2015/02/oop-design-patterns-la-gi.html)
- [https://refactoring.guru/design-patterns/catalog](https://refactoring.guru/design-patterns/catalog)
- [https://www.ibm.com/developerworks/java/tutorials/j-patterns/j-patterns.html](https://www.ibm.com/developerworks/java/tutorials/j-patterns/j-patterns.html)
- [https://www.journaldev.com/1827/java-design-patterns-example-tutorial](https://www.journaldev.com/1827/java-design-patterns-example-tutorial)
- [https://viblo.asia/tags/design-pattern](https://viblo.asia/tags/design-pattern)
- [Lập trình cho interface chứ không phải để implement interface đó.](https://stackoverflow.com/questions/2697783/what-does-program-to-interfaces-not-implementations-mean)
- [Ưu tiên object composition (chứa trong) hơn là inheritance (thừa kế).](https://stackoverflow.com/questions/49002/prefer-composition-over-inheritance)
