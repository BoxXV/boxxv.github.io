---
layout: post
title: Tổng hợp về Design Pattern
subtitle: Nhập môn Design Patterns
tags:
- Csharp
- Design Patterns
- Creational
- Structural
- Behavioral
---

Có thể chúng ta đã gặp Design patterns ở đâu đó trong các ứng dụng, cũng có thể chúng ta đã từng sử dụng những mẫu tương tự như Design pattern để giải quyết những tình huống của mình, nhưng chúng ta không rõ hoặc không có một khái niệm gì về nó. Trong bài này, chúng ta sẽ cùng tìm hiểu một số kiến thức tổng quan Design Pattern, sau đó sẽ tìm hiểu chi tiết về từng Design Pattern trong các bài viết tiếp theo.

### 1. Design Patterns là gì?

`Design Patterns` (mẫu thiết kế) là một kỹ thuật trong lập trình hướng đối tượng, nó khá quan trọng và mọi lập trình viên muốn giỏi đều phải biết. Design Pattern được sử dụng thường xuyên trong các ngôn ngữ OOP. Nó cung cấp cho bạn các “mẫu thiết kế”, giải pháp để giải quyết các vấn đề chung, thường gặp trong lập trình. Các vấn đề mà bạn gặp phải có thể bạn sẽ tự nghĩ ra cách giải quyết nhưng có thể nó chưa phải là tối ưu. Design Pattern giúp bạn giải quyết vấn đề một cách tối ưu nhất, cung cấp cho bạn các giải pháp trong lập trình OOP.

**Design Patterns** không phải là ngôn ngữ cụ thể nào cả. Nó có thể thực hiện được ở phần lớn các ngôn ngữ lập trình, chẳng hạn như Java, C#, thậm chí là Javascript hay bất kỳ ngôn ngữ lập trình nào khác.

> Mỗi pattern mô tả một vấn đề xảy ra lặp đi lặp lại, và trình bày trọng tâm của giải pháp cho vấn đề đó, theo cách mà bạn có thể dùng đi dùng lại hàng triệu lần mà không cần phải suy nghĩ.
— Christopher Alexander —

-----

### 2. Tại sao phải sử dụng Design Patterns?

Design Pattern giúp bạn tái sử dụng mã lệnh và dẽ dàng mở rộng.

Nó là tập hơn những giải pháp đã được tối ưu hóa, đã được kiểm chứng để giải quyết các vấn đề trong software engineering. Vậy khi bạn gặp bất kỳ khó khăn gì, design patterns là kim chỉ nam giúp bạn giải quyết vấn đề thay vì tự tìm kiếm giải pháp cho một vấn đề đã được chứng minh.

Design pattern cung cấp giải pháp ở dạng tổng quát, giúp tăng tốc độ phát triển phần mềm bằng cách đưa ra các mô hình test, mô hình phát triển đã qua kiểm nghiệm.

Dùng lại các design pattern giúp tránh được các vấn đề tiềm ẩn có thể gây ra những lỗi lớn, dễ dàng nâng cấp, bảo trì về sau.

Giúp cho các lập trình viên có thể hiểu code của người khác 1 cách nhanh chóng (có thể hiểu là tính communicate). Mọi thành viên trong team có thể dễ dàng trao đổi với nhau để cùng xây dựng dự án mà không mất quá nhiều thời gian.

-----

### 3. Khi nào nên sử dụng Design patterns?

Khi bạn muốn giữ cho chương trình của mình thực sự đơn giản. Việc sử dụng các design pattern sẽ giúp chúng ta giảm được thời gian và công sức suy nghĩ ra các cách giải quyết cho những vấn đề đã có lời giải.

-----

### 4. Phân loại Design Patterns

Năm 1994, bốn tác giả **Erich Gamma, Richard Helm, Ralph Johnson và John Vlissides** đã cho xuất bản một cuốn sách với tiêu đề **Design Patterns – Elements of Reusable Object-Oriented Software**, đây là khởi nguồn của khái niệm design pattern trong lập trình phần mềm.

