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
- [Entity-Attribute-Value](https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model): Thực thể-Thuộc tính-Giá trị, Một bảng cho Sản phẩm và một bảng xoay các thuộc tính thành hàng, thay vì cột. EAV không phải là một thiết kế hợp lệ đối với mô hình quan hệ, nhưng nhiều người vẫn sử dụng nó. Đây là “Mô hình thuộc tính” được đề cập bởi một câu trả lời khác. Xem các câu hỏi khác với thẻ [eav](https://stackoverflow.com/questions/tagged/entity-attribute-value?tab=Active) trên StackOverflow để biết một số cạm bẫy.

Về cơ bản, không có giải pháp nào trong số này dễ dàng hoặc hiệu quả trong cơ sở dữ liệu quan hệ. Toàn bộ ý tưởng về việc có "các thuộc tính biến đổi" về cơ bản là mâu thuẫn với lý thuyết quan hệ.

Điều quan trọng là bạn phải chọn một trong những giải pháp dựa trên đó là giải pháp ít xấu nhất cho ứng dụng của bạn. Do đó, bạn cần biết mình sẽ truy vấn dữ liệu như thế nào trước khi chọn thiết kế cơ sở dữ liệu. Không có cách nào để chọn một giải pháp "tốt nhất" bởi vì bất kỳ giải pháp nào trong số các giải pháp đều có thể tốt nhất cho một ứng dụng nhất định. 


## Single Table Inheritance

> Biểu diễn một hệ thống phân cấp kế thừa của các lớp dưới dạng một bảng duy nhất có các cột cho tất cả các trường của các lớp khác nhau.

![Single Table Inheritance](https://boxxv.github.io/img/db/singleTableInheritance.png "Single Table Inheritance")

Cơ sở dữ liệu quan hệ không hỗ trợ kế thừa, vì vậy khi ánh xạ từ các đối tượng đến cơ sở dữ liệu, chúng ta phải xem xét cách thể hiện các cấu trúc kế thừa tốt đẹp của chúng ta trong các bảng quan hệ. Khi ánh xạ tới cơ sở dữ liệu quan hệ, chúng tôi cố gắng giảm thiểu các phép nối có thể nhanh chóng gắn kết khi xử lý cấu trúc kế thừa trong nhiều bảng. Kế thừa bảng đơn ánh xạ tất cả các trường của tất cả các lớp của cấu trúc kế thừa thành một bảng duy nhất.

Để có mô tả đầy đủ, hãy xem [Patterns of Enterprise Application Architecture](https://martinfowler.com/books/eaa.html) trang 278


## Class Table Inheritance

> Đại diện cho một hệ thống phân cấp kế thừa của các lớp với một bảng cho mỗi lớp.

![Class Table Inheritance](https://boxxv.github.io/img/db/classTableInheritance.png "Class Table Inheritance")

Một khía cạnh rất dễ thấy của sự không khớp đối tượng-quan hệ là thực tế là cơ sở dữ liệu quan hệ không hỗ trợ kế thừa. Bạn muốn cấu trúc cơ sở dữ liệu ánh xạ rõ ràng đến các đối tượng và cho phép liên kết ở bất kỳ đâu trong cấu trúc kế thừa. Kế thừa bảng lớp hỗ trợ điều này bằng cách sử dụng một bảng cơ sở dữ liệu cho mỗi lớp trong cấu trúc kế thừa. 

#### How It Works

Điều đơn giản về Kế thừa Bảng Lớp là nó có một bảng cho mỗi lớp trong mô hình miền. Các trường trong lớp miền ánh xạ trực tiếp đến các trường trong các bảng tương ứng. Như với các ánh xạ kế thừa khác, áp dụng phương pháp cơ bản của Trình lập bản đồ kế thừa (302).

Một vấn đề là làm thế nào để liên kết các hàng tương ứng của các bảng cơ sở dữ liệu. Một giải pháp khả thi là sử dụng một giá trị khóa chính chung sao cho hàng khóa 101 trong bảng cầu thủ và hàng khóa 101 trong bảng cầu thủ tương ứng với cùng một đối tượng miền. Vì bảng siêu lớp có một hàng cho mỗi hàng trong các bảng khác, các khóa chính sẽ là duy nhất trên các bảng nếu bạn sử dụng lược đồ này. Một giải pháp thay thế là để mỗi bảng có các khóa chính của riêng nó và sử dụng các khóa ngoại vào bảng lớp cha để buộc các hàng lại với nhau.

Vấn đề triển khai lớn nhất với Kế thừa bảng lớp là làm thế nào để đưa dữ liệu trở lại từ nhiều bảng một cách hiệu quả. Rõ ràng, việc thực hiện lệnh gọi cho từng bảng là không tốt vì bạn có nhiều lệnh gọi đến cơ sở dữ liệu. Bạn có thể tránh điều này bằng cách nối các bảng thành phần khác nhau; tuy nhiên, các phép nối cho hơn ba hoặc bốn bảng có xu hướng chậm do cách cơ sở dữ liệu thực hiện tối ưu hóa của chúng. 

Trên hết đây là vấn đề mà trong bất kỳ truy vấn nhất định nào, bạn thường không biết chính xác bảng nào để tham gia. Nếu bạn đang tìm kiếm một cầu thủ bóng đá, bạn nên sử dụng bảng cầu thủ bóng đá, nhưng nếu bạn đang tìm kiếm một nhóm cầu thủ, bạn sẽ sử dụng bảng nào? Để tham gia hiệu quả khi một số bảng không có dữ liệu, bạn sẽ cần thực hiện một phép nối bên ngoài, thao tác này không chuẩn và thường chậm. Thay vào đó là đọc bảng gốc trước và sau đó sử dụng mã để tìm ra bảng nào sẽ đọc tiếp theo, nhưng điều này liên quan đến nhiều truy vấn.

#### When to Use It

Class Table Inheritance, Single Table Inheritance và Concrete Table Inheritance là ba lựa chọn thay thế để xem xét cho ánh xạ kế thừa.

Điểm mạnh của Class Table Inheritance là
- Tất cả các cột đều có liên quan cho mọi hàng để các bảng dễ hiểu hơn và không lãng phí không gian.
- Mối quan hệ giữa mô hình miền (domain model) và cơ sở dữ liệu rất đơn giản.

Điểm yếu của Class Table Inheritance là
- Bạn cần chạm vào nhiều bảng để tải một đối tượng, có nghĩa là một phép nối hoặc nhiều truy vấn và may (sewing) trong bộ nhớ.
- Bất kỳ cấu trúc lại nào của các trường lên hoặc xuống hệ thống phân cấp đều gây ra các thay đổi cơ sở dữ liệu.
- Các bảng supertype có thể trở thành một nút cổ chai vì chúng phải được truy cập thường xuyên.
- Mức độ chuẩn hóa cao có thể gây khó hiểu cho các truy vấn đặc biệt.

Bạn không phải chỉ chọn một mẫu ánh xạ kế thừa cho một hệ thống phân cấp lớp. Bạn có thể sử dụng Class Table Inheritance cho các lớp ở trên cùng của hệ thống phân cấp và một loạt Concrete  Table  Inheritance cho những lớp thấp hơn.

#### Further Reading

Một số văn bản của IBM gọi mô hình này là Root-Leaf Mapping [Brown et al.].

#### Example: Players and Their Kin (C#)

Đây là cách triển khai cho bản phác thảo. Một lần nữa, tôi sẽ làm theo cách quen thuộc (nếu có lẽ hơi tẻ nhạt) của những người chơi và họ thích, bằng cách sử dụng Inheritance Mappers (302).

Mỗi lớp cần xác định bảng chứa dữ liệu của nó và mã kiểu cho nó.

{% highlight csharp %}
class AbstractPlayerMapper...
	abstract public String TypeCode {get;}
	protected static String TABLENAME = "Players";

class FootballerMapper...
	public override String TypeCode {
		get {return "F";}
	}
	protected new static String TABLENAME = "Footballers";
{% endhighlight %}

Để có mô tả đầy đủ, hãy xem [Patterns of Enterprise Application Architecture](https://martinfowler.com/books/eaa.html) trang 285



## Concrete Table Inheritance

> Đại diện cho một hệ thống phân cấp kế thừa của các lớp với một bảng cho mỗi lớp cụ thể trong hệ thống phân cấp.

![Concrete Table Inheritance](https://boxxv.github.io/img/db/concreteTableInheritance.png "Concrete Table Inheritance")

Như bất kỳ người theo chủ nghĩa đối tượng nào sẽ nói với bạn, cơ sở dữ liệu quan hệ không hỗ trợ kế thừa - một thực tế làm phức tạp việc ánh xạ quan hệ đối tượng. Suy nghĩ về các bảng từ một quan điểm đối tượng, một lộ trình hợp lý là lấy từng đối tượng trong bộ nhớ và ánh xạ nó vào một hàng cơ sở dữ liệu duy nhất. Điều này ngụ ý Concrete Table Inher-itance, nơi có một bảng cho mỗi lớp cụ thể trong hệ thống phân cấp kế thừa.

Tôi thú nhận là đã gặp một số khó khăn khi đặt tên cho mẫu này. Hầu hết mọi người nghĩ về nó như là định hướng lá vì bạn thường có một bảng cho mỗi lớp lá trong một hệ thống phân cấp. Theo logic đó, tôi có thể gọi đây là kế thừa bảng mẫu lá và thuật ngữ `"leaf"` thường được sử dụng cho mẫu này. Tuy nhiên, một cách nghiêm túc, một lớp cụ thể không phải là một chiếc lá cũng thường có một bảng, vì vậy tôi quyết định sử dụng thuật ngữ đúng hơn, nếu ít trực quan hơn.

#### How It Works

Concrete Table Inheritance sử dụng một bảng cơ sở dữ liệu cho mỗi lớp concrete trong hệ thống phân cấp. Mỗi bảng chứa các cột cho lớp cụ thể và tổ tiên của nó, vì vậy bất kỳ trường nào trong lớp cha đều được sao chép trên các bảng của lớp con. Như với một số lược đồ kế thừa này, hành vi cơ bản sử dụng Trình lập bản đồ kế thừa (302).

Bạn cần chú ý đến các keys có mô hình này. Thật tuyệt vời, điều quan trọng là đảm bảo rằng các khóa là duy nhất không chỉ cho một bảng mà cho tất cả các bảng từ một hệ thống phân cấp. Một ví dụ cổ điển về nơi bạn cần điều này là nếu bạn có một bộ sưu tập người chơi và bạn đang sử dụng Trường danh tính (Identity) với các keys toàn bảng (table-wide). Nếu các khóa có thể được sao chép giữa các bảng ánh xạ các lớp cụ thể, bạn sẽ nhận được nhiều hàng cho một giá trị khóa cụ thể. Do đó, bạn cần một hệ thống phân bổ khóa theo dõi việc sử dụng khóa trên các bảng; ngoài ra, bạn không thể dựa vào cơ chế duy nhất khóa chính của cơ sở dữ liệu.

Bạn có thể giải quyết một số vấn đề này bằng cách không có các trường được nhập vào lớp cha, nhưng rõ ràng điều đó làm tổn hại đến mô hình đối tượng. Thay vào đó là có trình truy cập cho supertype trong giao diện nhưng sử dụng một số trường riêng cho từng loại cụ thể trong quá trình triển khai. Sau đó, giao diện kết hợp các giá trị từ các trường riêng tư. Nếu giao diện công khai là một giá trị duy nhất, nó sẽ chọn bất kỳ giá trị nào trong số các giá trị riêng tư không rỗng. Nếu giao diện công khai là một giá trị tập hợp, nó sẽ trả lời với sự kết hợp của các giá trị từ các trường triển khai.

Đối với khóa ghép, bạn có thể sử dụng một đối tượng khóa đặc biệt làm trường ID của mình cho Trường danh tính. Khóa này sử dụng cả khóa chính của bảng và tên bảng để xác định tính duy nhất.

Liên quan đến vấn đề này là các vấn đề với tính toàn vẹn tham chiếu trong cơ sở dữ liệu. Hãy xem xét một mô hình đối tượng như Hình 12.10. Để triển khai tính toàn vẹn của tham chiếu, bạn cần một bảng liên kết chứa các cột khóa ngoại cho chức năng từ thiện và cho trình phát. Vấn đề là không có bàn cho cầu thủ, vì vậy bạn không thể đặt cùng nhau một ràng buộc toàn vẹn tham chiếu cho trường khóa ngoại có cả cầu thủ bóng đá hoặc cầu thủ cricket. Lựa chọn của bạn là bỏ qua tính toàn vẹn của tham chiếu hoặc sử dụng nhiều bảng liên kết, một bảng cho mỗi bảng thực tế trong cơ sở dữ liệu. Trên hết, bạn gặp vấn đề nếu không thể đảm bảo tính duy nhất của khóa.

Nếu bạn đang tìm kiếm người chơi bằng câu lệnh select, bạn cần phải xem tất cả các bảng để xem bảng nào chứa giá trị thích hợp. Điều này có nghĩa là sử dụng nhiều truy vấn hoặc sử dụng kết nối bên ngoài, cả hai đều không tốt cho hiệu suất. Bạn không bị ảnh hưởng về hiệu suất khi bạn biết lớp mình cần, nhưng bạn phải sử dụng lớp cụ thể để cải thiện hiệu suất.

Mô hình này thường được gọi là dọc theo các đường kế thừa bảng leaf. Một số người thích một biến thể trong đó bạn có một bảng cho mỗi lớp leaf thay vì một bảng cho mỗi lớp cụ thể. Nếu bạn không có bất kỳ lớp cha cụ thể nào trong hệ thống phân cấp, điều này sẽ xảy ra tương tự. Ngay cả khi bạn có các lớp siêu cụ thể, sự khác biệt là khá nhỏ.

#### When to Use It

Khi tìm ra cách lập bản đồ kế thừa, Concrete Table Inheritance, Class Table Inheritance và Single Table Inheritance là những lựa chọn thay thế 

Điểm mạnh của Kế thừa Bảng Concrete là:
- Mỗi bảng là độc lập và không có trường không liên quan. Do đó, nó có ý nghĩa tốt khi được sử dụng bởi các ứng dụng khác không sử dụng các đối tượng. 
- Không có liên kết nào để thực hiện khi đọc dữ liệu từ các trình vẽ bản đồ cụ thể. 
- Mỗi bảng chỉ được truy cập khi lớp đó được truy cập, điều này có thể tản ra tải trọng truy cập.

Điểm yếu của Kế thừa Bảng Concrete là:
- Các khóa chính có thể khó xử lý.
- Bạn không thể thực thi các mối quan hệ cơ sở dữ liệu đối với các lớp trừu tượng.
- Nếu các trường trên các lớp domain được đẩy lên hoặc xuống hệ thống phân cấp, bạn phải thay đổi các định nghĩa bảng. Bạn không phải thực hiện nhiều thay đổi như với Kế thừa bảng Class, nhưng bạn không thể bỏ qua điều này khi có thể với Kế thừa bảng Single.
- Nếu một trường lớp cha thay đổi, bạn cần thay đổi từng bảng có trường này vì các trường lớp cha được trùng lặp trên các bảng.
- Một phát hiện trên lớp cha buộc bạn phải kiểm tra tất cả các bảng, điều này dẫn đến nhiều quyền truy cập cơ sở dữ liệu (hoặc một phép nối kỳ lạ).

Hãy nhớ rằng bộ ba mẫu kế thừa có thể cùng tồn tại trong một hệ thống phân cấp duy nhất. Vì vậy, bạn có thể sử dụng Kế thừa Bảng Concrete cho một hoặc hai lớp con và Kế thừa Bảng Single cho phần còn lại.


Để có mô tả đầy đủ, hãy xem [Patterns of Enterprise Application Architecture](https://martinfowler.com/books/eaa.html) trang 293


## Serialized LOB

> Lưu một biểu đồ của các đối tượng bằng cách tuần tự hóa chúng thành một đối tượng lớn duy nhất (LOB), nó lưu trữ trong một trường cơ sở dữ liệu. 

![Serialized LOB](https://boxxv.github.io/img/db/serializedLOB.png "Serialized LOB")

Các mô hình đối tượng thường chứa các đồ thị phức tạp của các đối tượng nhỏ. Phần lớn thông tin trong các cấu trúc này không nằm trong các đối tượng mà nằm trong các liên kết giữa chúng. Cân nhắc lưu trữ hệ thống phân cấp tổ chức cho tất cả khách hàng của bạn. Một mô hình đối tượng hiển thị khá tự nhiên mô hình thành phần để đại diện cho phân cấp hữu quan và bạn có thể dễ dàng thêm các phương thức cho phép bạn lấy tổ tiên, anh chị em, con cháu và các mối quan hệ phổ biến khác.

Không dễ dàng như vậy là đưa tất cả những điều này vào một lược đồ quan hệ. Lược đồ cơ bản rất đơn giản - một bảng tổ chức có khóa ngoại chính, tuy nhiên, việc thao tác với lược đồ của nó yêu cầu nhiều phép nối, điều này vừa chậm vừa khó.

Các đối tượng không nhất thiết phải được duy trì dưới dạng các hàng bảng liên quan đến nhau. Một hình thức liên tục khác là tuần tự hóa, trong đó toàn bộ đồ thị của các đối tượng được viết ra dưới dạng một đối tượng lớn duy nhất (LOB) trong một bảng, LOB được tuần tự hóa này sau đó trở thành một dạng vật lưu niệm [Gang of Four].

Để có mô tả đầy đủ, hãy xem [Patterns of Enterprise Application Architecture](https://martinfowler.com/books/eaa.html) trang  272


## Entity-Attribute-Value

EAV Pattern Là một kỹ thuật thiết kế CSDL để đáp ứng được việc xây dựng, phát triển và mở rộng sản phẩm khi hệ thống yêu cầu có sự tùy biến cao.

Thực thể-Thuộc tính-Giá trị, Một bảng cho Sản phẩm và một bảng xoay các thuộc tính thành hàng, thay vì cột. EAV không phải là một thiết kế hợp lệ đối với mô hình quan hệ, nhưng nhiều người vẫn sử dụng nó. Đây là “Mô hình thuộc tính” được đề cập bởi một câu trả lời khác. Xem các câu hỏi khác với thẻ [eav](https://stackoverflow.com/questions/tagged/entity-attribute-value?tab=Active) trên StackOverflow để biết một số cạm bẫy.

![Entity-Attribute-Value Pattern](https://boxxv.github.io/img/db/eav.png "Entity-Attribute-Value Pattern")

Các phần phần tham gia vào EAV:
- **Entity (entities)**: Bảng chứa thông tin cơ bản của đối tượng
- **Attribute (attributes)**: Bảng chứa các thuộc tính ta có thể thêm vào
- **Value (attribute_values)**: Bảng chứa tổng hợp giá trị của cả Entity và Attribute với 2 khóa ngoại được tham chiếu đến

Mối quan hệ giữa các bảng:
- **Value - Attribute**: 1-n (một Attribute có nhiều Value)
- **Value - Entity**: n-n (một Entity có nhiều Value, một Value thuộc nhiều Entity)
- **Entity - Attribute**: n-n (một sản phẩm có nhiều Attribute, một Attribute thuộc nhiều sản phẩm)

Ví dụ về mối quan hệ giữa Entity-Attribute-Value:

| value_id | entity_id | value | attribute_id |
| -- | -- | -- | -- |
| 1 | 1 | "S" | 1 |
| 2 | 1 | "Trắng" | 2 |
| 3 | 1 | 30 | 3 |
| 4 | 1 | 100 | 4 |
| 5 | 2 | "S" | 1 |
| 6 | 2 | "Đen" | 2 |
| 7 | 2 | 20 | 3 |
| 8 | 2 | 200 | 4 |

[https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model](https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model)

[Tìm hiểu về Entity-Attribute-Value Pattern (EAV) (Structural Pattern)](https://viblo.asia/p/tim-hieu-ve-entity-attribute-value-pattern-eav-structural-pattern-Eb85okV452G)


-----
[Database Schema for Multiple Types of Products](https://www.codingblocks.net/programming/database-schema-for-multiple-types-of-products/)  
[How to design a product table for many kinds of product where each product has many parameters](https://stackoverflow.com/questions/695752/how-to-design-a-product-table-for-many-kinds-of-product-where-each-product-has-m)  
[Mô hình cơ sở dữ liệu EAV giải quyết bài toán các thực thể có số lượng các thuộc tính thay đổi](https://viblo.asia/p/mo-hinh-co-so-du-lieu-eav-giai-quyet-bai-toan-cac-thuc-the-co-so-luong-cac-thuoc-tinh-thay-doi-naQZRyLPKvx)


