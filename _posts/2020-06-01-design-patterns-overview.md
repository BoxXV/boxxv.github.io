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

![Design Patterns](https://boxxv.github.io/img/patterns/48e2578f-6105-4bf6-8aca-166f3263f169.webp "Design Patterns")

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

class Circle implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình tròn.");
   }
}
```

`shapefactory/Triangle.java`
```java
package shapefactory;

class Triangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình tam giác.");
   }
}
```

`shapefactory/Square.java`
```java
package shapefactory;

class Square implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình vuông.");
   }
}
```

#### Bước 3
Tạo `01 class Factory` để sản xuất các `object` thực thể với thông tin được cung cấp từ code client.

`shapefactory/Factory.java`
```java
package shapefactory;

public class Factory {
   public Shape createShape(String type) {
      if (type == null)                        return null;
      if (type.equalsIgnoreCase("circle"))     return new Circle();
      if (type.equalsIgnoreCase("triangle"))   return new Triangle();
      if (type.equalsIgnoreCase("square"))     return new Square();
      else                                     return null;
   }
}
```

#### Bước 4
Sử dụng `Factory` trong code client ở `main` để yêu cầu khởi tạo các `object` bằng cách truyền vào thông tin về loại hình của `Shape`.

`PatternDemo.java`
```java
import shapefactory.Factory;
import shapefactory.Shape;

public class FactoryPatternDemo {
   public static void main(String[] args) {
      Factory shapeFactory = new Factory();

      // Yêu cầu khởi tạo một `object` hình tròn và gọi `draw()` để vẽ
      Shape circle = shapeFactory.createShape("circle");
      circle.draw();

      // Yêu cầu khởi tạo một `object` hình tam giác và gọi `draw()` để vẽ
      Shape triangle = shapeFactory.createShape("triangle");
      triangle.draw();

      // Yêu cầu khởi tạo một `object` hình vuông và gọi `draw()` để vẽ
      Shape square = shapeFactory.createShape("square");
      square.draw();
   }
}
```

#### Bước 5
Kiểm chứng lại kết quả được in ra ở console.

``` bat
Một hình tròn.
Một hình tam giác.
Một hình vuông.
```


## Abstract Factory

Abstract Factory là dạng thức được đưa ra để làm việc xoay quanh trọng tâm tạo ra một "siêu" Factory đóng vai trò tạo ra các Factory khác. Abstract Factory cũng được xếp vào nhóm các dạng thức Khởi Tạo.

Trong phép triển khai Abstract Factory, `01 interface` được sử dụng để đảm nhiệm vai trò tạo ra `01 Factory` của các `object` liên quan mà không cần chỉ ra đặc định `class` của các `object` đó. Mỗi `Factory` được khởi tạo sẽ có thể giúp chúng ta khởi tạo các object thực thể như đã biết trong bài `Factory Pattern`.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/ea520e8b-fa3c-4f16-b42e-f3695c8c006d.webp "Design Patterns")

- Chúng ta sẽ tạo ra `01 interface Shape` mở `public`.
- Và `04 class` triển khai `interface` này.
- Ở bước tiếp theo, `01 class AbstractFactory` sẽ được tạo ra.
- Kế đến là `02 class Factory` mở rộng `AbstractFactory`.
- Sau đó là một phương thức `static` để khởi tạo các `object Factory`.
- Cuối cùng, trong `main` ở `PatternDemo`, chúng ta sử dụng phương thức `static` để tạo ra các `Factory`. Rồi sau đó truyền vào thông tin về kiểu `object` hình học muốn tạo ra (triangle / square).

![Design Patterns](https://boxxv.github.io/img/patterns/81af7874-c398-4b86-b636-f05e1af900ed.webp "Design Patterns")

Về mặt quản lý code, chúng ta sẽ có `01 package` được đặt tên là `shapefactory`. `Package` này sẽ chứa các thành phần `public` tới code client bao gồm `interface Shape` và `class AbstractFactory`. Tất cả các thành phần còn lại bao gồm `04 class` triển khai `Shape` và `02 class` mở rộng `AbstractFactory` sẽ đều sử dụng `access modifier` là `default`.

Do đó, toàn bộ tiến trình logic để khởi tạo các `Factory` cũng như các `Shape` đều không để mở về phía code client và các tham chiếu đều được thực hiện thông qua `abstract class` và `interface`.

#### Bước 1

Tạo `01 interface Shape` mở `public`.

`shapefactory/Shape.java`
```java
package shapefactory;

public interface Shape {
   void draw();
}
```

#### Bước 2
Tạo các `class` triển khai giao diện `Shape`.

`shapefactory/NormalTriangle.java`
```java
package shapefactory;

class NormalTriangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình tam giác bình thường.");
   }
}
```

`shapefactory/NormalSquare.java`
```java
package shapefactory;

class NormalSquare implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình vuông bình thường.");
   }
}
```

`shapefactory/RoundedTriangle.java`
```java
package shapefactory;

class RoundedTriangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình tam giác có các góc bo tròn.");
   }
}

```

`shapefactory/RoundedSquare.java`
```java
package shapefactory;