Bốn tác giả trên được biết đến rộng rãi dưới tên **Gang of Four** (bộ tứ). Theo quan điểm của bốn người, design pattern chủ yếu được dựa theo những quy tắc sau đây về thiết kế hướng đối tượng.

![Design Patterns](https://boxxv.github.io/img/patterns/design-patterns-classify.png "Design Patterns")_Design Patterns_

Hệ thống các mẫu Design pattern hiện có **23 mẫu** được định nghĩa trong cuốn "**Design patterns Elements of Reusable Object Oriented Software**" và được chia thành **3 nhóm**:

- `Creational Pattern` (nhóm khởi tạo – 5 mẫu) gồm: Factory Method, Abstract Factory, Builder, Prototype, Singleton. Những Design pattern loại này cung cấp một giải pháp để tạo ra các object và che giấu được logic của việc tạo ra nó, thay vì tạo ra object một cách trực tiếp bằng cách sử dụng method new. Điều này giúp cho chương trình trở nên mềm dẻo hơn trong việc quyết định object nào cần được tạo ra trong những tình huống được đưa ra.
- `Structural Pattern` (nhóm cấu trúc – 7 mẫu) gồm: Adapter, Bridge, Composite, Decorator, Facade, Flyweight và Proxy. Những Design pattern loại này liên quan tới class và các thành phần của object. Nó dùng để thiết lập, định nghĩa quan hệ giữa các đối tượng.
- `Behavioral Pattern` (nhóm tương tác/ hành vi – 11 mẫu) gồm: Interpreter, Template Method, Chain of Responsibility, Command, Iterator, Mediator, Memento, Observer, State, Strategy và Visitor. Nhóm này dùng trong thực hiện các hành vi của đối tượng, sự giao tiếp giữa các object với nhau.

Hình dưới là mối quan hệ giữa 23 Design Pattern cơ bản (GoF):

![Relationships between Design Patterns](https://boxxv.github.io/img/patterns/relationwithpatterns2.jpg "Relationships between Design Patterns")_Relationships between Design Patterns_

-----
### 4.1. Nhóm Creational (nhóm khởi tạo)

![Creational](https://boxxv.github.io/img/patterns/Creational.png "Creational")_Creational_

- [Singleton](https://gpcoder.com/4190-huong-dan-java-design-pattern-singleton/)
  - Đảm bảo 1 class chỉ có 1 instance và cung cấp 1 điểm truy xuất toàn cục đến nó.
  - Tần suất sử dụng: cao trung bình.

- [Abstract Factory](https://gpcoder.com/4365-huong-dan-java-design-pattern-abstract-factory/)
  - Cung cấp một interface cho việc tạo lập các đối tượng (có liên hệ với nhau) mà không cần qui định lớp khi hay xác định lớp cụ thể (concrete) tạo mỗi đối tượng.
  - Tần suất sử dụng: cao.

- [Factory Method](https://gpcoder.com/4352-huong-dan-java-design-pattern-factory-method/)
  - Định nghĩa Interface để sinh ra đối tượng nhưng để cho lớp con quyết định lớp nào được dùng để sinh ra đối tượng Factory method cho phép một lớp chuyển quá trình khởi tạo đối tượng cho lớp con.
  - Tần suất sử dụng: cao.

- [Builder](https://gpcoder.com/4434-huong-dan-java-design-pattern-builder/)
  - Tách rời việc xây dựng (construction) một đối tượng phức tạp khỏi biểu diễn của nó sao cho cùng một tiến trình xây dựng có thể tạo được các biểu diễn khác nhau.
  - Tần suất sử dụng: trung bình thấp.

- [Prototype](https://gpcoder.com/4413-huong-dan-java-design-pattern-prototype/)
  - Qui định loại của các đối tượng cần tạo bằng cách dùng một đối tượng mẫu, tạo mới nhờ vào sao chép đối tượng mẫu này.
  - Tần suất sử dụng: trung bình.


-----
### 4.2. Nhóm Structural (nhóm cấu trúc)

![Structural](https://boxxv.github.io/img/patterns/Structural.png "Structural")_Structural_

- [Adapter](https://gpcoder.com/4483-huong-dan-java-design-pattern-adapter/)
  - Do vấn đề tương thích, thay đổi interface của một lớp thành một interface khác phù hợp với yêu cầu người sử dụng lớp.
  - Tần suất sử dụng: cao trung bình.

- [Bridge](https://gpcoder.com/4520-huong-dan-java-design-pattern-bridge/)
  - Tách rời ngữ nghĩa của một vấn đề khỏi việc cài đặt, mục đích để cả hai bộ phận (ngữ nghĩa và cài đặt) có thể thay đổi độc lập nhau.
  - Tần suất sử dụng: trung bình.

- [Composite](https://gpcoder.com/4554-huong-dan-java-design-pattern-composite/)
  - Tổ chức các đối tượng theo cấu trúc phân cấp dạng cây. Tất cả các đối tượng trong cấu trúc được thao tác theo một cách thuần nhất như nhau.
Tạo quan hệ thứ bậc bao gộp giữa các đối tượng. Client có thể xem đối tượng bao gộp và bị bao gộp như nhau -> khả năng tổng quát hoá trong code của client -> dễ phát triển, nâng cấp, bảo trì.
  - Tần suất sử dụng: cao trung bình.

- [Decorator](https://gpcoder.com/4574-huong-dan-java-design-pattern-decorator/)
  - Gán thêm trách nhiệm cho đối tượng (mở rộng chức năng) vào lúc chạy (dynamically).
  - Tần suất sử dụng:trung bình.

- [Facade](https://gpcoder.com/4604-huong-dan-java-design-pattern-facade/)
  - Cung cấp một interface thuần nhất cho một tập hợp các interface trong một “hệ thống con” (subsystem). Nó định nghĩa 1 interface cao hơn các interface có sẵn để làm cho hệ thống con dễ sử dụng hơn.
  - Tần suất sử dụng: cao.

- [Flyweight](https://gpcoder.com/4626-huong-dan-java-design-pattern-flyweight/)
  - Sử dụng việc chia sẻ để thao tác hiệu quả trên một số lượng lớn đối tượng “cở nhỏ” (chẳng hạn paragraph, dòng, cột, ký tự…).
  - Tần suất sử dụng: thấp.

- [Proxy](https://gpcoder.com/4644-huong-dan-java-design-pattern-proxy/)
  - Cung cấp đối tượng đại diện cho một đối tượng khác để hỗ trợ hoặc kiểm soát quá trình truy xuất đối tượng đó. Đối tượng thay thế gọi là proxy.
  - Tần suất sử dụng: cao trung bình.



-----
### 4.2. Nhóm Behavioral (nhóm hành vi/ tương tác)

![Behavioral](https://boxxv.github.io/img/patterns/Behavioral.png "Behavioral")_Behavioral_

- [Chain of Responsibility](https://gpcoder.com/4665-huong-dan-java-design-pattern-chain-of-responsibility/)
  - Khắc phục việc ghép cặp giữa bộ gởi và bộ nhận thông điệp. Các đối tượng nhận thông điệp được kết nối thành một chuỗi và thông điệp được chuyển dọc theo chuỗi nầy đến khi gặp được đối tượng xử lý nó. Tránh việc gắn kết cứng giữa phần tử gởi request với phần tử nhận và xử lý request bằng cách cho phép hơn 1 đối tượng có có cơ hội xử lý request. Liên kết các đối tượng nhận request thành 1 dây chuyền rồi gửi request xuyên qua từng đối tượng xử lý đến khi gặp đối tượng xử lý cụ thể.
  - Tần suất sử dụng: trung bình thấp.

- [Command](https://gpcoder.com/4686-huong-dan-java-design-pattern-command/)
  - Mỗi yêu cầu (thực hiện một thao tác nào đó) được bao bọc thành một đối tượng. Các yêu cầu sẽ được lưu trữ và gởi đi như các đối tượng.Đóng gói request vào trong một Object, nhờ đó có thể nthông số hoá chương trình nhận request và thực hiện các thao tác trên request: sắp xếp, log, undo…
  - Tần suất sử dụng: cao trung bình.

- [Interpreter](https://gpcoder.com/4702-huong-dan-java-design-pattern-interpreter/)
  - Hỗ trợ việc định nghĩa biểu diễn văn phạm và bộ thông dịch cho một ngôn ngữ.
  - Tần suất sử dụng: thấp.

- [Iterator](https://gpcoder.com/4724-huong-dan-java-design-pattern-iterator/)
  - Truy xuất các phần tử của đối tượng dạng tập hợp tuần tự (list, array, …) mà không phụ thuộc vào biểu diễn bên trong của các phần tử.
  - Tần suất sử dụng: cao.

- [Mediator](https://gpcoder.com/4740-huong-dan-java-design-pattern-mediator/)
  - Hiệu chỉnh và trả lại như cũ trạng thái bên trong của đối tượng mà vẫn không vi phạm việc bao bọc dữ liệu.
  - Tần suất sử dụng: thấp.

- [Observer](https://gpcoder.com/4747-huong-dan-java-design-pattern-observer/)
  - Định nghĩa sự phụ thuộc một-nhiều giữa các đối tượng sao cho khi một đối tượng thay đổi trạng thái thì tất cả các đối tượng phụ thuộc nó cũng thay đổi theo.
  - Tần suất sử dụng: cao.

- [State](https://gpcoder.com/4785-huong-dan-java-design-pattern-state/)
  - Cho phép một đối tượng thay đổi hành vi khi trạng thái bên trong của nó thay đổi, ta có cảm giác như class của đối tượng bị thay đổi.
  - Tần suất sử dụng: trung bình.

- [Strategy](https://gpcoder.com/4796-huong-dan-java-design-pattern-strategy/)
  - Bao bọc một họ các thuật toán bằng các lớp đối tượng để thuật toán có thể thay đổi độc lập đối với chương trình sử dụng thuật toán.Cung cấp một họ giải thuật cho phép client chọn lựa linh động một giải thuật cụ thể khi sử dụng.
  - Tần suất sử dụng: cao trung bình.

- [Template Method](https://gpcoder.com/4810-huong-dan-java-design-pattern-template-method/)
  - Định nghĩa phần khung của một thuật toán, tức là một thuật toán tổng quát gọi đến một số phương thức chưa được cài đặt trong lớp cơ sở; việc cài đặt các phương thức được ủy nhiệm cho các lớp kế thừa.
  - Tần suất sử dụng: trung bình.

- [Visitor](https://gpcoder.com/4813-huong-dan-java-design-pattern-visitor/)
  - Cho phép định nghĩa thêm phép toán mới tác động lên các phần tử của một cấu trúc đối tượng mà không cần thay đổi các lớp định nghĩa cấu trúc đó.
  - Tần suất sử dụng: thấp.


-----

### 5. Để học Design Patterns cần có gì?

Để học tốt Design Pattern bạn nắm vững được Bốn đặc tính của OOP: Kế thừa, Đa hình, Trừu tượng, Bao đóng.

Tiếp theo là hai khái niệm interface và abstract : cái này cực kỳ quan trọng, để hiểu và áp dụng 2 khái niệm này có thể sẽ mất một thời gian, nhưng khi bạn nắm chắc nó bạn sẽ thấy nó thực sự cần thiết.

Bỏ tư duy theo lối cấu trúc, nâng tư duy hoàn toàn OOP.

Sau khi bạn đã nắm chắc các thứ kể trên, bạn nên bắt tay vào học Design Pattern càng sớm càng tốt. Design Pattern giúp bạn đặt trình cao mới :).

-----

### 6. Học ở đâu?

Sách:
- Design Patterns: Elements of Reusable Object-Oriented Software
- Head First Design Patterns
- Design Patterns For Dummies
- Pattern Hatching: Design Patterns Applied.
- Refactoring to Patterns.
- Patterns of Enterprise Application Architecture.

Các website viết về Design Pattern:
- https://sourcemaking.com/design_patterns
- https://refactoring.guru
- https://www.tutorialspoint.com/design_pattern/index.htm
- https://www.javatpoint.com/design-patterns-in-java
- http://www.oodesign.com/
- http://java-design-patterns.com
- http://www.javacamp.org/designPattern/
- <del>http://www.thejavageek.com/design-patterns/</del>
- https://en.wikipedia.org/wiki/Software_design_pattern
- dotNet Design Patterns: https://www.dofactory.com/net/design-patterns
- Javascript Design Patterns: https://www.dofactory.com/javascript/design-patterns


-----

### 7. Học Design Pattern như thế nào?

Để học tốt một Design Pattern bạn hãy tập trung chú ý vào 3 phần sau:
- Nó được sử dụng khi nào, vấn đề mà design pattern đó giải quyết là gì?
- Sơ đồ UML mô tả design pattern.
- Code minh họa, ứng dụng thực tiễn của nó là gì?


-----

### 8. Lời kết

Design pattern thể hiện tính kinh nghiệm của công việc lập trình, xây dựng và thiết kế phần mềm. Người hiểu và vận dụng được Design Pattern thích hợp trong hệ thống sẽ tiết kiệm được rất nhiều thời gian, công sức, dễ phát triển, mở rộng, bảo trì. Tuy nhiên không nên quá lạm dụng nó.

Chúng ta nên nhớ rằng:
- Design patterns là 1 đoạn mô tả, hoặc 1 khuôn mẫu để giải quyết 1 vấn đề nào đó. Nó không phải là thiết kế cuối cùng.
- Design Pattern được tạo ra để giải quyết vấn đề, chứ không phải để phức tạp hóa nó.
- Design Pattern giúp code được tối ưu hóa, dễ tái sử dụng, dễ hiểu, dễ nâng cấp sửa chữa.

Qua bài này mình hi vọng mọi người có thể hiểu hơn về design pattern và ưu điểm của nó. Bài tiếp theo chúng ta sẽ đi vào tìm hiểu từng mẫu Design Patterns. Vào chi tiết, nội dung tôi sẽ sử dụng thông tin chủ yếu từ trang SourceMaking, TutorialsPoint , sách Design Patterns – Elements of Reusable Object-Oriented Software (GOF), Design Pattern for dummies và tìm hiểu thêm những kiến thức từ nhiều trang khác để các bạn dễ hiểu hơn. Vì đây là những kiến thức nâng cao nên tôi cũng phải tìm hiểu từ rất nhiều nguồn để tổng hợp lại, cũng như những kinh nghiệm trong các dự án thực tế vào bài viết để giúp cho các bạn dễ tiếp cận nhất có thể. Mong nhận được sự phản hồi và góp ý của các bạn. Thanks a lot!!!



-----
Tham khảo:
- [Giới thiệu Design Patterns](https://gpcoder.com/4164-gioi-thieu-design-patterns/)
- [Nhập môn Design Pattern (Phong cách kiếm hiệp)](https://toidicodedao.com/2016/03/01/nhap-mon-design-pattern-phong-cach-kiem-hiep/)
- [Tổng quan về Design Pattern](https://www.swiftyvn.com/2018/09/tong-quan-ve-design-pattern/#ph%C3%A2n-lo%E1%BA%A1i-design-pattern)
- [https://tuanitpro.com/design-pattern-la-gi/](https://tuanitpro.com/design-pattern-la-gi/)
- [https://blog.duyet.net/2015/02/oop-design-patterns-la-gi.html](https://blog.duyet.net/2015/02/oop-design-patterns-la-gi.html)
- [https://refactoring.guru/design-patterns/catalog](https://refactoring.guru/design-patterns/catalog)
- [https://www.ibm.com/developerworks/java/tutorials/j-patterns/j-patterns.html](https://www.ibm.com/developerworks/java/tutorials/j-patterns/j-patterns.html)
- [https://www.journaldev.com/1827/java-design-patterns-example-tutorial](https://www.journaldev.com/1827/java-design-patterns-example-tutorial)
- [https://viblo.asia/tags/design-pattern](https://viblo.asia/tags/design-pattern)
- [Lập trình cho interface chứ không phải để implement interface đó.](https://stackoverflow.com/questions/2697783/what-does-program-to-interfaces-not-implementations-mean)
- [Ưu tiên object composition (chứa trong) hơn là inheritance (thừa kế).](https://stackoverflow.com/questions/49002/prefer-composition-over-inheritance)
