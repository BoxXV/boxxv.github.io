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

- [Factory Pattern](#factory-pattern)
- [Abstract Factory](#abstract-factory)
- [Singleton Pattern](#singleton-pattern)
- [Builder Pattern](#builder-pattern)
- [Prototype Pattern](#prototype-pattern)
- [Adapter Pattern](#adapter-pattern)
- [Bridge Pattern](#bridge-pattern)
- [Filter Pattern](#filter-pattern)
- [Composite Pattern](#composite-pattern)

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

#### Bước 2

Truy xuất tới `object` duy nhất và hiển thị tin nhắn.

`PatternDemo.java`
```java
import singleton.Thing;

public class PatternDemo {
   public static void main(String[] args) {
      // Lỗi biên dịch vì phương thức khởi tạo không khả dụng
      // Thing only = new Thing();

      // Truy xuất object đơn nguyên duy nhất
      Thing only = Thing.getInstance();

      // Hiển thị tin nhắn
      only.showMessage();
   }
}
```

#### Bước 3

Kiểm chứng lại kết quả được in ra ở `console`.

```bat
Tin nhắn từ `object` duy nhất của `Thing`!
```


## Builder Pattern

Builder Pattern giúp chúng ta xây dựng một `object` phức tạp từ những `object` đơn giản qua từng bước. Builder Pattern được xếp vào nhóm các pattern Khởi .

Một `class Builder` luôn luôn xây dựng `object` thực thể cuối cùng qua từng bước. Bản thân `Builder` luôn luôn độc lập và không lệ thuộc vào các `object` khác.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/40fe26e2-b78b-4fc2-a0c2-e3608577be64.webp "Design Patterns")

- Chúng ta sẽ tạo 01 abstract class Item để biểu thị hàng hóa và các class để mô tả các thực thể.
- Giao diện Packing thể hiện cách đóng gói của sản phẩm.
- Sau đó, chúng ta tạo ra 01 class Meal có chứa một mảng Item.
- Và tạo 01 class Builder để thực hiện công việc tổ hợp nên các object Meal khác nhau bằng việc kết hợp các Item.
- Cuối cùng là code main sử dụng Builder để xây dựng một Meal.

Về mặt quản lý code, chúng ta sẽ có `01 package` có tên là `mealbuilder`. Phần code client trên `main` sẽ chỉ cần tham chiếu tới `Builder` và `Meal` do đó sẽ chỉ có `02 class` này được mở `public`. Tất cả các thành phần còn lại của `package` sẽ đều được đặt `access modifier` là `default`.

#### Bước 1

Tạo `abstract class Item` và `interface Packing`.

`mealbuilder/Item.java`
```java
package mealbuilder;

abstract class Item {
   private final String  name;
   private final float   price;
   private final Packing packing;

   Item(
      String  name,
      float   price,
      Packing packing
   ) {
      this.name    = name;
      this.price   = price;
      this.packing = packing;
   }

   public String getName() {
      return name;
   }

   public float getPrice() {
      return price;
   }

   public Packing getPacking() {
      return packing;
   }
}
```

`mealbuilder/Packing.java`
```java
package mealbuilder;

interface Packing {
   public String pack();
}
```

#### Bước 2

Tạo các `class` triển khai của `Packing`.

`mealbuilder/Wrapper.java`
```java
package mealbuilder;

class Wrapper
implements Packing {
   @Override
   public String pack() {
      return "Wrapper";
   }
}
```

`mealbuilder/Bottle.java`
```java
package mealbuilder;

class Bottle
implements Packing {
   @Override
   public String pack() {
      return "Bottle";
   }
}
```

#### Bước 3

Tạo các `class Burger` mở rộng `Item`.

`mealbuilder/Burger.java`
```java
package mealbuilder;

public abstract class Burger extends Item {
   Burger(
      String  name,
      float   price,
      Packing packing
   ) {
      super(name, price, packing);
   }
}
```

`mealBuilder/BurgerForVeg.java`
```java
package mealbuilder;

class BurgerForVeg extends Burger {
   BurgerForVeg() {
      super("Bugger for Veg", 25.0f, new Wrapper());
   }
}
```

`mealBuilder/BurgerNonVeg.java`
```java
package mealbuilder;

class BurgerNonVeg extends Burger {
   BurgerNonVeg() {
      super("Burger non-Veg", 50.5f, new Wrapper());
   }
}
```

#### Bước 4

Tạo các `class Drink` mở rộng `Item` tương tự như `Burger`.

`mealbuilder/Drink.java`
```java
package mealbuilder;

public abstract class Drink extends Item {
   Drink(
      String  name,
      float   price,
      Packing packing
   ) {
      super(name, price, packing);
   }
}
```

`mealbuilder/DrinkCoke.java`
```java
package mealbuilder;

class DrinkCoke extends Drink {
   DrinkCoke() {
      super("Coke", 30.0f, new Bottle());
   }
}
```

`mealbuilder/DrinkPepsi.java`
```java
package mealbuilder;

class DrinkPepsiextends Drink {
   DrinkPepsi() {
      super("Pepsi", 35.0f, new Bottle());
   }
}
```

#### Bước 5

Tạo `class Meal` chứa các `object Item`.

`mealbuilder/Meal.java`
```java
package mealbuilder;

import java.util.ArrayList;
import java.util.List;

public class Meal {
   private List<Item> itemList = new ArrayList<Item>();

   public void addItem(Item newItem) {
      itemList.add(newItem);
   }

   public float getCost() {
      float totalCost = 0.0f;
      for (Item i : itemList) { totalCost += i.getPrice(); }
      return totalCost;
   }

   public void showItems() {
      for (Item i : itemList) {
         System.out.println(i.getName());
         System.out.println("   + Packing: " + i.getPacking().pack());
         System.out.println("   + Price: " + i.getPrice());
      }
   }
}
```

#### Bước 6

Tạo `class Builder` giúp xây dựng các `object Meal`.

`mealbuilder/Builder.java`
```java
package mealbuilder;

public class Builder {
   public Meal prepareMealForVeg() {
      Meal mealForVeg = new Meal();
      mealForVeg.addItem(new BurgerForVeg());
      mealForVeg.addItem(new DrinkCoke());
      return mealForVeg;
   }

   public Meal prepareMealNonVeg() {
      Meal mealNonVeg = new Meal();
      mealNonVeg.addItem(new BurgerNonVeg());
      mealNonVeg.addItem(new DrinkPepsi());
      return mealNonVeg;
   }
}
```

#### Bước 7

Code `main` tại `PatternDemo` để chạy thử pattern.

`PatternDemo.java`
```java
import mealbuilder.Builder;
import mealbuilder.Meal;

public class PatternDemo {
   public static void main(String[] args) {
      Builder mealBuilder = new Builder();

      Meal mealForVeg = mealBuilder.prepareMealForVeg();
      System.out.println("=== Meal for Veg ========");
      mealForVeg.showItems();
      System.out.println("Total cost: " + mealForVeg.getCost());

      Meal mealNonVeg = mealBuilder.prepareMealNonVeg();
      System.out.println("=== Meal non-Veg ========");
      mealNonVeg.showItems();
      System.out.println("Total cost: " + mealNonVeg.getCost());
   }
}
```

#### Bước 8

Kiểm chứng lại thông tin được in ra ở `console`.

```bat
=== Meal for Veg ========
Bugger for Veg
   + Packing: Wrapper
   + Price: 25.0
Coke
   + Packing: Bottle
   + Price: 30.0
Total cost: 55.0
=== Meal non-Veg ========
Burger non-Veg
   + Packing: Wrapper
   + Price: 50.5
Pepsi
   + Packing: Bottle
   + Price: 35.0
Total cost: 85.5
```


## Prototype Pattern

Prototype Pattern thường được sử dụng để nhân bản một `object` với lưu ý về mặt hiệu năng xử lý. Protype Pattern được xếp vào nhóm các pattern Khởi Tạo.

Prototype Pattern sử dụng một giao diện kiểu mẫu để tạo ra một bản sao `clone` của một `object`. Pattern này được sử dụng khi mà việc khởi tạo một `object` trực tiếp gặp nhiều khó khăn và tiêu tốn tài nguyên về thời gian.

Ví dụ, một `object` được tạo ra sau một lần mở kết nối tới CSDL có thể được cho là đắt đỏ. Chúng ta có thể ghi đệm lại `object` này vào một `cache`, và lần tới khi yêu cầu được gửi đến, chúng ta có thể tạo ra một bản sao `clone` và trả về, đồng thời cập nhật CSDL, thay vì truy xuất lại thông tin từ CSDL và khởi tạo lại `object` từ đầu.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/4f821d66-f712-4e6b-925a-d520427c2ebf.png "Design Patterns")

- Chúng ta sẽ tạo `01 abstract class Shape`.
- Và các `class` mô tả thực thể mở rộng `Shape`.
- Ở bước tiếp theo, `01 class Cache` ghi đệm các `object` đã được tạo ra sẽ được định nghĩa.
- Cuối cùng là code `main` ở `PatternDemo` sẽ sử dụng `Cache` để yêu cầu lấy các `object Shape`.

Về mặt quản lý code, chúng ta sẽ có `01 package` tên là `shapeprototype`. Code sử dụng ở phía client sẽ chỉ có thể tham chiếu tới `Cache` và `Shape` được mở `public`. Các thành phần còn lại của `shapeprototype` đều được đặt `access modifier` là `default`.

#### Bước 1

Tạo `01 abstract class Shape` triển khai `interface Cloneable`.

`shapeprototype/Shape.java`
```java
package shapeprototype;

public abstract class Shape
implements Cloneable {
   private String id;
   protected String type;

   public abstract void draw();

   public String getType() {
      return type;
   }

   public void setId(String id) {
      this.id = id;
   }

   public String getId() {
      return id;
   }

   @Override
   public Object clone() {
      Object clone = null;

      try {
         clone = super.clone();
      }
      catch (CloneNotSupportedException e) {
         e.printStackTrace();
      }

      return clone;
   }
}
```

#### Bước 2

Tạo các `class` mô tả thực thể mở rộng `Shape`.

`shapeprototype/Circle.java`
```java
package shapeprototype;

class Circle extends Shape {
   public Circle() {
      type = "circle";
   }

   @Override
   public void draw() {
      System.out.println("Một hình tròn.");
   }
}
```

`shapeprototype/Triangle.java`
```java
package shapeprototype;

class Triangle extends Shape {
   public Triangle() {
      type = "triangle";
   }

   @Override
   public void draw() {
      System.out.println("Một hình tam giác.");
   }
}
```

`shapeprototype/Square.java`
```java
package shapeprototype;

class Square
extends Shape {
   public Square() {
      type = "square";
   }

   @Override
   public void draw() {
      System.out.println("Một hình vuông.");
   }
}
```

#### Bước 3

Tạo `01 class Cache` để truy vấn các `object Shape` từ CSDL và ghi đệm vào một.

`shapeprototype/Cache.java`
```java
package shapeprototype;

import java.util.Hashtable;

public class Cache {
   private static Hashtable<String, Shape> cachedShapes = new Hashtable<String, Shape>();

   public static Shape getShape(String id) {
      return (Shape) cachedShapes.get(id).clone();
   }

   public static void load() {
      Circle circle = new Circle();
      circle.setId("1");
      cachedShapes.put(circle.getId(), circle);

      Triangle triangle = new Triangle();
      triangle.setId("2");
      cachedShapes.put(triangle.getId(), triangle);

      Square square = new Square();
      square.setId("3");
      cachedShapes.put(square.getId(), square);
   }
}
```

#### Bước 4

Tại `PatternDemo`, sử dụng `Cache` để tạo ra các bản sao của các `object Shape` được ghi đệm trước đó trong `Hashtable`.

`PatternDemo.java`
```java
import shapeprototype.Cache;
import shapeprototype.Shape;

public class PatternDemo {
   public static void main(String[] args) {
      Cache.load();

      Shape clonedCircle = (Shape) Cache.getShape("1");
      System.out.println("=== Cloned " + clonedCircle.getType());
      clonedCircle.draw();

      Shape clonedTriangle = (Shape) Cache.getShape("2");
      System.out.println("=== Cloned " + clonedTriangle.getType());
      clonedTriangle.draw();

      Shape clonedSquare = (Shape) Cache.getShape("3");
      System.out.println("=== Cloned " + clonedSquare.getType());
      clonedSquare.draw();
   }
}
```

#### Bước 5

Kiểm chứng lại thông tin được in ra ở `console`.

```bat
=== Cloned circle
Một hình tròn.
=== Cloned triangle
Một hình tam giác.
=== Cloned square
Một hình vuông.
```


## Adapter Pattern

Adapter Pattern hoạt động như một cầu nối giữa 2 giao diện không tương thích. Adapter Pattern được xếp vào nhóm các pattern Kiến Trúc.

Adapter Pattern sử dụng `01 class` đơn để đảm nhiệm việc kết nối các giao diện độc lập hoặc không tương thích.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/75591960-59be-404b-a24b-5c92aa4ef0c8.png "Design Patterns")

- Chúng ta có 01 `interface MediaPlaying` và `01 class` mô tả thực thể `MediaPlayer` triển khai giao diện đó. Mặc định thì `MediaPlayer` có thể phát các tệp định dạng Mp3.
- Ngoài ra chúng ta còn có `01 interface AdvancedPlaying` và các `class` triển khai giao diện bổ sung này. Các `class` này có thể phát các tệp Vlc hoặc Mp4.
- Bây giờ thì chúng ta muốn `MediaPlayer` có thể phát được các tệp định dạng khác nữa ngoài Mp3 mặc định.
- Để làm được điều này, chúng ta cần tạo `01 class MediaAdapter` triển khai `interface MediaPlaying` và sử dụng các `object AdvancedPlaying` để phát tệp được yêu cầu.
- `MediaPlayer` sẽ sử dụng `MediaApdater` bằng cách truyền vào đó định dạng media muốn phát mà không cần biết tới các class thực thụ được sử dụng để phát tệp.
- Cuối cùng là PatternDemo với code main sẽ sử dụng MediaPlayer để phát các định dạng media khác nhau.

Về mặt quản lý code, chúng ta có `01 package adapterpattern`. Code client trong `main` sẽ chỉ tham chiếu duy nhất tới `MediaPlayer` và trỏ `interface MediaPlaying`. Do đó chúng ta sẽ chỉ có duy nhất `class MediaPlayer` và `interface MediaPlaying` để mở `public`. Tất cả các thành phần còn lại của `package` đều sẽ được đặt `access modifier` là `default`.

#### Bước 1

Tạo các `interface` để phát tệp bao gồm `MediaPlaying` và `AdvancedPlaying`.

`adapterpattern/MediaPlaying.java`
```java
package adapterpattern;

public interface MediaPlaying {
   public MediaPlaying play(String mediaType, String fileName);
}
```

`adapterpattern/AdvancedPlaying.java`
```java
package adapterpattern;

interface AdvancedPlaying {
   public AdvancedPlaying playVlc(String fileName);
   public AdvancedPlaying playMp4(String fileName);
}
```

#### Bước 2

Tạo các class triển khai `interface AdvancedPlaying`.

`adapterpattern/VlcPlayer.java`
```java
package adapterpattern;

class VlcPlayer implements AdvancedPlaying {
   @Override
   public AdvancedPlaying playVlc(String fileName) {
      System.out.println("Đang phát tệp Vlc. Tên tệp: " + fileName);
      return this;
   }

   @Override
   public AdvancedPlaying playMp4(String fileName) {
      // do nothing
      return this;
   }
}
```

`adapterpattern/Mp4Player.java`
```java
package adapterpattern;

public class Mp4Player implements AdvancedPlaying {
   @Override
   public AdvancedPlaying playVlc(String fileName) {
      // do nothing
      return this;
   }

   @Override
   public AdvancedPlaying playMp4(String fileName) {
      System.out.println("Đang phát tệp Mp4. Tên tệp: " + fileName);
      return this;
   }
}
```

#### Bước 3

Tạo `class MediaAdapter` triển khai `MediaPlaying`.

`adapterpattern/MediaAdapter.java`
```java
package adapterpattern;

public class MediaAdapter implements MediaPlaying {
   AdvancedPlaying advancedPlayer;

   public MediaAdapter(String mediaType) {
      advancedPlayer = initPlayer(mediaType);
   }

   private AdvancedPlaying initPlayer(String mediaType) {
      if (mediaType.equalsIgnoreCase("vlc"))    return new VlcPlayer();
      if (mediaType.equalsIgnoreCase("mp4"))    return new Mp4Player();
      else                                                   return null;
   }

   @Override
   public MediaPlaying play(
      String mediaType,
      String fileName
   ) {
      if (mediaType.equalsIgnoreCase("vlc")) {
         advancedPlayer.playVlc(fileName);
         return this;
      }
      if (mediaType.equalsIgnoreCase("mp4")) {
         advancedPlayer.playMp4(fileName);
         return this;
      }
      else {
         System.out.println("Định dạng không được hỗ trợ");
         return this;
      }
   }
}
```

#### Bước 4

Tạo `class MediaPlayer` triển khai `MediaPlaying`.

`adapterpattern/MediaPlayer.java`
```java
package adapterpattern;

public class MediaPlayer implements MediaPlaying {
   @Override
   public MediaPlaying play(
      String mediaType,
      String fileName
   ) {
      if (mediaType.equalsIgnoreCase("mp3")) {
         System.out.println("Đang phát tệp Mp3. Tên tệp: " + fileName);
         return this;
      }
      if (
         mediaType.equalsIgnoreCase("vlc") ||
         mediaType.equalsIgnoreCase("mp4")
      ) {
         MediaAdapter adapter = new MediaAdapter(mediaType);
         adapter.play(mediaType, fileName);
         return this;
      }
      else {
         System.out.println("Kiểu tệp không hợp lệ. Định dạng `" + mediaType + "` không được hỗ trợ.");
         return this;
      }
   }
}
```

#### Bước 5

Sử dụng `MediaPlayer` để phát các định dạng tệp khác nhau.

`PatternDemo.java`
```java
import adapterpattern.MediaPlayer;

public class PatternDemo {
   public static void main(String[] args) {
      MediaPlayer player = new MediaPlayer();
      player.play("mp3", "beyond the horizon.mp3")
            .play("mp4", "alone.mp4")
            .play("vlc", "far far away.vlc")
            .play("avi", "mind me.avi");
   }
}
```

#### Bước 6

Kiểm chứng lại kết quả in ra ở `console`.

```bat
Đang phát tệp Mp3. Tên tệp: beyond the horizon.mp3
Đang phát tệp Mp4. Tên tệp: alone.mp4
Đang phát tệp Vlc. Tên tệp: far far away.vlc
Kiểu tệp không hợp lệ. Định dạng `avi` không được hỗ trợ.
```


## Bridge Pattern

Bridge được sử dụng khi chúng ta cần tách một `abstract` khỏi `class` thực thể và khiến cho cả 2 đều trở nên linh động. Bridge được xếp vào nhóm các pattern Kiến Trúc.

Bridge sử dụng một giao diện đóng vai trò như một cầu nối giúp cho các chức năng của `class` thực thể trở nên độc lập và tách riêng khỏi các `class` tạo giao diện. Lúc này, cả 2 loại `class` đều có thể được chỉnh sửa linh động mà không ảnh hưởng lẫn nhau.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/956bbd62-e48a-4931-bc82-1308f18ef853.webp "Design Patterns")

Ở đây chúng ta có một phần mềm vẽ các hình phẳng 2D có màu sắc khác nhau. Thông thường để đơn giản thì chúng ta chỉ cần có `01 class base` là `Circle` và tạo ra các `object` hình tròn có thuộc tính màu sắc khác nhau để vẽ. Lúc này, giao diện được sử dụng để vẽ là phương thức `draw()` của class `Circle`.

Tuy nhiên lúc này vấn đề nảy sinh là nếu như chúng ta muốn thay đổi cách hoạt động của `draw()`, thì việc chỉnh sửa sẽ phải thực hiện trực tiếp trên `class Circle`. Hoặc ví dụ như chúng ta có ý định chỉnh sửa `class Circle` thì cũng phải coi chừng cái thuộc tính màu sắc kẻo ảnh hưởng đến `draw()`.

Để tách rời giao diện `draw()` và `Circle`, một `bridge` được tạo ra bởi `interface Drawing`. Các `class` triển khai `DrawingRed` và `DrawingGreen` sẽ được `Circle` ủy thác hoàn toàn tác vụ `draw()` chi tiết. Như vậy, giờ đây chúng ta có thể yên tâm thực hiện những điều chỉnh cần thiết trên `Circle` mà không gây ảnh hưởng đến giao diện `draw()` đang hoạt động và ngược lại.

#### Bước 1

Tạo `interface bridge`.

`bridgepattern/drawingapi/Drawing.java`
```java
package bridgepattern.drawingapi;

public interface Drawing {
   public void draw(int x, int y, int radius);
}
```

#### Bước 2

Tạo các `class` triển khai `Drawing`.

`bridgepattern/drawingapi/DrawingGreen.java`
```java
package bridgepattern.drawingapi;

public class DrawingGreen implements Drawing {
   @Override
   public void draw (int radius, int x, int y) {
      System.out.println("=== Đang vẽ hình tròn..");
      System.out.println("Màu sắc: Xanh lá");
      System.out.println("Tọa độ tâm: (" + x + ", " + y + ")");
      System.out.println("Bán kính: " + radius);
   }
}
```

`bridgepattern/drawingapi/DrawingRed.java`
```java
package bridgepattern.drawingapi;

public class DrawingRed implements Drawing {
   @Override
   public void draw(int x, int y, int radius) {
      System.out.println("=== Đang vẽ hình tròn..");
      System.out.println("Màu sắc: Đỏ");
      System.out.println("Tọa độ tâm: (" + x + ", " + y + ")");
      System.out.println("Bán kính: " + radius);
   }
}
```

#### Bước 3

Tạo `abstract Shape` sử dụng giao diện `Drawing`.

`bridgepattern/Shape.java`
```java
package bridgepattern;

import bridgepattern.drawingapi.Drawing;

abstract public class Shape {
   protected Drawing drawingAPI;

   protected Shape(Drawing api) {
      drawingAPI = api;
   }

   public abstract void draw();
}
```

#### Bước 4

Tạo `class Circle` mở rộng `Shape`.

`bridgepattern/Circle.java`
```java
package bridgepattern;

import bridgepattern.drawingapi.Drawing;

public class Circle extends Shape {
   private int x, y, radius;

   public Circle(int x, int y, int radius, Drawing api) {
      super(api);
      this.x = x;
      this.y = y;
      this.radius = radius;
   }

   @Override
   public void draw() {
      drawingAPI.draw(x, y, radius);
   }
}
```

#### Bước 5

Sử dụng `Shape` và các `class Drawing` để vẽ các hình tròn với màu sắc khác nhau.

`PatternDemo.java`
```java
import bridgepattern.Circle;
import bridgepattern.drawingapi.DrawingGreen;
import bridgepattern.drawingapi.DrawingRed;
import bridgepattern.Shape;

public class PatternDemo {
   public static void main(String[] args) {
      Shape circleRed = new Circle(100, 100, 10, new DrawingRed());
      circleRed.draw();

      Shape circleGreen = new Circle(100, 100, 10, new DrawingGreen());
      circleGreen.draw();
   }
}
```

#### Bước 6

Kiểm chứng lại kết quả in ra ở `console`.

```java
=== Đang vẽ hình tròn..
Màu sắc: Đỏ
Tọa độ tâm: (100, 100)
Bán kính: 10
=== Đang vẽ hình tròn..
Màu sắc: Xanh lá
Tọa độ tâm: (100, 10)
Bán kính: 100
```


## Filter Pattern

Filter còn có tên gọi khác là Criteria. Cả 2 cách gọi này đều có nghĩa là sàng lọc hay màng lọc. Filter được xếp vào nhóm các pattern Kiến Trúc.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/f435a539-ba82-45c5-b160-80e80ed4095e.png "Design Patterns")

- Chúng ta có 1 danh sách người dùng được tạo bởi `class Person`.
- Để lọc danh sách này theo những tiêu chí khác nhau, chúng ta tạo ra một giao diện `Filter` và các `class` triển khai.
- Code `main` tại `PatternDemo` sẽ sử dụng các object `Filter` để lọc danh sách `List<Person>` theo các tiêu chí.


#### Bước 1

Tạo `class Person` để mô tả người dùng.

`filterperson/Person.java`
```java
package filterperson;

public class Person {
   private String name;
   private String gender;
   private String status;

   public Person(
      String name,
      String gender,
      String status
   ) {
      this.name = name;
      this.gender = gender;
      this.status = status;
   }

   public String getName() {
      return name;
   }

   public String getGender() {
      return gender;
   }

   public String getStatus() {
      return status;
   }
}
```

#### Bước 2

Tạo giao diện `Filter`.

`filterperson/Filter.java`
```java
package filterperson;

import java.util.List;

public interface Filter {
   public List<Person> match(List<Person> personList);
}
```

#### Bước 3

Tạo các `class` triển khai giao diện `Filter`.

`filterperson/FilterMale.java`
```java
package filterperson;

import java.util.ArrayList;
import java.util.List;

public class FilterMale implements Filter {
   @Override
   public List<Person> match(List<Person> personList) {
      List<Person> males = new ArrayList<Person>();

      for (Person p : personList)
         if (p.getGender().equalsIgnoreCase("male"))
            males.add(p);

      return males;
   }
}
```

`filterperson/FilterFemale.java`
```java
package filterperson;

import java.util.ArrayList;
import java.util.List;

public class FilterFemale implements Filter {
   @Override
   public List<Person> match(List<Person> personList) {
      List<Person> females = new ArrayList<Person>();

      for (Person p : personList)
         if (p.getGender().equalsIgnoreCase("female"))
            females.add(p);

      return females;
   }
}
```

`filterperson/FilterSingle.java`
```java
package filterperson;

import java.util.ArrayList;
import java.util.List;

public class FilterSingle implements Filter {
   @Override
   public List<Person> match(List<Person> personList) {
      List<Person> singles = new ArrayList<Person>();

      for (Person p : personList)
         if (p.getStatus().equalsIgnoreCase("single"))
            singles.add(p);

      return singles;
   }
}
```

`filterperson/FilterAnd.java`
```java
package filterperson;

import java.util.List;

public class FilterAnd implements Filter {
   private Filter firstFilter;
   private Filter secondFilter;

   public FilterAnd(
      Filter firstFilter,
      Filter secondFilter
   ) {
      this.firstFilter = firstFilter;
      this.secondFilter = secondFilter;
   }

   @Override
   public List<Person> match(List<Person> personList) {
      List<Person> firstMatched = firstFilter.match(personList);
      return secondFilter.match(firstMatched);
   }
}
```

`filterperson/FilterOr.java`
```java
package filterperson;

import java.util.List;

public class FilterOr implements Filter {
   private Filter firstFilter;
   private Filter secondFilter;

   public FilterOr(
      Filter firstFilter,
      Filter secondFilter
   ) {
      this.firstFilter = firstFilter;
      this.secondFilter = secondFilter;
   }

   @Override
   public List<Person> match(List<Person> personList) {
      List<Person> firstMatched = firstFilter.match(personList);
      List<Person> secondMatched = secondFilter.match(personList);

      for (Person p : secondMatched)
         if (! firstMatched.contains(p))
            firstMatched.add(p);

      return firstMatched;
   }
}
```

#### Bước 4

Sử dụng `Shape` và các `class Drawing` để vẽ các hình tròn với màu sắc khác nhau.

`PatternDemo.java`
```java
import filterperson.*;

import java.util.ArrayList;
import java.util.List;

public class PatternDemo {
   public static void main(String[] args) {
      List<Person> personList = new ArrayList<Person>();

      personList.add(new Person("Robert","Male", "Single"));
      personList.add(new Person("John", "Male", "Married"));
      personList.add(new Person("Laura", "Female", "Married"));
      personList.add(new Person("Diana", "Female", "Single"));
      personList.add(new Person("Mike", "Male", "Single"));
      personList.add(new Person("Bobby", "Male", "Single"));

      Filter filterMale = new FilterMale();
      Filter filterFemale = new FilterFemale();
      Filter filterSingle = new FilterSingle();
      Filter filterSingleAndMale = new FilterAnd(filterSingle, filterMale);
      Filter filterSingleOrFemale = new FilterOr(filterSingle, filterFemale);

      System.out.println("MALE:");
      print(filterMale.match(personList));

      System.out.println("FEMALE:");
      print(filterFemale.match(personList));

      System.out.println("SINGLE and MALE:");
      print(filterSingleAndMale.match(personList));

      System.out.println("SINGLE or FEMALE");
      print(filterSingleOrFemale.match(personList));
   }

   public static void print(List<Person> personList) {
      for (Person p : personList) {
         System.out.println(
            "[ Name: " + p.getName() +
            ", Gender: " + p.getGender() +
            ", Status: " + p.getStatus() + " ]"
         );
      }
   }
}
```

#### Bước 5

Kiểm chứng lại kết quả in ra ở `console`.

```bat
MALE:
[ Name: Robert, Gender: Male, Status: Single ]
[ Name: John, Gender: Male, Status: Married ]
[ Name: Mike, Gender: Male, Status: Single ]
[ Name: Bobby, Gender: Male, Status: Single ]
FEMALE:
[ Name: Laura, Gender: Female, Status: Married ]
[ Name: Diana, Gender: Female, Status: Single ]
SINGLE and MALE:
[ Name: Robert, Gender: Male, Status: Single ]
[ Name: Mike, Gender: Male, Status: Single ]
[ Name: Bobby, Gender: Male, Status: Single ]
SINGLE or FEMALE
[ Name: Robert, Gender: Male, Status: Single ]
[ Name: Diana, Gender: Female, Status: Single ]
[ Name: Mike, Gender: Male, Status: Single ]
[ Name: Bobby, Gender: Male, Status: Single ]
[ Name: Laura, Gender: Female, Status: Married ]
```


## Composite Pattern

Composite được hiểu nôm na là tổng hợp. Composite được sử dụng khi chúng ta muốn làm việc với một nhóm các `object` như một `object` đơn duy nhất. Composite được xếp vào nhóm các pattern Kiến Trúc.

Composite tạo ra một `class` có chứa nhóm các `object` của chính `class` đó và đồng thời cung cấp các phương thức để làm việc với nhóm các `object` này.

#### Áp dụng triển khai

![Design Patterns](https://boxxv.github.io/img/patterns/40b1d862-e26d-4c87-8cb0-64d337f1b3f2.png "Design Patterns")

- Chúng ta có một phần mềm mô tả kiến trúc nhân sự của một cửa hàng.
- `01 class Employee` được tạo ra để mô tả thực thể nhân viên.
- Mỗi `object Employee` cũng có thể chứa danh sách các nhân viên cấp thấp hơn.
- Code `main` trong `PatternDemo` sẽ sử dụng `class Employee` để tạo một kiến trúc nhân sự và in ra danh sách tất cả các nhân viên.


#### Bước 1

Tạo `class Employee`.

`compositepattern/Employee.java`
```java
package compositepattern;

import java.util.ArrayList;
import java.util.List;

public class Employee {
   private String name;
   private String role;
   private int salary;
   private List<Employee> subordinateList;

   public Employee(
      String name,
      String role,
      int salary
   ) {
      this.name = name;
      this.salary = salary;
      this.role = role;
      this.subordinateList = new ArrayList<Employee>();
   }

   public void addSub(Employee emp) {
      subordinateList.add(emp);
   }

   public void removeSub(Employee emp) {
      subordinateList.remove(emp);
   }

   public List<Employee> getSubList() {
      return subordinateList;
   }

   public String toString() {
      return "Employee: [ Name: " + name + ", Role: " + role + ", Salary : " + salary+" ]";
   }
}
```

#### Bước 2

Sử dụng `class Employee` để tạo và in danh sách nhân viên.

`PatternDemo.java`
```java
import compositepattern.Employee;

public class PatternDemo {
   public static void main(String[] args) {
      Employee CEO = new Employee("John","CEO", 30000);

      Employee headSales = new Employee("Robert","Head Sales", 20000);
      CEO.addSub(headSales);

      Employee headMarketing = new Employee("Micheal","Head Marketing", 20000);
      CEO.addSub(headMarketing);

      Employee sale1 = new Employee("Richard","Sales", 10000);
      headSales.addSub(sale1);
      Employee sale2 = new Employee("Rob","Sales", 10000);
      headSales.addSub(sale2);

      Employee clerk1 = new Employee("Laura","Marketing", 10000);
      headMarketing.addSub(clerk1);
      Employee clerk2 = new Employee("Ryan","Marketing", 10000);
      headMarketing.addSub(clerk2);

      // in danh sách tất cả các nhân viên
      System.out.println(CEO);
      for (Employee headEmployee : CEO.getSubList()) {
         System.out.println(headEmployee);
         for (Employee employee : headEmployee.getSubList()) {
            System.out.println(employee);
         }
      }
   }
}
```

#### Bước 3

Kiểm chứng lại kết quả được in ra ở `console`.

```java
Employee: [ Name: John, Role: CEO, Salary : 30000 ]
Employee: [ Name: Robert, Role: Head Sales, Salary : 20000 ]
Employee: [ Name: Richard, Role: Sales, Salary : 10000 ]
Employee: [ Name: Rob, Role: Sales, Salary : 10000 ]
Employee: [ Name: Micheal, Role: Head Marketing, Salary : 20000 ]
Employee: [ Name: Laura, Role: Marketing, Salary : 10000 ]
Employee: [ Name: Ryan, Role: Marketing, Salary : 10000 ]
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