class RoundedSquare implements Shape {
   @Override
   public void draw() {
      System.out.println("Một hình vuông có các góc bo tròn.");
   }
}
```

#### Bước 3
Tạo `01 class abstract` để khái quát hóa các `Factory`.

`shapefactory/AbstractFactory.java`
```java
package shapefactory;

public abstract class AbstractFactory {
   public abstract Shape createShape(String type);
}
```

#### Bước 4

Tạo các `class` mở rộng `AbstractFactory` giúp khởi tạo các `Shape` với thông tin được cung cấp.

`shapefactory/NormalFactory.java`
```java
package shapefactory;

class NormalFactory extends AbstractFactory {
   @Override
   public Shape createShape(String type) {
      if (type == null)                        return null;
      if (type.equalsIgnoreCase("triangle"))   return new NormalTriangle();
      if (type.equalsIgnoreCase("square"))     return new NormalSquare();
      else                                     return null;
   }
}
```

`shapefactory/RoundedFactory.java`
```java
package shapefactory;

class RoundedFactory extends AbstractFactory {
   @Override
   public Shape createShape(String type) {
      if (type == null)                        return null;
      if (type.equalsIgnoreCase("triangle"))   return new RoundedTriangle();
      if (type.equalsIgnoreCase("square"))     return new RoundedSquare();
      else                                     return null;
   }
}
```

#### Bước 5

Thêm phương thức `static` cho `AbstractFactory` để khởi tạo các `object Factory` cụ thể.

`shapefactory/AbstractFactory`
```java
package shapefactory;

public abstract class AbstractFactory {
   public static AbstractFactory createFactory(boolean rounded) {
      if (rounded)      return new RoundedFactory();
      else              return new NormalFactory();
   }

   abstract public Shape createShape(String type);
}
```

#### Bước 6

Sử dụng phương thức `static` vừa rồi để khởi tạo các `objectFactory`. Sau đó, sử dụng các `Factory` để khởi tạo các `object` hình học bằng cách truyền vào thông tin về kiểu `Shape`.

`PatternDemo.java`
```java
import shapefactory.AbstractFactory;
import shapefactory.Shape;

public class DesignPatterns {
   public static void main(String[] args) {
      // Tạo ra một Factory cho các hình 2D bình thường
      AbstractFactory normalFactory = AbstractFactory.createFactory(false);

      // Yêu cầu khởi tạo 1 hình tam giác bình thường và gọi `draw()`
      Shape normalTriangle = normalFactory.createShape("triangle");
      normalTriangle.draw();

      // Yêu cầu khởi tạo 1 hình vuông bình thường và gọi `draw()`
      Shape normalSquare = normalFactory.createShape("square");
      normalSquare.draw();

      // Tạo ra một Factory cho các hình 2D bo tròn góc
      AbstractFactory roundedFactory = AbstractFactory.createFactory(true);

      // Yêu cầu khởi tạo 1 hình tam giác bo góc và gọi `draw()`
      Shape roundedTriangle = roundedFactory.createShape("triangle");
      roundedTriangle.draw();

      // Yêu cầu khởi tạo 1 hình vuông bình thường và gọi `draw()`
      Shape roundedSquare = roundedFactory.createShape("square");
      roundedSquare.draw();
   }
}
```

#### Bước 7

Kiểm chứng lại kết quả được in ra ở `console`.
```bat
Một hình tam giác bình thường.
Một hình vuông bình thường.
Một hình tam giác với các góc bo tròn.
Một hình vuông với các góc bo tròn.
```


## Singleton Pattern

Singleton là một trong số những dạng thức triển khai đơn giản nhất của OOP và được xếp vào nhóm các dạng thức Khởi Tạo. Singleton giúp chúng ta đảm bảo chỉ có `01 object` đơn duy nhất của `01 class` đặc định được tạo ra trong suốt thời gian phần mềm hoạt động. `Class` này có cung cấp một phương thức để truy xuất `object` đơn nguyên này và không cho phép khởi tạo `object` mới tương tự ở bất kỳ nơi nào khác.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/734fb702-73c2-414a-a883-5cc2ce329fda.png "Design Patterns")

- Chúng ta sẽ tạo ra `01 class` có tên là `Thing`. Bên trong `class` này sẽ có hàm khởi tạo được khóa `private` và một thuộc tính `static` để lưu tham chiếu của `object` duy nhất được tạo ra.
- `Thing` có cung cấp một phương thức `static` để chia sẻ tham chiếu tới `object` duy nhất cho phần code client sử dụng.
- Cuối cùng là `main` ở `PatternDemo` sẽ sử dụng `Thing` để hỏi truy xuất tới `object` duy nhất và hiển thị tin nhắn của `object` đó.

#### Bước 1

Tạo `01 class singleton` có tên là `Thing`.

`singleton/Thing.java`
```java
package singleton;

public class Thing {
   private static final Thing instance = new Thing();

   private Thing() {
      // khóa `private` phương thức khởi tạo với `new` từ bên ngoài `class`
   }

   public static Thing getInstance() {
      return instance;
   }

   public void showMessage() {
      System.out.println("Tin nhắn từ `object` duy nhất của `Thing`!");
   }
}
```


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
